# Git it Write - Comprehensive API Documentation

## Table of Contents

1. [Overview](#overview)
2. [Content API](#content-api)
3. [File Structure API](#file-structure-api)
4. [Front Matter Configuration](#front-matter-configuration)
5. [Image Management API](#image-management-api)
6. [Link Management](#link-management)
7. [Taxonomy API](#taxonomy-api)
8. [Custom Fields API](#custom-fields-api)
9. [Examples and Usage](#examples-and-usage)
10. [Best Practices](#best-practices)

## Overview

Git it Write is a WordPress plugin that enables content creation using Markdown files stored in a Git repository. This documentation covers all public APIs and configuration options available for content creators and developers.

### Supported File Formats

- **Markdown (.md)**: Primary content format
- **HTML (.html)**: Static page content
- **Images**: Stored in `_images/` directory

## Content API

### File Naming Convention

The filename serves as the post slug identifier.

```markdown
# Example
getting-started.md → /getting-started/ (slug)
user-guide.md → /user-guide/ (slug)
```

**API Rules:**
- Use lowercase characters
- Replace spaces with hyphens
- Avoid special characters
- Maintain consistency for SEO

### Directory Structure API

Each directory automatically creates a post using the `index.md` file as content.

```
docs/
├── guide/
│   ├── index.md          # Creates /guide/ post
│   ├── getting-started.md # Creates /guide/getting-started/ post
│   └── advanced.md       # Creates /guide/advanced/ post
└── api/
    ├── index.md          # Creates /api/ post
    └── reference.md      # Creates /api/reference/ post
```

## Front Matter Configuration

### Basic Configuration API

```yaml
---
title: "Your Post Title"
menu_order: 1
post_status: publish
post_excerpt: "Brief description of the content"
post_date: "2024-01-15 10:30:00"
comment_status: open
page_template: "custom-template.php"
stick_post: yes
skip_file: no
---
```

### Configuration Parameters

| Parameter | Type | Values | Description |
|-----------|------|--------|-------------|
| `title` | string | Any text | Sets the post title |
| `menu_order` | integer | 0-999 | Controls display order |
| `post_status` | string | `publish`, `draft`, `pending`, `future` | Publication status |
| `post_excerpt` | string | Any text | Post excerpt/summary |
| `post_date` | datetime | `YYYY-MM-DD HH:MM:SS` | Publication date |
| `comment_status` | string | `open`, `closed` | Comment permissions |
| `page_template` | string | Template filename | Custom page template |
| `stick_post` | string | `yes`, `no` | Sticky post setting |
| `skip_file` | string | `yes`, `no` | Skip file processing |

## Taxonomy API

### Categories and Tags

```yaml
---
taxonomy:
    category:
        - web-development
        - tutorials
        - wordpress
    post_tag:
        - markdown
        - git
        - automation
    custom_taxonomy_name:
        - custom-term-1
        - custom-term-2
---
```

### Custom Taxonomies

For custom post types, use the exact taxonomy name:

```yaml
---
taxonomy:
    product_category:
        - electronics
        - software
    skill_level:
        - beginner
        - intermediate
        - advanced
---
```

## Custom Fields API

### Basic Custom Fields

```yaml
---
custom_fields:
    author_bio: "John is a senior developer with 10 years of experience"
    difficulty_level: "intermediate"
    estimated_time: "30 minutes"
    prerequisites: "Basic HTML knowledge"
    version: "2.1.0"
---
```

### Advanced Custom Fields

```yaml
---
custom_fields:
    # Text fields
    subtitle: "Advanced WordPress Development"
    external_url: "https://example.com"
    
    # Numeric fields
    rating: 4.5
    views: 1250
    
    # Boolean-like fields
    featured: "true"
    premium_content: "false"
    
    # Array-like data (as strings)
    related_posts: "post-1,post-2,post-3"
    technologies: "PHP,JavaScript,MySQL"
---
```

## Image Management API

### Image Directory Structure

```
_images/
├── screenshots/
├── diagrams/
├── icons/
└── photos/
```

### Image Usage Syntax

```markdown
![Alt text](/_images/screenshot.jpg "Optional title")
![Diagram](/_images/diagrams/workflow.png "Workflow diagram")
![Icon](/_images/icons/warning.svg "Warning icon")
```

### Image API Features

- **Automatic Upload**: Images uploaded to WordPress media library
- **Deduplication**: Same images reused across posts
- **Relative Paths**: Use `/_images/` prefix for all images
- **Format Support**: JPG, PNG, GIF, SVG, WebP

## Link Management

### Internal Links API

```markdown
# Relative links (recommended)
[Getting Started](./getting-started.md)
[API Reference](../api/reference.md)
[Home](/)

# Absolute repository links
[Documentation](/docs/guide/introduction.md)
[Changelog](/changelog/latest.md)
```

### Link Conversion Rules

| Markdown Link | WordPress URL |
|--------------|---------------|
| `./page.md` | `/page/` |
| `../guide/intro.md` | `/guide/intro/` |
| `/docs/api.md` | `/docs/api/` |

## Examples and Usage

### Complete Blog Post Example

```yaml
---
title: "Advanced Git Workflows for WordPress Development"
menu_order: 5
post_status: publish
post_excerpt: "Learn advanced Git techniques specifically for WordPress projects"
post_date: "2024-01-15 09:00:00"
comment_status: open
taxonomy:
    category:
        - wordpress-development
        - git-tutorials
    post_tag:
        - git
        - workflows
        - collaboration
        - version-control
custom_fields:
    difficulty_level: "advanced"
    estimated_reading_time: "15 minutes"
    author_expertise: "Git specialist"
    related_course: "wordpress-git-mastery"
---

# Advanced Git Workflows for WordPress Development

## Introduction

This guide covers advanced Git workflows specifically designed for WordPress development teams.

![Git Workflow](/_images/diagrams/git-workflow.png "Advanced Git workflow diagram")

## Topics Covered

1. [Feature Branch Strategy](#feature-branch-strategy)
2. [Environment Management](#environment-management)
3. [Deployment Pipelines](#deployment-pipelines)

## Feature Branch Strategy

When working with WordPress projects, consider this branching model:

```bash
# Create feature branch
git checkout -b feature/new-plugin-functionality

# Work on your changes
git add .
git commit -m "Add new plugin functionality"

# Push and create pull request
git push origin feature/new-plugin-functionality
```

For more basic Git concepts, see our [Getting Started Guide](./getting-started.md).

## Related Resources

- [WordPress Development Best Practices](../best-practices/wordpress.md)
- [Testing Strategies](/testing/wordpress-testing.md)
```

### Documentation Page Example

```yaml
---
title: "API Reference Documentation"
menu_order: 1
post_status: publish
page_template: "documentation-template.php"
taxonomy:
    doc_category:
        - api-reference
        - developer-docs
custom_fields:
    sidebar_navigation: "true"
    search_enabled: "true"
    version: "v2.1"
    last_updated: "2024-01-15"
---

# API Reference

## Authentication

All API requests require authentication using your API key:

```php
$api_key = 'your-api-key-here';
$headers = [
    'Authorization' => 'Bearer ' . $api_key,
    'Content-Type' => 'application/json'
];
```

## Endpoints

### GET /api/posts

Retrieve all posts with optional filtering.

**Parameters:**
- `status` (string): Filter by post status
- `category` (string): Filter by category slug
- `limit` (integer): Number of results (default: 10)

**Example:**
```bash
curl -H "Authorization: Bearer your-api-key" \
     "https://yoursite.com/api/posts?status=publish&limit=20"
```
```

### Tutorial Series Example

```yaml
---
title: "WordPress Plugin Development - Part 1: Setup"
menu_order: 1
post_status: publish
taxonomy:
    series:
        - wordpress-plugin-development
    difficulty:
        - beginner
custom_fields:
    series_part: "1"
    series_total: "10"
    next_post: "wordpress-plugin-development-part-2"
    github_repo: "https://github.com/example/wp-plugin-tutorial"
---

# WordPress Plugin Development Series - Part 1: Setup

Welcome to our comprehensive WordPress plugin development series!

## What You'll Learn

By the end of this 10-part series, you'll be able to:

- Create custom WordPress plugins from scratch
- Implement proper security measures
- Follow WordPress coding standards
- Deploy and maintain your plugins

## Prerequisites

Before starting, ensure you have:

- Basic PHP knowledge
- Local WordPress development environment
- Code editor (VS Code, PhpStorm, etc.)

## Next Steps

Continue with [Part 2: Plugin Structure](./wordpress-plugin-development-part-2.md)

## Series Navigation

- **Part 1: Setup** (Current)
- [Part 2: Plugin Structure](./wordpress-plugin-development-part-2.md)
- [Part 3: Hooks and Filters](./wordpress-plugin-development-part-3.md)
```

## Best Practices

### Content Organization

1. **Hierarchical Structure**: Use directories to group related content
2. **Consistent Naming**: Follow kebab-case for filenames
3. **Index Files**: Always include `index.md` in directories
4. **Cross-References**: Link related content appropriately

### Front Matter Standards

1. **Required Fields**: Always include `title` and `post_status`
2. **SEO Fields**: Use `post_excerpt` for meta descriptions
3. **Taxonomy Consistency**: Maintain consistent category/tag naming
4. **Custom Fields**: Document your custom field schema

### Performance Optimization

1. **Image Optimization**: Compress images before adding to `_images/`
2. **Link Validation**: Regularly check internal links
3. **Content Length**: Balance comprehensive content with readability
4. **Update Frequency**: Keep documentation current with version changes

### Version Control

1. **Commit Messages**: Use clear, descriptive commit messages
2. **Branch Strategy**: Use feature branches for major content updates
3. **Review Process**: Implement peer review for documentation changes
4. **Change Tracking**: Maintain changelogs for major updates

## Error Handling

### Common Issues and Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| Post not appearing | Invalid front matter YAML | Validate YAML syntax |
| Images not loading | Incorrect path | Use `/_images/` prefix |
| Links broken | Incorrect relative paths | Check path structure |
| Taxonomy not assigned | Typo in taxonomy name | Verify exact taxonomy names |

### Debugging Tips

1. **YAML Validation**: Use online YAML validators for front matter
2. **Path Testing**: Test relative links in local environment
3. **Image Verification**: Ensure images exist in `_images/` directory
4. **Preview Mode**: Use draft status to test before publishing

## Migration and Updates

### Content Migration

When migrating existing content:

1. Convert HTML to Markdown format
2. Update image paths to use `_images/` directory
3. Add appropriate front matter
4. Test all internal links
5. Verify taxonomy assignments

### Version Updates

When updating the Git it Write plugin:

1. Review changelog for breaking changes
2. Test front matter compatibility
3. Update documentation examples
4. Verify image handling still works
5. Check link conversion functionality