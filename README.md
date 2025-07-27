# Git it Write - Complete Documentation Suite

Welcome to the comprehensive documentation for **Git it Write**, a WordPress plugin that enables content creation using Markdown files stored in Git repositories.

## 📚 Documentation Overview

This documentation suite provides complete coverage of all public APIs, functions, components, and usage patterns for the Git it Write system.

### 📖 Available Documentation

| Document | Purpose | Audience |
|----------|---------|----------|
| **[API Documentation](./API_DOCUMENTATION.md)** | Complete API reference with examples | Developers & Content Creators |
| **[Component Reference](./COMPONENT_REFERENCE.md)** | Detailed component and function specs | Developers & Integrators |
| **[Quick Reference](./QUICK_REFERENCE.md)** | Condensed syntax and troubleshooting | All Users |

## 🚀 Getting Started

### What is Git it Write?

Git it Write is a WordPress plugin that bridges the gap between Git-based content management and WordPress publishing. It allows you to:

- Write content in Markdown format
- Store content in Git repositories  
- Automatically sync to WordPress
- Manage images and assets efficiently
- Maintain version control for all content

### Key Features

- **Markdown Support**: Write in familiar Markdown syntax
- **Git Integration**: Full version control for content
- **Automatic Publishing**: Seamless WordPress integration
- **Image Management**: Centralized asset handling
- **Flexible Configuration**: Extensive customization options
- **SEO Optimization**: Built-in SEO best practices

## 📁 Project Structure

```
your-repository/
├── README.md                 # This file
├── API_DOCUMENTATION.md      # Complete API reference
├── COMPONENT_REFERENCE.md    # Technical component details
├── QUICK_REFERENCE.md        # Quick syntax lookup
├── _images/                  # Central image repository
│   ├── screenshots/
│   ├── diagrams/
│   └── icons/
├── docs/                     # Documentation section
│   ├── index.md
│   ├── guide/
│   └── api/
├── blog/                     # Blog posts
│   ├── index.md
│   └── posts/
└── examples/                 # Usage examples
    ├── basic-post.md
    ├── advanced-tutorial.md
    └── documentation-page.md
```

## ⚡ Quick Start

### 1. Create Your First Post

Create a new `.md` file with front matter:

```yaml
---
title: "My First Post"
post_status: publish
post_excerpt: "Introduction to Git it Write"
taxonomy:
  category: [getting-started]
  post_tag: [tutorial, beginner]
---

# Welcome to Git it Write!

This is your first post created with Markdown.

## What's Next?

- Learn about [front matter configuration](./API_DOCUMENTATION.md#front-matter-configuration)
- Explore [image management](./API_DOCUMENTATION.md#image-management-api)
- Check out [advanced examples](./API_DOCUMENTATION.md#examples-and-usage)
```

### 2. Add Images

1. Place images in the `_images/` directory
2. Reference them in markdown:

```markdown
![Screenshot](/_images/screenshots/dashboard.png "Dashboard overview")
```

### 3. Link Content

Create connections between content:

```markdown
[Getting Started Guide](./getting-started.md)
[API Reference](../api/reference.md)
```

## 🎯 Common Use Cases

### Blog Management
- Create blog posts in Markdown
- Manage categories and tags
- Schedule publications
- Track content versions

### Documentation Sites
- Technical documentation
- User guides and tutorials
- API references
- Knowledge bases

### Content Workflows
- Editorial review processes
- Multi-author collaboration
- Content versioning
- Automated publishing

## 🔧 Configuration Options

### Front Matter Fields

| Field | Type | Purpose |
|-------|------|---------|
| `title` | string | Post title |
| `post_status` | string | Publication status |
| `menu_order` | integer | Display order |
| `taxonomy` | object | Categories and tags |
| `custom_fields` | object | Custom metadata |

