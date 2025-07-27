# Git it Write - Quick Reference Guide

## Essential Syntax

### File Creation
```markdown
filename.md → /filename/ (WordPress URL)
directory/index.md → /directory/ (WordPress URL)
```

### Front Matter (YAML)
```yaml
---
title: "Post Title"           # Required
post_status: publish          # publish|draft|pending|future
menu_order: 1                 # Integer for ordering
post_excerpt: "Summary"       # Meta description
post_date: "2024-01-15 10:30:00"  # Publication date
comment_status: open          # open|closed
page_template: "template.php" # Custom template
stick_post: yes              # yes|no
skip_file: yes               # yes|no (skip processing)
taxonomy:
  category: [cat1, cat2]     # Categories
  post_tag: [tag1, tag2]     # Tags
custom_fields:
  key: "value"               # Custom metadata
---
```

## Content Formatting

### Images
```markdown
![Alt text](/_images/filename.jpg "Optional title")
![Diagram](/_images/diagrams/flow.png)
```

### Links
```markdown
[Text](./relative-file.md)      # Same directory
[Text](../parent/file.md)       # Parent directory
[Text](/absolute/path/file.md)  # Absolute path
```

### Markdown Basics
```markdown
# H1 Header
## H2 Header
### H3 Header

**Bold text**
*Italic text*
`Inline code`

- Bullet list
1. Numbered list

[Link text](URL)
![Image alt](image-url)

```code blocks```

> Blockquote

| Table | Header |
|-------|--------|
| Cell  | Cell   |
```

## Directory Structure

```
project/
├── index.md              # Site homepage
├── _images/              # Image repository
│   ├── screenshots/
│   ├── diagrams/
│   └── icons/
├── docs/                 # Documentation section
│   ├── index.md         # Docs homepage
│   ├── guide/
│   │   ├── index.md
│   │   └── getting-started.md
│   └── api/
│       ├── index.md
│       └── reference.md
└── blog/                 # Blog section
    ├── index.md
    ├── 2024-01-post.md
    └── 2024-02-post.md
```

## Common Patterns

### Blog Post
```yaml
---
title: "Blog Post Title"
post_status: publish
post_excerpt: "Brief summary for SEO"
taxonomy:
  category: [blog]
  post_tag: [topic1, topic2]
custom_fields:
  author: "Author Name"
  reading_time: "5 minutes"
---

# Blog Post Title

Your content here...
```

### Documentation Page
```yaml
---
title: "Documentation Page"
menu_order: 1
post_status: publish
taxonomy:
  doc_category: [user-guide]
custom_fields:
  version: "v2.1"
  difficulty: "beginner"
---

# Documentation Page

Your documentation content...
```

### Tutorial Series
```yaml
---
title: "Tutorial Part 1: Setup"
menu_order: 1
taxonomy:
  series: [tutorial-name]
  difficulty: [beginner]
custom_fields:
  series_part: "1"
  series_total: "5"
  next_post: "tutorial-part-2"
---

# Tutorial Part 1: Setup

Tutorial content...

## Next Steps
Continue with [Part 2](./tutorial-part-2.md)
```

## Taxonomy Reference

### Standard Taxonomies
```yaml
taxonomy:
  category:          # WordPress categories
    - web-development
    - tutorials
  post_tag:          # WordPress tags  
    - javascript
    - beginner
```

### Custom Taxonomies
```yaml
taxonomy:
  difficulty:        # Custom taxonomy
    - beginner
    - intermediate
    - advanced
  series:           # Custom taxonomy
    - wordpress-basics
    - advanced-php
```

## Custom Fields Reference

### Common Fields
```yaml
custom_fields:
  # Content metadata
  author: "John Doe"
  difficulty_level: "intermediate"
  estimated_time: "30 minutes"
  prerequisites: "Basic HTML knowledge"
  
  # SEO and social
  meta_description: "Custom meta description"
  social_image: "/_images/social/post-image.jpg"
  
  # Content organization
  version: "2.1.0"
  last_updated: "2024-01-15"
  related_posts: "post-1,post-2,post-3"
  
  # Features and flags
  featured: "true"
  premium_content: "false"
  enable_comments: "true"
  show_sidebar: "false"
```

## Link Conversion Examples

| Markdown Link | WordPress URL | Description |
|---------------|---------------|-------------|
| `./file.md` | `/current-dir/file/` | Same directory |
| `../file.md` | `/parent-dir/file/` | Parent directory |
| `../../file.md` | `/grandparent/file/` | Two levels up |
| `/docs/api.md` | `/docs/api/` | Absolute path |
| `subfolder/file.md` | `/current-dir/subfolder/file/` | Subdirectory |

## Image Path Examples

| Markdown Image | Description |
|----------------|-------------|
| `![Alt](/_images/pic.jpg)` | Root image |
| `![Alt](/_images/screenshots/app.png)` | Organized in subfolder |
| `![Alt](/_images/icons/warning.svg)` | SVG icon |

## Status Values

| Status | Description |
|--------|-------------|
| `publish` | Live and public |
| `draft` | Saved but not published |
| `pending` | Awaiting review |
| `future` | Scheduled for future |

## Validation Checklist

- [ ] Valid YAML front matter (check indentation)
- [ ] Required `title` field present
- [ ] Valid `post_status` value
- [ ] Images exist in `_images/` directory
- [ ] Internal links use `.md` extension
- [ ] No spaces in filenames
- [ ] Consistent taxonomy naming
- [ ] Custom fields properly formatted

## Troubleshooting

### Post Not Appearing
- Check YAML syntax with validator
- Verify `post_status` is not "draft"
- Ensure filename has no spaces or special characters

### Images Not Loading
- Confirm image exists in `_images/` directory
- Use `/_images/` prefix (with leading slash)
- Check file extension matches actual file

### Links Broken
- Use relative paths (`./, ../`)
- Include `.md` extension in markdown
- Test path structure matches repository

### Taxonomy Not Assigned
- Check exact spelling of taxonomy names
- Verify taxonomy exists in WordPress
- Use array format `[item1, item2]`

## Performance Tips

1. **Optimize Images**: Compress before adding to `_images/`
2. **Consistent Structure**: Use predictable directory organization
3. **Link Validation**: Regular check internal links
4. **Content Length**: Balance detail with readability
5. **Update Frequency**: Keep content current

## File Naming Best Practices

✅ **Good Examples:**
- `getting-started.md`
- `api-reference.md`
- `2024-01-15-blog-post.md`
- `user-guide.md`

❌ **Avoid:**
- `Getting Started.md` (spaces)
- `API_Reference.md` (underscores)
- `blog post!.md` (special characters)
- `GUIDE.MD` (all caps)

## Quick Commands

### Validate YAML
```bash
# Use online YAML validator for front matter
# Common tools: yamllint.com, yaml-online-parser.appspot.com
```

### Check Links
```bash
# Test relative paths in local environment
# Verify all referenced files exist
```

### Image Organization
```bash
# Recommended structure
_images/
├── screenshots/
├── diagrams/  
├── icons/
└── social/
```

This quick reference provides immediate access to the most commonly needed syntax, patterns, and troubleshooting information for Git it Write users.