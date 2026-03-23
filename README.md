# nvim-mini.org

This repository contains the source code for [nvim-mini.org](https://nvim-mini.org), the official website for **MINI** (**M**odular **I**ndependent **N**eovim **I**mprovements).

## Overview

The website is built using [Quarto](https://quarto.org/) and serves as a central hub for:

- [**mini.nvim**](https://github.com/echasnovski/mini.nvim): A collection of independent Neovim modules.
- [**MiniMax**](https://github.com/echasnovski/MiniMax): Minimal and Maximally useful Neovim configurations.
- **Blog**: Announcements and updates about the MINI ecosystem.

## Structure

- `index.qmd`: The landing page.
- `mini.nvim/`: Mirrored documentation and resources from the `mini.nvim` repository.
- `MiniMax/`: Mirrored documentation and resources from the `MiniMax` repository.
- `blog/`: Quarto blog posts.
- `_scripts/`: Lua and shell scripts for syncing and processing documentation.
- `assets/`: Images and other static assets.
- `theme/`: Quarto themes and syntax definitions.

## Development

The content in `mini.nvim/` and `MiniMax/` is automatically synced from their respective repositories using scripts in `_scripts/`.

### Syncing Content

To fetch and sync the latest documentation from the upstream repositories:

```bash
# Fetch and sync both mini.nvim and MiniMax
make sync
```

Individual components can also be synced:

```bash
# Sync only mini.nvim
make mini.nvim

# Sync only MiniMax
make MiniMax
```

### Building the Website

The website is built using Quarto. To preview or render the site locally, you'll need to have [Quarto installed](https://quarto.org/docs/get-started/).

```bash
# Preview the website locally
quarto preview

# Render the website (output to docs/ directory)
quarto render
```

## Contributing

Contributions to the website are welcome! If you find any issues with the documentation or have suggestions for improvements, please open an issue or submit a pull request.

Note that documentation for `mini.nvim` and `MiniMax` should be contributed directly to their respective repositories.

## License

The content of this repository is licensed under the [MIT License](LICENSE).
