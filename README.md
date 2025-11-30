# Z-Image Generator

Generate images using Z-Image with the latest `diffusers` from source.

## Usage

```bash
# From this directory with optional size
uv run ./gen "green car on the moon with an upside down clown" example.png 512

# Or from another location
uv run --directory <path-to-z-image-dir> gen <prompt> <output_path> <size>
```

![example output](example.png)

## How it works

1. `uv` reads `pyproject.toml`
2. Installs dependencies (including diffusers from git)
3. Caches everything for future runs
4. Runs the script

### Note: First run will be slower (cloning diffusers repo), subsequent runs are instant.

#### Why a directory instead of a single script?

We need to install `diffusers` from source until they merge the `ZImagePipeline` into the main repo.

PEP 723 (inline script metadata with `# /// script`) doesn't support git URLs in dependencies. To use `diffusers` from source, we need a `pyproject.toml` which supports:

```toml
dependencies = [
    "diffusers @ git+https://github.com/huggingface/diffusers.git",
]
```
