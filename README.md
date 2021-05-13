## base16.lua

lua library to use [base16](https://github.com/chriskempson/base16) themes in
[Neovim](https://github.com/neovim/neovim).

## Usage

Install via your plugin manager. e.g.

```vim
use { "amirrezaask/base16.nvim" }
```

then somewhere in your init.lua

```lua
require('base16.themes')[theme_name]:apply()
```

also you can see list of available themes with

```lua
print(vim.inspect(require('base16.themes').names()))
```

## Telescope integration
You can have a simple telescope picker and cycle thorough all themes
and apply any one you want with this simple picker

```lua
function M.base16_theme_selector()
  local theme_names = require('base16.themes'):names() 
  pickers.new({}, {
    finder = finders.new_table({
      results = theme_names,
    }),
    sorter = conf.generic_sorter(),
    attach_mappings = function(_)
      actions.select_default:replace(function()
        local theme = action_state.get_selected_entry()[1]
        for k, v in pairs(require('base16.themes')) do
          if k == theme then
            v:apply()
          end
        end
      end)
      return true
    end,
  }):find()
end
```


## Credits

Chris Kempson and [Base16](https://github.com/chriskempson/base16) and [base16-vim](https://github.com/chriskempson/base16-vim)
Ashkan Kiani (norcalli)
