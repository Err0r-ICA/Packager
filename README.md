# Packager
Termux interactive package installer

# One line magic
alias pk="pkg list-all 2> /dev/null | grep -v -E '^Listing\.\.\.' | sed -r 's#^([^/]+)/.*\$#\\1#' | fzf --multi --preview 'pkg show {} 2> /dev/null | bat --color=always --pager=never --decorations=never --language=yaml' --preview-window='down:50%:wrap' | xargs -ro pkg install"

# What the hell is that?
This command allows you to list all packages and then use the fuzzy finder (fzf) to select and install packages. 

The alias `pk` is defined as follows:

```bash
pk="pkg list-all 2> /dev/null | grep -v -E '^Listing\.\.\.' | sed -r 's#^([^/]+)/.*\$#\\1#' | fzf --multi --preview 'pkg show {} 2> /dev/null | bat --color=always --pager=never --decorations=never --language=yaml' --preview-window='down:50%:wrap' | xargs -ro pkg install"
```

Here's a breakdown of what each command does:

1. `pkg list-all 2> /dev/null`: Lists all available packages and redirects any error output to `/dev/null`.
2. `grep -v -E '^Listing\.\.\.'`: Filters out any lines starting with "Listing...".
3. `sed -r 's#^([^/]+)/.*\$#\\1#'`: Extracts the package name from each line by removing the package version and other information.
4. `fzf --multi --preview 'pkg show {} 2> /dev/null | bat --color=always --pager=never --decorations=never --language=yaml' --preview-window='down:50%:wrap'`: Uses fzf to create an interactive fuzzy finder that previews package details using the `pkg show` command. The preview is displayed using the `bat` command with specific configurations.
5. `xargs -ro pkg install`: Takes the selected packages from fzf and passes them as arguments to the `pkg install` command for installation.

Please note that this command assumes you have the required packages (`pkg`, `fzf`, and `bat`) installed on your system and that you are using a Unix-like shell.
