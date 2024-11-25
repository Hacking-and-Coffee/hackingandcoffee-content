---
title: "Unique Policy of Transferring Usernames by Telegram"
date: 2017-06-01
draft: false
author_image: 'images/about.jpg'
author: 'hon1nbo'
---

Telegram has been around for a little while now, and its user base is growing. However, despite their attempts to be the secure system to beat out the larger social networks, they have one particularly alarming policy: They will transfer a username unilaterally from an established account to another.

It recently came to the attention of a larger audience after a user, who had the handle *@saman*, had his account taken over by someone who claimed the handle on other services, described in detail in a [Medium post](https://medium.com/@saman/how-telegram-took-my-unique-username-40aa7507d45c).That user was in fact acting maliciously, however Telegram’s official policy would affect users even in cases where the other accounts are legitimate. [Here is the verbatim policy](https://telegram.org/faq#q-what-do-i-do-if-my-username-is-taken), reproduced below:

> ### Q: What do I do if my username is taken?
> Telegram usernames are distributed on a first come — first serve basis.
> >
> We understand that certain usernames are part of an online identity for some of us. If your desired username is already taken, we will be happy to help you acquire it for your account or channel, provided that you have that same username on at least two of these services: Facebook, Twitter, Instagram.

## This is concerning to say the least
I wrote an {initial response on Telegra.ph](https://telegra.ph/Why-the-saman-case-is-serious-05-31), however it was not comprehensive and covered only one case (poorly I might add, since it was written quickly I implied that a conversation already existed in a current state when I said they talk regularly).

So here I present a set of conditions this policy does not account for, and reasons why most large providers have set a long agreed upon industry standard for *not* reissuing usernames or handles.

Let’s have the following users:
- **Bob**: the user who had @bob taken from him
- **Alice**. A potential victim, and a friend of Bob’s
- **Charlie**: A potential victim, who has not yet talked with Bob on Telegram but Bob already had shared contact details with. Could be a business contact, an acquaintance, etc
- **Eve**: The Evil user, who wants to either impersonate Bob as a goal, or convince Alice or Charlie of something using Bob’s trusted status amongst them

Let’s also have the following conditions to exploit this:
- Bob does not have his handle registered on at least two of the three services Telegram describes. Bob may not have these because he is unaware of the Telegram policy and simply does not use them, the services are blocked in his geopolitical region (government censorship, etc), he may not want his real name tied with this handle for privacy or safety reasons (LGBTQ discrimination, abusive ex-partners, etc. Facebook Real Name Policy), or he may not want to violate their terms of service by opening an account purely to squat on the handle when not using that particular service (Instragram ToS, using a fake name on Facebook)
-- n.b: none of the services Telegram allows for this to “verify” who should have the account themselves allow a handle to be taken in such a fashion, as industry standards dictate. The only exception is Trademark disputes, which require legal action and only apply in cases where the username was originally registered with Malice.
- Eve can register the handle on the services. This is considered a trivial action, as Eve is not acting within the law necessarily and may break Terms of Service to create such accounts.

- So what does Eve do after registering the handles on two of the three services? She only has to request that Telegram transfer the handle to her.

Bob receives the notice, but none of his contacts do. There are two possible ways a contact knows that Bob has lost his handle:

- If Bob can communicate it manually to all of them, or there are a lot of contacts (Bob may miss one).
- If Bob and the contact have an established conversation that is currently active, but this assumes a user never resets their device, that they don’t clean up conversations that have not had activity in some time, nor that there is an established contact in the first place (not possible if a handle is provided on say a business card, and that user has not contacted him yet). Items like Business Cards have long spans in which they may still be used by the recipient, similar to how long users may inadvertently messaged an old email address not knowing if the user had moved on. Hence, why organizations like Google do not reassign email users.

This can cause a lot of havoc, especially in the case where one has, I don’t know, dropped over a thousand business cards at networking events with that handle? Or if someone has had this handle listed on every major service they use (which, as the Streisand Effect shows, even if trying hard the Internet never forgets as it is cached somewhere, somehow).

Below is a basic attack path for a common conversation amongst furries with an established handle (at least allegedly around me… don’t know why people say they see me at FurCons, or why people say I have a purple tail and ears. I find the accusations outrageous).

![Basic Telegram Handle Theft Attack](/images/telegram_attack_path_01.webp)

See how this can quickly become a problem? Since Charlie does not have Bob as a phone contact, the handle is the only method of opening a communication channel. @Charlie would have no way of knowing about the name change. Why does Telegram allow this?  Telegram don’t have a clear answer to why they believe this is a non-issue.. They say the policy is as it is because their legal team is small, but if there was an actual Trademark dispute then it would be a different scenario in the first place (and a court makes that determination, not Telegram). I have had some interesting discussions on twitter, but no productive explanation came of it. Some defending Telegram blame IG/FB for something that they have no control over (i.e. Telegram’s policy choice), but that has not been an official answer either (and would be an unacceptable one if they officially said that)

I guess I’ll wait to see how this plays out in the long term. I already found some juicy targets should I be more than *thinking* maliciously, and chose to act. I hope Telegram chooses to make the right decision and get with the rest of the major players in handling username transfers (i.e. don’t).

One other comment, though not from Telegram, was that this policy had been in place for 4 years and this was the first trouble. Well, this is a common argument amongst developers in general for considering something a non-issue.  It is not a good argument; it just means there hasn’t been incentive to exploit it yet (either due to user base size, or lack of interest). There are well documented cases of stealing user handles (including the extremely rare single character twitter handles). At the same time, I have seen this argument made for reasons not to patch critical systems, and not deploying best practice. My personal favourite has been a client that claimed “we won’t fix this because it’s behind a firewall & VPN, so these trivial RCEs are not exploitable.” Now, I didn’t say it was easy to exploit, but they were trivial to fix as well but the developers wanted to push features in that change window instead of fixes. Well, I got a good laugh a week or so later when an 0day for that particular firewall dropped, and sure enough they got pwned almost instantly. I guess Karma has a good sense of humor.

