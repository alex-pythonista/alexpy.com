# Content Creation Guide

This guide covers how to create and manage content for your Hugo site using the hugo-theme-console theme.

## Table of Contents
1. [Creating Blog Posts](#creating-blog-posts)
2. [Creating Pages](#creating-pages)
3. [Creating Photo Gallery](#creating-photo-gallery)
4. [Front Matter Reference](#front-matter-reference)
5. [Content Organization](#content-organization)

---

## Creating Blog Posts

### Quick Start

```bash
# Create a new blog post
hugo new posts/my-post-title.md
```

This creates `content/posts/my-post-title.md` with default front matter.

### Post Structure

```markdown
+++
title = "My Amazing Blog Post"
date = "2026-01-10"
draft = false
+++

This is the introduction paragraph that will appear in the post summary on the homepage.

<!--more-->

This is the rest of your content that appears only on the full post page.

## Heading 2
Your content here...

### Heading 3
More content...

- Bullet points
- Work great
- For lists

1. Numbered lists
2. Also work
3. Perfectly
```

### Key Points

- **File location**: `content/posts/your-post-name.md`
- **URL**: `https://alexpy.com/posts/your-post-name/`
- **Draft status**: Set `draft = false` to publish
- **Summary split**: Use `<!--more-->` to control what appears in post previews
- **Date format**: `YYYY-MM-DD` or `YYYY-MM-DDTHH:MM:SS+TZ`

### Publishing Workflow

1. Create the post: `hugo new posts/my-post.md`
2. Edit the file in `content/posts/my-post.md`
3. Set `draft = false` when ready to publish
4. Test locally: `hugo serve`
5. Build for production: `hugo --minify`

---

## Creating Pages

### About Page

The about page is special - it appears on both the homepage and at `/about/`.

**File**: `content/about/_index.md`

```markdown
+++
title = "About"
date = "2026-01-10"
draft = false
+++

Hi, I'm Alex Py! This is my personal website where I share my thoughts and projects.

I'm a [your profession/passion]. You can find me on [links to social media].

## What I Do

- Thing 1
- Thing 2
- Thing 3

## Contact

Email: your@email.com
```

**Note**: The first paragraph appears on the homepage automatically.

### Custom Pages

Create any custom page:

```bash
# Creates content/contact/_index.md
hugo new contact/_index.md
```

Then add it to your navigation in `hugo.toml`:

```toml
[[params.navlinks]]
  name = "Contact"
  url = "/contact/"
```

---

## Creating Photo Gallery

### Directory Structure

Each photo should be in its own directory with an `index.md` file:

```
content/photos/
├── _index.md                    # Photos section index (optional)
├── vacation-2026/
│   ├── index.md                 # Photo metadata
│   └── beach-sunset.jpg         # The actual photo
├── city-walk/
│   ├── index.md
│   └── downtown.jpg
└── nature/
    ├── index.md
    └── mountain-view.jpg
```

### Creating a Photo Entry

```bash
# Create the directory
mkdir -p content/photos/my-photo-name

# Create the metadata file
hugo new photos/my-photo-name/index.md

# Copy your photo into the directory
cp /path/to/your/photo.jpg content/photos/my-photo-name/
```

### Photo Front Matter

**File**: `content/photos/my-photo-name/index.md`

```markdown
+++
image = "photo-filename.jpg"
date = "2026-01-10"
title = "Sunset at the Beach"
type = "gallery"
draft = false
+++

A beautiful sunset I captured during my vacation in Hawaii.
The colors were absolutely stunning that evening.

## Photo Details
- Location: Waikiki Beach, Hawaii
- Camera: Sony A7III
- Date taken: January 10, 2026
```

### Key Photo Requirements

- **`type = "gallery"`**: Required for photos to display correctly
- **`image = "filename.jpg"`**: Must match the actual filename in the directory
- **File location**: Photo and `index.md` must be in the same directory
- **Supported formats**: JPG, PNG, WebP

---

## Front Matter Reference

### Common Fields

```toml
+++
title = "Content Title"           # Required: Page/post title
date = "2026-01-10"               # Required: Publication date
draft = false                     # Required: false to publish, true to hide
+++
```

### Blog Post Specific

```toml
+++
title = "My Post"
date = "2026-01-10"
draft = false
tags = ["hugo", "webdev"]         # Optional: Post tags
categories = ["tutorials"]        # Optional: Post categories
+++
```

### Photo Gallery Specific

```toml
+++
title = "Photo Title"
date = "2026-01-10"
draft = false
type = "gallery"                  # Required: Marks as gallery item
image = "photo.jpg"               # Required: Filename of the image
+++
```

### Privacy Control

```toml
+++
title = "Private Post"
date = "2026-01-10"
draft = false
private = true                    # Hides from homepage listings
+++
```

---

## Content Organization

### Directory Structure

```
content/
├── about/
│   └── _index.md                 # About page
├── posts/
│   ├── _index.md                 # Posts section page (optional)
│   ├── 2026-01-10-first-post.md  # Individual posts
│   ├── 2026-01-15-second-post.md
│   └── tutorial-series/
│       └── index.md              # Organized in subdirectories
├── photos/
│   ├── _index.md                 # Photos section page (optional)
│   ├── photo-1/
│   │   ├── index.md
│   │   └── image.jpg
│   └── photo-2/
│       ├── index.md
│       └── image.jpg
└── projects/                     # Custom section
    ├── _index.md
    └── my-project.md
```

### File Naming Conventions

**Blog Posts**:
- `my-post-title.md` - Simple naming
- `2026-01-10-my-post.md` - Date-prefixed (helps with sorting)
- `series-name/part-1.md` - Organized in subdirectories

**Pages**:
- `_index.md` - Section index page (e.g., `/about/`, `/posts/`)
- `page-name.md` - Individual page

### Content Tips

1. **Use meaningful filenames**: They become part of the URL
2. **Organize by topic**: Use subdirectories for related content
3. **Add front matter carefully**: TOML format requires `+++` delimiters
4. **Test locally first**: Always run `hugo serve` before publishing
5. **Keep drafts**: Use `draft = true` while working on content

---

## Quick Reference Commands

```bash
# Start local development server
hugo serve

# Create new blog post
hugo new posts/my-post-name.md

# Create new page
hugo new about/_index.md

# Create new photo entry
hugo new photos/photo-name/index.md

# Build for production
hugo --minify

# Build including drafts (for preview)
hugo serve -D
```

---

## Homepage Display

The homepage (`/`) automatically shows:
- **About section**: First paragraph from `content/about/_index.md`
- **Latest posts**: 3 most recent posts from `content/posts/`
- **Latest photos**: 3 most recent photos from `content/photos/`

To control what appears:
- Edit `content/about/_index.md` for the intro
- Posts marked with `private = true` won't appear in listings
- Only published content (`draft = false`) appears on the homepage

---

## Troubleshooting

### Content not showing up?
- Check `draft = false` in front matter
- Verify file is in correct directory
- Run `hugo serve` and check terminal for errors

### Photo not displaying?
- Verify `type = "gallery"` is set
- Check `image = "filename.jpg"` matches actual filename
- Ensure photo and `index.md` are in same directory

### Homepage not updating?
- Content with `private = true` won't show
- Only latest 3 posts/photos appear
- Clear browser cache and refresh

---

## Additional Resources

- Hugo Documentation: https://gohugo.io/documentation/
- Theme Repository: https://github.com/mrmierzejewski/hugo-theme-console
- Markdown Guide: https://www.markdownguide.org/