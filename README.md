# Rixl OpenAPI Specification

![CI](https://github.com/rixlhq/openapi/actions/workflows/trigger.yml/badge.svg)

The canonical OpenAPI 3.x specification for the [Rixl](https://rixl.com) platform API (`api.rixl.com`).

This repository holds the `openapi.yaml` contract that serves as the single source of truth for all Rixl SDKs. When this file changes on `main`, a GitHub Actions workflow automatically dispatches a regeneration event to every supported SDK repository, keeping them in sync with the latest API surface.

## Supported SDKs

The following SDKs are auto-generated from this specification:

| SDK | Repository |
|-----|------------|
| JavaScript / TypeScript | [rixlhq/rixl-js](https://github.com/rixlhq/rixl-js) |
| Go | [rixlhq/rixl-go](https://github.com/rixlhq/rixl-go) |
| Java | [rixlhq/rixl-java](https://github.com/rixlhq/rixl-java) |
| C# | [rixlhq/rixl-csharp](https://github.com/rixlhq/rixl-csharp) |
| PHP | [rixlhq/rixl-php](https://github.com/rixlhq/rixl-php) |
| Python | [rixlhq/rixl-python](https://github.com/rixlhq/rixl-python) |
| Ruby | [rixlhq/rixl-ruby](https://github.com/rixlhq/rixl-ruby) |
| Rust | [rixlhq/rixl-rust](https://github.com/rixlhq/rixl-rust) |

## How it works

1. A change to `openapi.yaml` is pushed to the `main` branch.
2. The **SDK Trigger** workflow (`.github/workflows/trigger.yml`) detects the change.
3. For each SDK listed in the matrix, the workflow sends a `repository_dispatch` event with type `regenerate-sdk`.
4. Each SDK repository listens for that event and runs its own code-generation pipeline.

## API overview

The Rixl API (`api.rixl.com`) covers video and audio content management, including:

- **Videos** — upload initialization, upload completion, and metadata management
- **Audio tracks** — creation, listing, and deletion of audio files in various formats (MP3, Opus, FLAC, WAV, AC3, M4A, AAC)
- **Subtitles** — upload, management, and deletion of subtitle files (SRT, VTT)
- **Images** — thumbnail upload and management
- **Chapters** — chapter marker management for video content
- **Posts** — post creation and management with typed content

## Making changes

### Edit `openapi.yaml`

This is the only file that matters. Edit it following OpenAPI 3.x conventions. After merging to `main`, SDK regeneration is triggered automatically.

### Local validation

You can validate the spec locally before pushing:

```bash
# Using Spectral (recommended)
npx @stoplight/spectral-cli lint openapi.yaml

# Or simply check YAML syntax
python3 -c "import yaml; yaml.safe_load(open('openapi.yaml'))"
```

## Contributing

All changes go through the `openapi.yaml` file. Open a PR against `main`, and the SDK regeneration pipeline handles the rest.

## License

Rixl API Specification — © Rixl Inc.