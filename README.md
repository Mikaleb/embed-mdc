# Obsidian Embed MDC

> Transform URLs in your Obsidian notes into rich embedded previews with MDC (Markdown Components) format support.

![demo](https://raw.githubusercontent.com/Seraphli/obsidian-link-embed/main/docs/demo.gif)

## Overview

Obsidian Embed MDC automatically converts URLs into rich preview cards with titles, images, descriptions, and metadata. Unlike basic link previews, it generates structured MDC format compatible with Nuxt Content and other static site generators.

The plugin offers multiple parsing engines, smart caching, and customizable templates - making it ideal for content creators who want professional-looking embeds without manual formatting.

## Installation

1. Open Obsidian Settings → Community Plugins
2. Search for "Embed MDC"
3. Install and enable the plugin

**Requirements:** Obsidian v0.15.0+

## Getting Started

### Method 1: Paste & Select (Easiest)

1. Paste any URL into your note
2. Choose from the popup menu:
    - **Create Embed** - Rich preview with title, image, and description
    - **Create Markdown Link** - Standard `[title](url)` format
    - **Dismiss** - Close popup

### Method 2: Command Palette

1. Select a URL, place cursor in URL text, or copy URL to clipboard
2. Open Command Palette (`Ctrl/Cmd + P`)
3. Run `Link Embed: Embed link`

> **Tip**: Use `Link Embed: Embed link with...` to choose a specific parser if the default fails.

## Configuration

### Basic Settings

-   **Auto Embed**: Automatically create embeds when pasting URLs (disabled by default)
-   **Parser Selection**: Choose primary and secondary parsers with automatic fallback
-   **In Place**: Replace selected URL instead of inserting on next line

### Advanced Options

-   **Save Images to Vault**: Download and store images locally (folder: `link-embed-images`)
-   **Respect Aspect Ratio**: Maintain original image proportions
-   **Enable Favicon**: Show website icons in embeds
-   **Use Cache**: Cache images and metadata for better performance
-   **Max Concurrent Parsers**: Limit simultaneous operations to prevent system overload
-   **Custom Metadata**: Add notes, tags, or custom data to embeds
-   **Metadata Templates**: Use variables like `{{parser}}`, `{{date}}`, `{{#formatDate}}YYYY-MM-DD{{/formatDate}}`

## Parsers

| Parser                                      | API Required | Limits     | Notes                |
| ------------------------------------------- | ------------ | ---------- | -------------------- |
| **Local** (Default)                         | ❌           | None       | Parses HTML directly |
| [JSONLink](https://jsonlink.io/)            | ✅           | Varies     | Requires API key     |
| [MicroLink](https://microlink.io/)          | ❌           | 50/day     | Free tier available  |
| [Iframely](https://iframely.com/)           | ❌           | 1000/month | Free tier available  |
| [LinkPreview](https://www.linkpreview.net/) | ✅           | Varies     | Requires API key     |

## MDC Format

Embeds are generated in MDC (Markdown Components) format:

```markdown
## ::embeded

title: "Page Title"
image: "https://example.com/preview.jpg"
description: "Page description"
url: "https://example.com"
favicon: "https://example.com/favicon.ico"
aspectRatio: "1.5"
metadata: "Custom notes or tags"
parser: "local"
date: "2023-04-01"

---

::
```

### Nuxt Content Integration

Create `components/content/Embeded.vue` to render embeds:

```vue
<template>
	<div class="embed-card">
		<img v-if="image" :src="image" :alt="title" />
		<div class="embed-content">
			<img v-if="favicon" :src="favicon" class="favicon" />
			<h3>{{ title }}</h3>
			<p>{{ description }}</p>
			<a :href="url" target="_blank">{{ url }}</a>
		</div>
	</div>
</template>

<script setup>
defineProps({
	title: String,
	image: String,
	description: String,
	url: String,
	favicon: String,
	aspectRatio: String,
	metadata: String,
	parser: String,
	date: String,
});
</script>
```

## Features

### Interface

-   **Hover Controls**: Refresh and copy buttons appear on hover
-   **Popup Menu**: Quick options when pasting URLs
-   **In-place Replacement**: Replace URLs directly or insert below

### Performance

-   **Smart Caching**: Stores images and favicons locally
-   **Concurrency Control**: Prevents system overload
-   **Lazy Loading**: Async image loading for better performance

## Contributing

We welcome contributions! Please:

1. **Bug Reports**: Use GitHub Issues with detailed reproduction steps
2. **Feature Requests**: Describe use case and expected behavior
3. **Pull Requests**: Fork → Branch → Test → PR

[Contributing Guidelines](CONTRIBUTING.md) | [Code of Conduct](CODE_OF_CONDUCT.md)

## Known Issues

-   Some sites block automated parsing (use alternative parsers)
-   Large images may slow initial load (enable caching)
-   Rate limits apply to free API parsers

## Documentation

-   [API Documentation](docs/api.md)
-   [Advanced Configuration](docs/advanced.md)
-   [Troubleshooting Guide](docs/troubleshooting.md)
-   [Parser Comparison](docs/parsers.md)

## FAQ

**Q: Why aren't embeds showing?**  
A: Check parser settings and network connectivity. Try alternative parsers.

**Q: Can I customize embed appearance?**  
A: Yes, modify the MDC component in your content framework.

**Q: How do I backup embed data?**  
A: Enable "Save Images to Vault" to store locally.

## License

[MIT License](LICENSE) - Free for personal and commercial use.

## Credits

**Created by:** [Seraphli](https://github.com/Seraphli)  
**Updated by:** [Mikaleb](https://github.com/Mikaleb)  
**Built upon:** [Obsidian Rich Link](https://github.com/dhamaniasad/obsidian-rich-links), [Obsidian Auto Link Title](https://github.com/zolrath/obsidian-auto-link-title)

**Version:** 3.0.0 | [Changelog](CHANGELOG.md) | [GitHub](https://github.com/Mikaleb/obsidian-embed-mdc)
