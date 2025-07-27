# Git it Write - Component Reference Guide

## Table of Contents

1. [File Components](#file-components)
2. [Directory Components](#directory-components)
3. [Content Processing Functions](#content-processing-functions)
4. [Configuration Components](#configuration-components)
5. [Utility Functions](#utility-functions)

## File Components

### Markdown Files (.md)

#### Primary Content Component

```markdown
# File: example-post.md
# Component Type: Content Document
# Function: Creates WordPress post content
```

**Properties:**
- **Extension**: `.md`
- **Purpose**: Primary content creation
- **Processing**: Converted to HTML and published as WordPress post
- **Slug Generation**: Filename becomes post slug

**Example Implementation:**
```markdown
---
title: "Getting Started with Git it Write"
post_status: publish
---

# Welcome to Git it Write

This is your content body written in markdown.

## Features

- Easy content management
- Git-based workflow
- Markdown support
```

**API Functions:**
- `parseMarkdown()`: Converts markdown to HTML
- `extractFrontMatter()`: Processes YAML front matter
- `generateSlug()`: Creates URL slug from filename

#### Index File Component

```markdown
# File: index.md
# Component Type: Directory Index
# Function: Represents directory as WordPress post
```

**Properties:**
- **Location**: Root of any directory
- **Purpose**: Creates post for directory itself
- **URL Structure**: Maps to directory path
- **Fallback**: Empty content if missing

**Example Implementation:**
```markdown
---
title: "Documentation Hub"
menu_order: 1
---

# Documentation Hub

Welcome to our comprehensive documentation. Choose a section below:

- [Getting Started](./getting-started.md)
- [Advanced Topics](./advanced.md)
- [API Reference](./api-reference.md)
```

### HTML Files (.html)

#### Static Page Component

```html
<!-- File: page.html -->
<!-- Component Type: Static Content -->
<!-- Function: Direct HTML content -->
```

**Properties:**
- **Extension**: `.html`
- **Purpose**: Static page content
- **Processing**: Direct inclusion without markdown conversion
- **Use Cases**: Landing pages, special layouts

**Example Implementation:**
```html
<h1>Welcome to Our Site</h1>
<p>This is a static HTML page.</p>
<div class="special-layout">
    <button onclick="doSomething()">Click me</button>
</div>
```

## Directory Components

### Documentation Directory Structure

```
docs/
├── index.md              # Main documentation hub
├── guide/                # User guide section
│   ├── index.md         # Guide overview
│   ├── getting-started.md
│   └── advanced.md
├── api/                  # API documentation
│   ├── index.md         # API overview
│   └── reference.md
└── tutorials/            # Tutorial collection
    ├── index.md         # Tutorial index
    ├── beginner/        # Nested organization
    │   ├── index.md
    │   └── first-steps.md
    └── advanced/
        ├── index.md
        └── expert-tips.md
```

### Image Directory Component

```
_images/
├── screenshots/          # Application screenshots
├── diagrams/            # Technical diagrams
├── icons/               # UI icons and symbols
├── photos/              # Photography content
└── logos/               # Brand assets
```

**Component Properties:**
- **Reserved Name**: `_images/` (underscore prefix)
- **Function**: Central image repository
- **Processing**: Automatic WordPress media upload
- **Deduplication**: Prevents duplicate uploads
- **Path Resolution**: Relative paths converted to absolute URLs

## Content Processing Functions

### Front Matter Parser

```yaml
# Function: parseFrontMatter()
# Input: Raw markdown file content
# Output: Separated metadata and content
```

**Supported Fields:**

| Field | Function | Example |
|-------|----------|---------|
| `title` | `setPostTitle()` | "My Blog Post" |
| `menu_order` | `setMenuOrder()` | 5 |
| `post_status` | `setPublishStatus()` | "publish" |
| `post_excerpt` | `setExcerpt()` | "Brief summary" |
| `taxonomy` | `assignTaxonomies()` | Categories and tags |
| `custom_fields` | `setCustomFields()` | Metadata storage |

**Example Processing:**
```javascript
// Pseudo-code for front matter processing
function parseFrontMatter(fileContent) {
    const parts = fileContent.split('---');
    const frontMatter = yaml.parse(parts[1]);
    const content = parts.slice(2).join('---');
    
    return {
        metadata: frontMatter,
        content: content,
        processed: {
            title: frontMatter.title || generateTitleFromFilename(),
            slug: generateSlugFromFilename(),
            status: frontMatter.post_status || 'draft'
        }
    };
}
```

### Link Processor

```markdown
# Function: processLinks()
# Input: Markdown content with relative links
# Output: WordPress-compatible absolute links
```

**Link Conversion Rules:**

| Input Pattern | Function | Output |
|---------------|----------|--------|
| `./file.md` | `convertRelativeLink()` | `/current-dir/file/` |
| `../dir/file.md` | `convertParentLink()` | `/parent-dir/dir/file/` |
| `/path/file.md` | `convertAbsoluteLink()` | `/path/file/` |

**Example Implementation:**
```javascript
function processLinks(content, currentPath) {
    return content.replace(/\[([^\]]+)\]\(([^)]+\.md)\)/g, (match, text, link) => {
        const processedLink = convertMarkdownLinkToWordPressURL(link, currentPath);
        return `[${text}](${processedLink})`;
    });
}

function convertMarkdownLinkToWordPressURL(link, basePath) {
    if (link.startsWith('./')) {
        return path.join(basePath, link.substring(2)).replace('.md', '/');
    }
    if (link.startsWith('../')) {
        return path.join(path.dirname(basePath), link.substring(3)).replace('.md', '/');
    }
    if (link.startsWith('/')) {
        return link.replace('.md', '/');
    }
    return link;
}
```

### Image Processor

```markdown
# Function: processImages()
# Input: Markdown content with image references
# Output: WordPress media library URLs
```

**Image Processing Pipeline:**

1. **Detection**: Find `![alt](/_images/...)` patterns
2. **Upload**: Transfer to WordPress media library
3. **URL Replacement**: Replace local paths with media URLs
4. **Caching**: Store URLs for reuse

**Example Implementation:**
```javascript
function processImages(content, imageCache) {
    return content.replace(/!\[([^\]]*)\]\(\/_images\/([^)]+)\)/g, async (match, alt, imagePath) => {
        let mediaUrl = imageCache.get(imagePath);
        
        if (!mediaUrl) {
            mediaUrl = await uploadToWordPressMedia(imagePath);
            imageCache.set(imagePath, mediaUrl);
        }
        
        return `![${alt}](${mediaUrl})`;
    });
}

async function uploadToWordPressMedia(imagePath) {
    const imageFile = fs.readFileSync(`_images/${imagePath}`);
    const response = await wp.media().file(imageFile).create({
        title: path.basename(imagePath),
        alt_text: generateAltText(imagePath)
    });
    return response.source_url;
}
```

## Configuration Components

### Taxonomy Configuration

```yaml
# Component: TaxonomyManager
# Function: Manages categories, tags, and custom taxonomies
```

**Configuration Structure:**
```yaml
taxonomy:
    category:              # Standard WordPress categories
        - web-development
        - tutorials
    post_tag:             # Standard WordPress tags
        - javascript
        - php
    custom_taxonomy:      # Custom taxonomies
        - custom-term
```

**Processing Functions:**
- `validateTaxonomy()`: Ensures taxonomy exists
- `createTerms()`: Creates missing terms
- `assignToPost()`: Associates terms with post

### Custom Fields Manager

```yaml
# Component: CustomFieldsManager
# Function: Handles post metadata
```

**Field Processing:**
```javascript
function processCustomFields(fields, postId) {
    Object.entries(fields).forEach(([key, value]) => {
        const processedValue = sanitizeFieldValue(value);
        updatePostMeta(postId, key, processedValue);
    });
}

function sanitizeFieldValue(value) {
    if (typeof value === 'object') {
        return JSON.stringify(value);
    }
    return String(value);
}
```

## Utility Functions

### File System Utilities

```javascript
// Function: scanDirectory()
// Purpose: Discover all markdown files in repository
function scanDirectory(dirPath) {
    const files = [];
    const items = fs.readdirSync(dirPath);
    
    items.forEach(item => {
        const fullPath = path.join(dirPath, item);
        const stat = fs.statSync(fullPath);
        
        if (stat.isDirectory()) {
            files.push(...scanDirectory(fullPath));
        } else if (item.endsWith('.md')) {
            files.push({
                path: fullPath,
                name: item,
                directory: dirPath,
                slug: generateSlugFromPath(fullPath)
            });
        }
    });
    
    return files;
}

// Function: generateSlugFromPath()
// Purpose: Create WordPress-compatible URL slug
function generateSlugFromPath(filePath) {
    return filePath
        .replace(/\.md$/, '')
        .replace(/[^a-z0-9]/gi, '-')
        .toLowerCase()
        .replace(/-+/g, '-')
        .replace(/^-|-$/g, '');
}
```

### Content Validation

```javascript
// Function: validateContent()
// Purpose: Ensure content meets WordPress requirements
function validateContent(file) {
    const issues = [];
    
    // Check front matter validity
    if (!file.frontMatter) {
        issues.push('Missing front matter');
    }
    
    // Validate required fields
    if (!file.frontMatter.title) {
        issues.push('Missing title field');
    }
    
    // Check content length
    if (file.content.length < 50) {
        issues.push('Content too short');
    }
    
    // Validate image references
    const imageRefs = file.content.match(/!\[.*?\]\(\/_images\/.*?\)/g) || [];
    imageRefs.forEach(ref => {
        const imagePath = ref.match(/\/_images\/(.+?)\)/)[1];
        if (!fs.existsSync(`_images/${imagePath}`)) {
            issues.push(`Missing image: ${imagePath}`);
        }
    });
    
    return {
        valid: issues.length === 0,
        issues: issues
    };
}
```

### WordPress Integration

```javascript
// Function: createWordPressPost()
// Purpose: Create or update WordPress post
async function createWordPressPost(fileData) {
    const postData = {
        title: fileData.frontMatter.title,
        content: fileData.processedContent,
        status: fileData.frontMatter.post_status || 'draft',
        slug: fileData.slug,
        excerpt: fileData.frontMatter.post_excerpt,
        menu_order: fileData.frontMatter.menu_order || 0,
        comment_status: fileData.frontMatter.comment_status || 'open'
    };
    
    // Handle date if specified
    if (fileData.frontMatter.post_date) {
        postData.date = new Date(fileData.frontMatter.post_date);
    }
    
    // Create or update post
    let post;
    const existingPost = await findPostBySlug(postData.slug);
    
    if (existingPost) {
        post = await wp.posts().id(existingPost.id).update(postData);
    } else {
        post = await wp.posts().create(postData);
    }
    
    // Handle taxonomies
    if (fileData.frontMatter.taxonomy) {
        await assignTaxonomies(post.id, fileData.frontMatter.taxonomy);
    }
    
    // Handle custom fields
    if (fileData.frontMatter.custom_fields) {
        await assignCustomFields(post.id, fileData.frontMatter.custom_fields);
    }
    
    return post;
}
```

## Error Handling Components

### Validation Pipeline

```javascript
// Component: ValidationPipeline
// Function: Comprehensive content validation
class ValidationPipeline {
    constructor() {
        this.validators = [
            new FrontMatterValidator(),
            new ContentValidator(),
            new ImageValidator(),
            new LinkValidator(),
            new TaxonomyValidator()
        ];
    }
    
    async validate(files) {
        const results = [];
        
        for (const file of files) {
            const fileResult = {
                path: file.path,
                valid: true,
                errors: [],
                warnings: []
            };
            
            for (const validator of this.validators) {
                const result = await validator.validate(file);
                if (result.errors.length > 0) {
                    fileResult.valid = false;
                    fileResult.errors.push(...result.errors);
                }
                fileResult.warnings.push(...result.warnings);
            }
            
            results.push(fileResult);
        }
        
        return results;
    }
}
```

This component reference provides detailed documentation of all the internal functions, components, and APIs that make up the Git it Write system, including examples and implementation details for each component.