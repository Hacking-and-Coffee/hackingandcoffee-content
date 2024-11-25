---
title: "Red Team Laptop & Infrastructure (pt 1: Architecture)"
date: 2018-02-28
draft: true
author_image: 'images/about.jpg'
author: 'hon1nbo'
---

I get a lot of questions about my laptop, ranging from “Windows or Mac?” to “do you have a preferred chipset for Ethernet NICs.”

Well, with the exception of “neither” to the first question, most things will vary. Rather than talk about specific hardware or version choices, I’m going to talk about Architecture; in future posts I’ll talk about specific ways of implementing my Infrastructure architecture for supporting penetration testing, but for now we will focus on the high level. This design is Reasonably secure in the right hands, fast, and extremely flexible.


# Requirements
Let’s start with some basic requirements for an assessment laptop.

- Reasonably Secure
- Granular network control
- Access to assessment firm domain / internal resources, whilst having access to client side systems
- Long term storage of tools, documents, and other artifacts
- Tech Agnostic
  
That last item tends to be the tricky part; in red teaming, one never knows what they will encounter and usually they will want the most capability on hand, and no restrictions on what their machine can talk with or plug into. At the same time, said things being plugged into may pose hazards, especially to machines that have multiple client tenants.

# The Architecture

TKTK Photo

Laptop Architecture

### High-Level Breakdown
At a high level, the pentesting laptop is basically a hypervisor with a minimalist user interface, and all the actual work is broken up into VMs. Before anyone says “This is Qubes!,” the issue here is that the Xen beneath Qubes doesn’t get a long with some items in the field, and this has a far higher level of granularity. Qubes’ design, and best role, is a defensive endpoint; it is not designed for offensive work, and does not contain the testing required to ensure a stable build like Kali Linux for purposes such as pentesting and exploitation. I’m still keeping my eye on the Qubes project though in general, and do run it on some of my other hardware.

Each client or project is given a linked clone of the associated base VM. This allows for lighter disk space requirements, as well as ensures only a few VMs need to be regularly updated and configured.

We have three networking zones, and one independent VM.

- PfSense independent VM
- Trust zone
- DMZ
- Dirty Zone

### Networking
The PfSense controls routing between the zones, of which Trust contains items such as a Domain joined windows box for internal corporate access, as well as VMs containing proprietary items; the DMZ contains items that aren’t explicitly malicious, but not trusted either. This is general web browsing, scouring for known exploits in what may turn out to be unsavory places, etc; then there is the Dirty zone, from which all attack traffic and malware originates or is inspected. Zones can talk to only the network resources they need, and nothing else, and are enforced through the PfSense firewall. The Trust zone is only granted outbound to the corporate VPN endpoints; the DMZ has general internet access, but nothing else; and the Dirty zone is granted access to the clients’ networks for their respective work.

Wait, “clients” plural? This is where this architecture really shines. Often, a team will find members are pulling double duty with multiple clients. Sometimes is because of license limitations needed across multiple projects, sometimes it’s just the availability of the talent. Regardless, we can all agree that it would be bad of attack traffic for one client started hitting another. Let’s face it. VPNs suck; they drop, they stutter, and clients often have vastly different ideas of what traffic can go over them. Some clients provide VPNs that tunnel everything, some only provide VPNs that tunnel items in their address range. This means that, in the end, you can end up with a lot of traffic go over the local network that is undesirable. Such traffic can get you caught easily by even crappy network monitoring systems, and some may choose to take down something it shouldn’t.

Using PfSense, we can create rules for where each specific VM can go out to. No out of scope items sent, no dangerous exploits mistakenly sent to that delicate legacy system rather than that stubborn system you’ve been poking at.

# Practical Hardening
We all know that theoretically a hypervisor is robust and secure; practically, things are a bit more complicated than that. The most common exploits are usually environmental rather than on the core hypervisor: VM extensions like copy/paste and virtualized interfaces, or attacks like Spectre. However, the systems can still be reasonably secure. Most importantly, they can be reasonably secure whilst still being usable.

### Disk Encryption
Full Disk Encryption (FDE) is a matter of debate among some experts. Should I use something like LUKS (software FDE)? Should I splurge for an OPAL compliant Self Encrypting Drive (SED)?

Well, the answer will depend partly on your threat model, and choice of hardware other than the drive itself. Software FDE is known vulnerable to cold boot attacks on s1-3 sleep states or a locked screen, and when Direct Memory Access (DMA) interfaces are available. These DMA interfaces include Firewire, Thunderbolt, USB 3.0+, and PCIe. Exploiting these, depending on the system configuration, is possible but not always trivial. SEDs are resistant to these attacks, the key is never in memory, and there is zero performance hit. However, they are vulnerable to a hot swap attack in which the data lines are connected to a different machine whilst keeping the drive powered and unlocked.

Attacking SEDs versus software FDE systems is well documented and out of the scope of this write up. Personally, I chose to go the SED route, as my laptop hardware enforces a drive power cut for it’s OPAL configuration on soft reboots and data loss. However, this should be evaluated based on your hardware at hand.

### Extensions
The guest extensions are a must when using the desktop environments rather than headless VMs, but we can mitigate the risks. Items such as copy/paste are disabled by default, and enabled on a case by case basis. Simple enough

But what about the Shared Folders? The host machine may have, across all VMs and storage, a history of clients, reports, and exploits that are not yet public. Kali Linux, on the other hand, is not a very secure OS (though it can be; stop running everything as root!). How can we mitigate attacks?

First off, don’t mount folders unless you have to; I set my base images to have the configurations for it but disable auto-mounting. When a VM needs it, I flip the switch and specific a specific path.

Second, mount the shared folder on the host with a local bind. Using this, one can set an enforced fmask, dmask, and noexec that disables execute bits on files and enforces permissions. This prevents a VM from writing items in another user’s context on the host machine, and from the setting of execute / setuid bits on files. It’s a neat trick, and using the local bind allows for doing this to specific folders on the host machine. If storing data on a separate partition, mount the partition using the normal means with these flags rather than a bind.

Look, we’ve already solved the practical attack vectors!

# The Bigger Architecture
In the bigger scheme of things, having a local kick-ass laptop build is nice but it can do more. Let’s take a look at how I tied this into a red team support infrastructure.

TKTK photo

Infrastructure Architecture

In the support infrastructure we have a PfSense image running in a provider such as Google Cloud, with backend C2. This can, of course, run on any externally available environment.

Using site-to-site tunnels, we can secure all the VMs on the laptops without burdening each one with a VPN connection individually, rather letting the PfSense image handle the load. This helps mitigate effects VPN tun and tap interfaces have on toolchains, which often break as the local network changes. At the same time, the external address of the cloud PfSense image is accessible to our C2 payloads, such as Beacon.

But let’s say your tool needs a direct callback; thanks to the site-to-site, the cloud PfSense can forward the connection to the respective red team member. Each team member can open ports and forward as needed, either to their laptop (which the local PfSense can send to a specific VM), or to a backend compute instance such as a Cobalt Strike  teamserver. It is always recommended to separate various red team phases into separate servers, and thanks to multi-WAN support in PfSense, the same routers and rule systems can handle multiple C2 points between the same team and set of resources, following the entire engagement life cycle.

At a high level, this is how I run most of my infrastructure for a red team engagement; in the future I’ll write up some specifics on how to get it running. PfSense has amazing documentation, and I wholeheartedly recommend it for anyone who needs a featureful and reliable routing and firewall system.

Cheers,

~H
