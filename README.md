# Automations

## srchx

Search disparate text content more powerfully.

- Search by tags which classify similar search terms and document types.
- Supplement pre-defined tags with direct search terms.
- Configure min and max result counts.
- Leverages *grep*.

### Usage

1. Place `.srchx.conf` either in the current or your home directory, or ~/.config/srchx.conf directory. See the provided example conf for the layout. The below examples appeal to this config.
1. Place `srchx` somewhere in your path.

Run `srchx` with no arguments to display the command line parameters.

Search through all text content defined by the tags 'notes' and 'blog' for all terms defined by 'dev'. See the example config.

```
srchx dev notes blog
```

Pass the tags and free search terms in any order, provided their uniqueness in the config. Any terms not explicitly defined are taken to be free search terms.

Search all your *notes* and *blog* for the terms defined by tags *dev* and *success*, in addition to the free term 'FET transistor'.

```
srchx notes dev blog 'FET transistor' success
```

Supply the parameter '-c' to limit the results to counts next to each matched file, respecting the configuration parameters 'min-count' and 'max-count'.

## alias-gen

Define complex shell aliases via templates. Rather than explain, see the provided example in the repository.

### Usage

1. Place `alias-gen` somewhere in your path.
1. Invoke `alias-gen <config>` to generate the respective aliases and write to `~/.shortcuts` (configurable).
1. Source `~/.shortcuts` in whatever shell initialization file applicable to you. Example for `~/.bashrc`:

    ```
    [ -f ~/.shortcuts ] && . ~/.shortcuts
    ```
1. Bonus: If a VIM user, automatically regenerate the aliases upon the config modification. Provided '.aliases' (placed in any directory) represents the config, place the following in your '~/.vimrc':

    ```vim
    autocmd BufWritePost */.aliases !alias-gen %
    ```

### More info

- Set the 'OUTPUT' config variable to whatever file you wish to generate your shell aliases.
- Each template in the *cmd_templates* section of the config must correspond to an existing section of aliases below. See the example.
- The template format accepts only one '%s' parameter to be replaced with the alias def. If the def must appear more than once in the definition, leverage a shell variable in your command, providing the proper escapes, per the example:

```
tmux_sessions = arg=%s && tmux select-window -t \"\$arg\" >/dev/null 2>&1 ||
    tmux new-window -n \"\$arg\" \; send-keys \"\$arg\" C-m 
    \"vim '+:call LoadSession()'\" C-m
```
