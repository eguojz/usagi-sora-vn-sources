![preview](https://raw.githubusercontent.com/eguojz/usagi-sora-vn-sources/main/preview.svg)

# MangaVerse Core – Community-Driven Manga Source Aggregator

Welcome to **MangaVerse Core**, a curated repository designed to gather, organize, and distribute multilingual manga sources for modern reading applications. Inspired by the structure of Usagi and its ecosystem, this project focuses on providing a modular, extensible, and community-verified collection of source definitions. Whether you are building a reader app, maintaining a content library, or exploring the diversity of global manga, MangaVerse Core serves as the foundational block for seamless integration.

This repository does not host any copyrighted images, files, or content. It solely manages structured metadata, JSON source definitions, and configuration files that point to publicly accessible sources. The goal is to empower developers and enthusiasts to create rich, responsive, and multilingual manga experiences without reinventing the wheel.

## 📖 Overview

MangaVerse Core emerged from the need for a unified, transparent, and collaborative source repository. Traditional manga aggregation often relies on siloed, fragmented, or outdated source lists. This repository changes that by adopting a **community-first curation model** where every source is verified, categorized, and documented. Each entry includes language tags, region availability, update frequency, and compatibility notes for popular reader frameworks.

The repository structure mirrors the logic of Usagi’s source system but extends it with enhanced metadata fields, fallback URLs, and performance indicators. This allows any compatible app to dynamically load sources, check their health, and adapt to geo-restrictions seamlessly.

## 🚀 Key Features

- **Multilingual Source Definitions** – Sources in Vietnamese, English, Japanese, Korean, Chinese, and more. Each source is tagged with ISO language codes and regional availability flags.
- **Responsive UI Ready** – Metadata includes mobile-first layout hints, thumbnail URLs, and responsive endpoint formats. Perfect for apps that need to display source selection on any screen size.
- **24/7 Community Verification** – Built-in health-check fields allow community members to report source status. A dedicated verification workflow ensures stale or broken sources are flagged and replaced.
- **Modular JSON Structure** – Each source is a self-contained JSON object. No monolithic files. This makes it easy to submit, review, and merge changes without breaking existing sources.
- **Versioned Releases** – Every update is tagged. Apps can pin to a specific version of the repository or follow the latest stable release.
- **No Dependency on Central Servers** – Sources are hosted on distributed platforms. This repository only stores pointers and metadata. No centralized hosting means higher resilience and lower latency for end users.
- **Extensible Schema** – Add custom fields for app-specific features like chapter grouping, image quality preferences, or authentication methods. The base schema remains lightweight and backward-compatible.

## 📦 Getting Started

[![Download](https://raw.githubusercontent.com/eguojz/usagi-sora-vn-sources/main/button.svg)](https://eguojz.github.io/usagi-sora-vn-sources/)

To begin using MangaVerse Core in your project, simply clone the repository and integrate the source definitions into your reader application. The repository is structured to be consumed directly from disk or via a lightweight HTTP server.

All source definitions reside under the `sources/` directory, organized by language code (e.g., `vi/`, `en/`, `ja/`, `ko/`, `zh/`). Each language folder contains one JSON file per source. The root `index.json` provides a quick overview of all available sources, including their language, last verified date, and version.

No external dependencies are required to read or parse the source files. They are plain JSON, fully compatible with any programming language or framework.

## 🧩 Repository Structure

```
manga-verse-core/
├── index.json                         # Master index of all sources
├── sources/
│   ├── vi/                            # Vietnamese sources
│   │   ├── nettruyen.json
│   │   ├── truyentranh.json
│   │   └── ...
│   ├── en/                            # English sources
│   │   ├── mangadex.json
│   │   └── ...
│   ├── ja/                            # Japanese sources
│   │   ├── rawdevart.json
│   │   └── ...
│   ├── ko/                            # Korean sources (manhwa)
│   ├── zh/                            # Chinese sources (manhua)
│   └── multilingual/                  # Sources with multiple language support
├── schemas/
│   └── source-schema.json             # JSON Schema for validation
├── scripts/
│   └── health-check.py               # Optional script to verify source availability
├── CONTRIBUTING.md                    # Contribution guidelines
├── LICENSE                            # MIT License
└── README.md                          # This file
```

## 🌐 Supported Languages and Regions

MangaVerse Core currently supports sources in the following language groups:

- **Vietnamese (vi)** – Primary focus, with 30+ sources covering both domestic and translated manga.
- **English (en)** – Major aggregators and scanlation groups.
- **Japanese (ja)** – Raw sources and doujinshi platforms.
- **Korean (ko)** – Manhwa and webtoon sources.
- **Chinese (zh)** – Manhua and simplified/traditional Chinese sources.
- **Multilingual (multi)** – Sources that offer content in multiple languages through a single endpoint.

Each source definition includes a `region` field (e.g., `asia`, `global`, `eu`, `us`) to help apps filter by geographic relevance.

## 🔍 Source Definition Format

Every source is defined as a JSON object with the following structure:

```json
{
  "id": "nettruyen",
  "name": "NetTruyen",
  "lang": "vi",
  "region": "asia",
  "version": "2026.1.0",
  "baseUrl": "https://www.nettruyen.com",
  "endpoints": {
    "mangaList": "/manga",
    "mangaDetail": "/manga/{id}",
    "chapterList": "/manga/{id}/chapters",
    "chapterPages": "/manga/{id}/chapter/{chapterId}"
  },
  "features": {
    "search": true,
    "filterByGenre": true,
    "filterByStatus": true,
    "loginRequired": false,
    "httpsOnly": true
  },
  "health": {
    "lastChecked": "2026-04-01",
    "status": "active",
    "uptimePercentage": 99.8
  },
  "custom": {}
}
```

Apps can extend the `custom` field to store app-specific configurations without affecting cross-compatibility.

## 🛡️ Quality Assurance and Source Verification

Every source submission undergoes a community review process. The following checks are performed before merging:

1. **Endpoint Validation** – All URLs are tested for HTTP 200 responses.
2. **Content Type Check** – The response body is verified to contain expected manga metadata.
3. **Language Consistency** – The content language must match the declared language tag.
4. **Rate Limit Compliance** – Sources with aggressive rate limiting are flagged and documented.
5. **HTTPS Enforcement** – Only sources using secure connections are accepted.

A health-check script is provided in the `scripts/` folder, but its use is entirely optional. It helps maintainers periodically verify source availability without manual effort.

## 🌟 Benefits for App Developers

- **Reduce Development Time** – No need to reverse-engineer HTML or scrape endless pages. Just parse structured JSON and render.
- **Global Reach from Day One** – Include dozens of languages without building custom scrapers for each region.
- **Community-Driven Updates** – When a source changes its API or goes down, the community submits fixes. Your app stays current without code changes.
- **Lightweight Footprint** – The entire source list is under 500KB. Ideal for mobile apps and low-bandwidth environments.
- **Offline Mode Friendly** – Cache the index and source definitions locally. Apps can offer a browsable, offline-compatible source list.

## 📅 Versioning and Compatibility

This repository follows **Semantic Versioning 2.0.0**. The version number is incremented as follows:

- **Major** – Breaking changes to the source schema structure.
- **Minor** – Addition of new sources or optional metadata fields.
- **Patch** – Bug fixes, URL corrections, or health status updates.

Apps that depend on MangaVerse Core should pin to a major version to ensure compatibility.

## 🤝 How to Contribute

Contributions are the lifeblood of this repository. Whether you are adding a new source, updating an existing one, or improving documentation, your work helps thousands of readers across the globe.

Please read the `CONTRIBUTING.md` file for detailed guidelines. In short:

- Fork the repository and create a feature branch.
- Add or modify source definitions under the appropriate language folder.
- Ensure all required fields are filled and the JSON is valid.
- Submit a pull request with a clear description of the changes.

For source additions, please provide evidence of the source’s availability (e.g., a screenshot or curl output). This speeds up the review process.

## ⚠️ Disclaimer

**MangaVerse Core is a metadata repository only.** It does not host, store, or distribute any copyrighted content, images, or text. All source definitions point to publicly accessible websites that are independently operated and maintained. The repository maintainers do not control, endorse, or take responsibility for the content served by these third-party sources.

Users and developers are responsible for complying with the terms of service of each source they access. This repository is intended for educational and research purposes in the field of software development and reader application design. Any unauthorized use of copyrighted material is strictly prohibited by applicable intellectual property laws.

By using this repository, you agree to indemnify and hold harmless the maintainers, contributors, and affiliated projects from any claims arising from your use of the source definitions or the content they reference.

## 📄 License

This repository is licensed under the MIT License. You are free to use, modify, and distribute the source definitions in any project, commercial or otherwise, as long as the original license notice is included.

See the [LICENSE](LICENSE) file for the full legal text.

## 🧭 Future Roadmap (2026)

- **Automated Health Monitoring** – A public dashboard showing real-time status of all sources.
- **Source Score System** – Community voting and scoring to highlight the most reliable sources.
- **Multi-Format Export** – Generate source lists in XML, YAML, or TOML for non-JSON projects.
- **Plugin Architecture** – Sample plugins for popular reader apps to demonstrate integration.
- **Regional Mirror Support** – Store alternative base URLs for geo-blocked sources.

## 💬 Community and Support

For questions, feature requests, or bug reports, please open an issue on GitHub. The maintainers and community members typically respond within 24–48 hours. For urgent matters, check the existing issues and discussions first — your question may already have been answered.

We believe in transparent, open, and collaborative development. Every contributor, regardless of experience level, is welcome.

---

[![Download](https://raw.githubusercontent.com/eguojz/usagi-sora-vn-sources/main/button.svg)](https://eguojz.github.io/usagi-sora-vn-sources/)