# Hacking and Coffee Content

This repository contains all the content for the Hacking and Coffee site, including blog posts, images, and other media. It is structured to work seamlessly with the Hugo static site generator.

## Repository Structure

- **Content**: All markdown files for blog posts, pages, and art pieces are stored in the `content` directory in their respective directories.
- **Images and Media**: Store images and other media files within the respective content directories. This ensures they are accessible and organized alongside their related content.

## Adding New Content

To add a new blog post, project, or art piece, create a new directory or markdown file under the appropriate subdirectory in `content`. Each directory should contain a markdown file and any associated images. Use the following front matter template to ensure consistency:

```yaml
---
title: "Your Post Title"
date: MM-DD-YYYY
draft: true
tags: ["tag1", "tag2"]
categories: ["category1"]
authors: ['hon1nbo']
---
```

- **Title**: The title of your post.
- **Date**: The publication date in `MM-DD-YYYY` format.
- **Draft**: Set to `true` if the post is a draft and should not be published.
- **Tags**: A list of tags for categorizing the post.
- **Categories**: A list of categories for organizing the post.
- **Authors**: A list of authors that worked on the post.

### Art Gallery Specific Front Matter

The art gallery comes with it's own specific frontmatter to include in the `_index.md` markdown file for each image.

```yaml
---
title: "The title of the art piece"
date: MM-DD-YYYY
draft: true
tags: ["tag1", "tag2"]
categories: ["category1"]
artists: ["Artist Name"]
link: "https://furaffinity.net/view/1234567890"
---
```

- **Title**: The title of the art piece.
- **Date**: The publication date in `MM-DD-YYYY` format.
- **Draft**: Set to `true` if the post is a draft and should not be published.
- **Tags**: A list of tags for categorizing the post.
- **Categories**: A list of categories for organizing the post.
- **Artists**: A list of artists who worked on the piece.
- **Link**: A link to the art piece.

## Managing Media

- **Blog Posts and Projects**: Place images in the same directory as the markdown file for the post or project. Reference these files in your markdown content using relative paths:

  ```markdown
  ![Alt text](./your-image.jpg)
  ```

- **Art Gallery**: Each art piece should have its own directory containing a markdown file and an image. 

## Development Workflow

When working on content, ensure that your local Hugo server is running to preview changes. Use the following command in the main site repository:

```bash
npm run dev
```

This will start the Hugo server and watch for changes in your content files, automatically rebuilding the site and refreshing your browser.

## Additional Information

- **Hugo Content Management**: [https://gohugo.io/content-management/](https://gohugo.io/content-management/)