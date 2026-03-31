<!-- markdownlint-disable MD013 -->
# Leavism's zmk-config

This is my personal [ZMK firmware](https://github.com/zmkfirmware/zmk/) configuration for [Boardsource Wireless Unicorne](https://boardsource.xyz/products/corne-wireless-smt-pcb). It is primarily optimized for macOS.
The configuration currently builds against `v0.3` of upstream ZMK, extended by various ZMK modules that are mostly from [urob's zmk-config](https://github.com/urob/zmk-config). All build dependencies are pinned in this [`west`
manifest](https://github.com/leavism/wireless-corne_zmk_config/blob/master/config/west.yml).

## Highlight

- Urob's "timeless" homerow mods. They are truly wonderful defaults.
- Combos for symbols instead of a dedicated layer.
  - I prioritize horizontal combos over vertical since my keycaps aren't close enough for vertical combos to be executed consistently. I organize the symbols for easy vim motions.
- Shifted keys with a bias for vim keybindings.
  - `, ↦ ;`, `. ↦ :`
  - Urob does `? ↦ !` that replaces the `/ ↦ ?` which makes a lot of sense for most cases, but this breaks my bias for vim keybindings.
- A `num` layer with shifted keys and combos that allow for one handed arithmetic operations.
  - `- ↦ +`, `/ ↦ *`
  - Horizontal combos for parenthesis and brackets.
- Support for a nix-powered automated local build environment taken directly from urob's configs, as well as a GitHub Actions build workflow. Build locally for rapid testing of your layout or let GitHub Actions do it if you so please.

## Setup

Note to self: Your nixos-config and dotfiles installs and configures all the prerequisites already. Skip the Prerequisites section.

Just like [urob's zmk-config](https://github.com/urob/zmk-config), the local build process uses `nix`, `direnv`, and `just`. This allows us to create a virtual development environment with `west`, `zephyr-sdk`, and all other dependencies installed and loaded upon `cd`-ing into the project ZMK workspace.

### Prerequisites

1. Install the `nix` package manager.

```bash
# Install Nix with flake support enabled
curl -sSf -L https://install.lix.systems/lix | sh -s -- install --nix-build-group-id 30000

# Start the nix daemon without restarting the shell
. /nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh
```

2. Install `direnv` and `nix-direnv`.

```bash
nix profile install nixpkgs#direnv nixpkgs#nix-direnv
```

3. Setup the `direnv` shell-hook. Below example is for zsh.

```bash
# Install the shell-hook
echo 'eval "$(direnv hook bash)"' >> ~/.zshrc

# Enable nix-direnv (if installed in the previous step)
mkdir -p ~/.config/direnv
echo 'source $HOME/.nix-profile/share/nix-direnv/direnvrc' >> ~/.config/direnv/direnvrc

# Source the bashrc to activate the hook (or start a new shell)
source ~/.bashrc
```

### Setup Workspace

1. Clone the repository and cd into the project directory.
2. Set up the environment:

```bash
# Enable direnv for this directory which will set up the workspace. This may take a while.
direnv allow

# Initialize the Zephyr workspace and pull in the ZMK dependencies
just init
```
