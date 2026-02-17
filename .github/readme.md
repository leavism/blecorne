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
