# Vim / Neovim

## Integracja Neovim ze schowkiem systemowym

- https://neovim.io/doc/user/provider.html#clipboard
- plugin fauxClip

Dodanie pluginu do konfiguracji (packer.nvim)

```
use({ "Jorengarenar/fauxClip", disable = false })
```

Konfiguracja

```
-- fauxClip
g.SESSION_TYPE = vim.fn.getenv("XDG_SESSION_TYPE")

if SESSION_TYPE == "wayland" then
  g.fauxClip_copy_cmd = "wl-copy"
  g.fauxClip_paste_cmd = "wl-paste"

  g.fauxClip_always_use = 1
else
  -- kopiowanie
  g.fauxClip_copy_cmd = "xclip -f -i -selection clipboard"
  g.fauxClip_copy_primary_cmd = "xclip -f -i"
  g.fauxClip_copy_primary_cmd = "xclip -f -i"
  -- wklejanie
  g.fauxClip_paste_cmd = "xclip -o -selection clipboard"
  g.fauxClip_paste_primary_cmd = "xclip -o"

  g.fauxClip_always_use = 1
end
```
