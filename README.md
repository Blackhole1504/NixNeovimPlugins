# All vim plugins, ready to go

This repo auto generates nix packages for vim/neovim plugins.
Packages are automatically updated twice per week using a GitHub Actions.

Plugins are fetched from the `manifest.txt` and [awesome-neovim][0] repo.

## Available plugins

The [plugins.md](plugins.md) contains an auto-generated list of all available plugins.

## Usage

The overlay adds extra Vim plugins to `pkgs.vimExtraPlugins`.
First, add this repo to your inputs

```
inputs.vim-extra-plugins.url = github:jooooscha/nixpkgs-vim-extra-plugins
```

And use the provided overlay

```
nixpkgs.overlays = [
  inputs.vim-extra-plugins.overlays.default
];

```

You can add the packages to your vim/neovim config. For example you can use [nixvim](https://github.com/jooooscha/nixvim) or you can override the neovim package:

```
 programs.neovim = {
   plugins = [
     pkgs.vimExtraPlugins.nvim-colorizer-lua
   ];
 }
```

More info on using neovim with nix can be found here: [NixOS Neovim](https://nixos.wiki/wiki/Neovim)

[0]: https://github.com/rockerBOO/awesome-neovim
[1]: https://nixos.org/manual/nix/stable/release-notes/rl-2.4.html?highlight=builtins.getFlake#other-features
[2]: https://nur.nix-community.org/
[3]: https://nur.nix-community.org/repos/m15a/


## Contribution

### How to add a new plugin

#### 1. Add the plugin to manifest.txt:

```
# Examples

haringsrob/nvim_context_vt
sourcehut:henriquehbr/ataraxis.lua
gitlab:yorickpeterse/nvim-pqf
williamboman/mason.nvim:45b9a4da776d9fb017960b3ac7241161fb7bc578 
foo/bar::baz                   --> renamed to baz
foo/bar:dev                    --> using dev branch
```

Supported are Github (default), SourceHut, and GitLab.

#### 2. Format the Manifest and Generate the plugins (optional)

```
nix run .#update-vim-plugins -- lint
nix run .#update-vim-plugins
```

This updates `pkgs/vim-plugins.nix` and `README.md`

#### 3. Create a Pull Request

Create a pull request with all your changed files.
I am happy for any contribution. :)