See [API Documentation](./API_DOCUMENTATION.md#front-matter-configuration) for complete details.

### Directory Structure

- **Automatic Posts**: Each directory creates a post via `index.md`
- **Hierarchical URLs**: Directory structure maps to URL paths
- **Flexible Organization**: Organize content logically

### Image Management

- **Central Repository**: All images in `_images/` directory
- **Automatic Upload**: Images sync to WordPress media library
- **Deduplication**: Prevent duplicate uploads
- **Format Support**: JPG, PNG, GIF, SVG, WebP

## 📋 Best Practices

### Content Organization
1. Use descriptive, SEO-friendly filenames
2. Organize content in logical directory structures
3. Include `index.md` files for directory navigation
4. Maintain consistent taxonomy naming

### Performance Optimization
1. Compress images before adding to repository
2. Use relative links for internal content
3. Validate YAML front matter syntax
4. Test content in staging environments

### Collaboration Workflows
1. Use feature branches for content updates
2. Implement peer review processes
3. Maintain changelog documentation
4. Use meaningful commit messages

## 🔍 Advanced Features

### Custom Taxonomies
```yaml
taxonomy:
  difficulty: [beginner, intermediate, advanced]
  series: [wordpress-basics, advanced-development]
  content_type: [tutorial, reference, example]
```

### Scheduled Publishing
```yaml
post_date: "2024-06-15 09:00:00"
post_status: future
```

### Template Selection
```yaml
page_template: "custom-documentation.php"
```

### Content Series Management
```yaml
custom_fields:
  series_part: "3"
  series_total: "10"
  next_post: "tutorial-part-4"
  prev_post: "tutorial-part-2"
```

## 🛠️ Troubleshooting

### Common Issues

**Posts Not Appearing**
- Verify YAML front matter syntax
- Check `post_status` value
- Ensure proper file naming

**Images Not Loading**
- Confirm files exist in `_images/` directory
- Use correct path format: `/_images/filename.jpg`
- Check file extensions match

**Broken Links**
- Use relative paths with `.md` extensions
- Verify target files exist
- Test path structure

See [Quick Reference](./QUICK_REFERENCE.md#troubleshooting) for more solutions.

## 📚 Learning Resources

### For Content Creators
- Start with [Quick Reference](./QUICK_REFERENCE.md) for syntax
- Review [examples](./API_DOCUMENTATION.md#examples-and-usage) for patterns
- Learn [best practices](./API_DOCUMENTATION.md#best-practices)

### For Developers
- Explore [Component Reference](./COMPONENT_REFERENCE.md) for technical details
- Study [API Documentation](./API_DOCUMENTATION.md) for integration
- Review [utility functions](./COMPONENT_REFERENCE.md#utility-functions)

### For Site Administrators
- Understand [directory structure](./API_DOCUMENTATION.md#file-structure-api)
- Configure [taxonomies](./API_DOCUMENTATION.md#taxonomy-api)
- Set up [custom fields](./API_DOCUMENTATION.md#custom-fields-api)

## 🤝 Contributing

### Documentation Updates
1. Edit relevant documentation files
2. Follow existing formatting patterns
3. Include practical examples
4. Test all code snippets

### Content Examples
1. Create example files in `examples/` directory
2. Include comprehensive front matter
3. Demonstrate best practices
4. Link to relevant documentation

## 📄 License & Support

### Documentation License
This documentation is provided under the same license as the Git it Write plugin.

### Getting Help
- Review documentation thoroughly
- Check [troubleshooting section](./QUICK_REFERENCE.md#troubleshooting)
- Validate syntax with recommended tools
- Test in development environment first

### Version Information
- **Documentation Version**: 1.0.0
- **Last Updated**: January 2024
- **Compatible with**: Git it Write Plugin v2.x

## 🔗 Additional Resources

### External Links
- [Markdown Guide](https://www.markdownguide.org/) - Official Markdown documentation
- [YAML Syntax](https://yaml.org/spec/1.2/spec.html) - YAML specification
- [WordPress Codex](https://codex.wordpress.org/) - WordPress development resources

### Validation Tools
- [YAML Lint](http://yamllint.com/) - Validate YAML syntax
- [Markdown Preview](https://markdownlivepreview.com/) - Preview Markdown rendering
- [Link Checker](https://validator.w3.org/checklink) - Validate link structures

---

**Ready to get started?** Begin with the [Quick Reference Guide](./QUICK_REFERENCE.md) for immediate productivity, or dive into the [API Documentation](./API_DOCUMENTATION.md) for comprehensive coverage.

For technical implementation details, explore the [Component Reference](./COMPONENT_REFERENCE.md).