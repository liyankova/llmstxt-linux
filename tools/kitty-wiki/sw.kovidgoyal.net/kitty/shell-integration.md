---
source_url: "https://sw.kovidgoyal.net/kitty/shell-integration/"
title: "Shell integration - kitty"
crawl_date: "2025-11-16T14:49:27.804365Z"
selector: "article"
---

# Shell integration - kitty

# Shell integration[¶](#shell-integration "Link to this heading")

kitty has the ability to integrate closely within common shells, such as [zsh](https://www.zsh.org/), [fish](https://fishshell.com) and [bash](https://www.gnu.org/software/bash/) to enable features such as jumping to
previous prompts in the scrollback, viewing the output of the last command in
**less**, using the mouse to move the cursor while editing prompts, etc.

Added in version 0.24.0.

# Features[¶](#features "Link to this heading")

* Open the output of the last command in a pager such as **less**
  ([`ctrl+shift+g`](../conf/#shortcut-kitty.Browse-output-of-the-last-shell-command-in-pager))
* Jump to the previous/next prompt in the scrollback
  ([`ctrl+shift+z`](../conf/#shortcut-kitty.Scroll-to-previous-shell-prompt) / [`ctrl+shift+x`](../conf/#shortcut-kitty.Scroll-to-next-shell-prompt))
* Click with the mouse anywhere in the current command to move the cursor there
* Hold `Ctrl`+`Shift` and right-click on any command output in the scrollback
  to view it in a pager
* The current working directory or the command being executed are automatically
  displayed in the kitty window titlebar/tab title
* The text cursor is changed to a bar when editing commands at the shell prompt
* [Clone the current shell into a new window](#clone-shell) with all environment variables and the working directory
  copied
* [Edit files in new kitty windows](#edit-file) even over SSH
* Glitch free window resizing even with complex prompts. Achieved by erasing
  the prompt on resize and allowing the shell to redraw it cleanly.
* Sophisticated completion for the **kitty** command in the shell.
* When confirming a quit command if a window is sitting at a shell prompt,
  it is not counted (for details, see [`confirm_os_window_close`](../conf/#opt-kitty.confirm_os_window_close))

# Configuration[¶](#configuration "Link to this heading")

Shell integration is controlled by the [`shell_integration`](../conf/#opt-kitty.shell_integration) option. By
default, all integration features are enabled. Individual features can be turned
off or it can be disabled entirely as well. The [`shell_integration`](../conf/#opt-kitty.shell_integration) option
takes a space separated list of keywords:

disabled
:   Turn off all shell integration. The shell’s launch environment is not
    modified and [`KITTY_SHELL_INTEGRATION`](../glossary/#envvar-KITTY_SHELL_INTEGRATION) is not set. Useful for
    [manual integration](#manual-shell-integration).

no-rc
:   Do not modify the shell’s launch environment to enable integration. Useful
    if you prefer to load the kitty shell integration code yourself, either as
    part of [manual integration](#manual-shell-integration) or because
    you have some other software that sets up shell integration.
    This will still set the [`KITTY_SHELL_INTEGRATION`](../glossary/#envvar-KITTY_SHELL_INTEGRATION) environment
    variable when kitty runs the shell.

no-cursor
:   Turn off changing of the text cursor to a bar when editing shell command
    line.

no-title
:   Turn off setting the kitty window/tab title based on shell state.
    Note that for the fish shell kitty relies on fish’s native title setting
    functionality instead.

no-cwd
:   Turn off reporting the current working directory. This is used to allow
    [`new_window_with_cwd`](../actions/#action-new_window_with_cwd) and similar to open windows logged into remote
    machines using the [ssh kitten](../kittens/ssh/) automatically with the
    same working directory as the current window.
    Note that for the fish shell this will not disable its built-in current
    working directory reporting.

no-prompt-mark
:   Turn off marking of prompts. This disables jumping to prompt, browsing
    output of last command and click to move cursor functionality.
    Note that for the fish shell this does not take effect, since fish always
    marks prompts.

no-complete
:   Turn off completion for the kitty command.
    Note that for the fish shell this does not take effect, since fish already
    comes with a kitty completion script.

no-sudo
:   Do not alias **sudo** to ensure the kitty terminfo files are
    available in the sudo environment. This is needed if you have sudo
    configured to disable setting of environment variables on the command line.
    By default, if sudo is configured to allow all commands for the current
    user, setting of environment variables at the command line is also allowed.
    Only if commands are restricted is this needed.

## More ways to browse command output[¶](#more-ways-to-browse-command-output "Link to this heading")

You can add further key and mouse bindings to browse the output of commands
easily. For example to select the output of a command by right clicking the
mouse on the output, define the following in `kitty.conf`:

```
mouse_map right press ungrabbed mouse_select_command_output
```

Now, when you right click on the output, the entire output is selected, ready
to be copied.

The feature to jump to previous prompts (
[`ctrl+shift+z`](../conf/#shortcut-kitty.Scroll-to-previous-shell-prompt) and [`ctrl+shift+x`](../conf/#shortcut-kitty.Scroll-to-next-shell-prompt)) and mouse
actions ([`mouse_select_command_output`](../actions/#action-mouse_select_command_output) and [`mouse_show_command_output`](../actions/#action-mouse_show_command_output))
can be integrated with browsing command output as well. For example, define the
following mapping in `kitty.conf`:

```
map f1 show_last_visited_command_output
```

Now, pressing `F1` will cause the output of the last jumped to command or
the last mouse clicked command output to be opened in a pager for easy browsing.

In addition, You can define shortcut to get the first command output on screen.
For example, define the following in `kitty.conf`:

```
map f1 show_first_command_output_on_screen
```

Now, pressing `F1` will cause the output of the first command output on
screen to be opened in a pager.

You can also add shortcut to scroll to the last jumped position. For example,
define the following in `kitty.conf`:

```
map f1 scroll_to_prompt 0
```

# How it works[¶](#how-it-works "Link to this heading")

At startup, kitty detects if the shell you have configured (either system wide
or the [`shell`](../conf/#opt-kitty.shell) option in `kitty.conf`) is a supported shell. If so,
kitty injects some shell specific code into the shell, to enable shell
integration. How it does so varies for different shells.

zsh

For zsh, kitty sets the [`ZDOTDIR`](../glossary/#envvar-ZDOTDIR) environment variable to make zsh
load kitty’s `.zshenv` which restores the original value of
[`ZDOTDIR`](../glossary/#envvar-ZDOTDIR) and sources the original `.zshenv`. It then loads
the shell integration code. The remainder of zsh’s startup process proceeds
as normal.

fish

For fish, to make it automatically load the integration code provided by
kitty, the integration script directory path is prepended to the
[`XDG_DATA_DIRS`](../glossary/#envvar-XDG_DATA_DIRS) environment variable. This is only applied to the
fish process and will be cleaned up by the integration script after startup.
No files are added or modified.

bash

For bash, kitty starts bash in POSIX mode, using the environment variable
[`ENV`](../glossary/#envvar-ENV) to load the shell integration script. This prevents bash from
loading any startup files itself. The loading of the startup files is done
by the integration script, after disabling POSIX mode. From the perspective
of those scripts there should be no difference to running vanilla bash.

Then, when launching the shell, kitty sets the environment variable
[`KITTY_SHELL_INTEGRATION`](../glossary/#envvar-KITTY_SHELL_INTEGRATION) to the value of the [`shell_integration`](../conf/#opt-kitty.shell_integration)
option. The shell integration code reads the environment variable, turns on the
specified integration functionality and then unsets the variable so as to not
pollute the system.

The actual shell integration code uses hooks provided by each shell to send
special escape codes to kitty, to perform the various tasks. You can see the
code used for each shell below:

Click to toggle shell integration code

zsh

```
#!/bin/zsh
#
# Enables integration between zsh and kitty based on KITTY_SHELL_INTEGRATION.
# The latter is set by kitty based on kitty.conf.
#
# This is an autoloadable function. It's invoked automatically in shells
# directly spawned by kitty but not in any other shells. For example, running
# `exec zsh`, `sudo -E zsh`, `tmux`, or plain `zsh` will create a shell where
# kitty-integration won't automatically run. Zsh users who want integration with
# kitty in all shells should add the following lines to their .zshrc:
#
#   if [[ -n "$KITTY_INSTALLATION_DIR" ]]; then
#     export KITTY_SHELL_INTEGRATION="enabled"
#     autoload -Uz -- "$KITTY_INSTALLATION_DIR"/shell-integration/zsh/kitty-integration
#     kitty-integration
#     unfunction kitty-integration
#   fi
#
# Implementation note: We can assume that alias expansion is disabled in this
# file, so no need to quote defensively. We still have to defensively prefix all
# builtins with `builtin` to avoid accidentally invoking user-defined functions.
# We avoid `function` reserved word as an additional defensive measure.

builtin emulate -L zsh -o no_warn_create_global -o no_aliases

[[ -o interactive ]]                || builtin return 0  # non-interactive shell
[[ -n "$KITTY_SHELL_INTEGRATION" ]] || builtin return 0  # integration disabled
(( ! $+_ksi_state ))                || builtin return 0  # already initialized

# 0: no OSC 133 [AC] marks have been written yet.
# 1: the last written OSC 133 C has not been closed with D yet.
# 2: none of the above.
builtin typeset -gi _ksi_state

# Attempt to create a writable file descriptor to the TTY so that we can print
# to the TTY later even when STDOUT is redirected. This code is fairly subtle.
#
# - It's tempting to do `[[ -t 1 ]] && exec {_ksi_state}>&1` but we cannot do this
#   because it'll create a file descriptor >= 10 without O_CLOEXEC. This file
#   descriptor will leak to child processes.
# - If we do `exec {3}>&1`, the file descriptor won't leak to the child processes
#   but it'll still leak if the current process is replaced with another. In
#   addition, it'll break user code that relies on fd 3 being available.
# - Zsh doesn't expose dup3, which would have allowed us to copy STDOUT with
#   O_CLOEXEC. The only way to create a file descriptor with O_CLOEXEC is via
#   sysopen.
# - `zmodload zsh/system` and `sysopen -o cloexec -wu _ksi_fd -- /dev/tty` can
#   fail with an error message to STDERR (the latter can happen even if /dev/tty
#   is writable), hence the redirection of STDERR. We do it for the whole block
#   for performance reasons (redirections are slow).
# - We must open the file descriptor right here rather than in _ksi_deferred_init
#   because there are broken zsh plugins out there that run `exec {fd}< <(cmd)`
#   and then close the file descriptor more than once while suppressing errors.
#   This could end up closing our file descriptor if we opened it in
#   _ksi_deferred_init.
typeset -gi _ksi_fd
{
    builtin zmodload zsh/system && (( $+builtins[sysopen] )) && {
        { [[ -w     $TTY ]] && builtin sysopen -o cloexec -wu _ksi_fd --     $TTY } ||
        { [[ -w /dev/tty ]] && builtin sysopen -o cloexec -wu _ksi_fd -- /dev/tty }
    }
} 2>/dev/null || (( _ksi_fd = 1 ))

# Asks kitty to print $@ to its STDERR. This is for debugging.
_ksi_debug_print() {
    builtin local data
    data=$(builtin command base64 <<<"${(j: :)@}") || builtin return
    # Removing all spaces rather than just \n allows this code to
    # work on broken systems where base64 outputs \r\n.
    builtin print -nu "$_ksi_fd" '\eP@kitty-print|'"${data//[[:space:]]}"'\e\\'
}

# We defer initialization until precmd for several reasons:
#
# - Oh My Zsh and many other configs remove zle-line-init and
#   zle-line-finish hooks when they initialize.
# - By deferring initialization we allow user rc files to opt out from some
#   parts of integration. For example, if a zshrc theme prints OSC 133
#   marks, it can append " no-prompt-mark" to KITTY_SHELL_INTEGRATION during
#   initialization to avoid redundant marks from our code.
builtin typeset -ag precmd_functions
precmd_functions+=(_ksi_deferred_init)

_ksi_deferred_init() {
    builtin emulate -L zsh -o no_warn_create_global -o no_aliases

    # Recognized options: no-cursor, no-title, no-prompt-mark, no-complete, no-cwd, no-sudo.
    builtin local -a opt
    opt=(${(s: :)KITTY_SHELL_INTEGRATION})
    builtin unset KITTY_SHELL_INTEGRATION
    builtin local krcs="$KITTY_SI_RUN_COMMAND_AT_STARTUP"
    builtin unset KITTY_SI_RUN_COMMAND_AT_STARTUP

    if [[ -n "$SSH_KITTEN_KITTY_DIR" ]]; then
        if [[ ! "$PATH" =~ (^|:)${SSH_KITTEN_KITTY_DIR}(:|$) ]] && [[ -z "$(builtin command -v kitten)" ]]; then
            builtin export PATH="${PATH}:${SSH_KITTEN_KITTY_DIR}"
        fi
        builtin unset SSH_KITTEN_KITTY_DIR
    fi

    # The directory where kitty-integration is located: /.../shell-integration/zsh.
    builtin local self_dir="${functions_source[_ksi_deferred_init]:A:h}"
    # The directory with _kitty. We store it in a directory of its own rather than
    # in $self_dir because we are adding it to fpath and we don't want any other
    # files to be accidentally autoloadable.
    builtin local comp_dir="$self_dir/completions"

    # Enable completions for `kitty` command.
    if (( ! opt[(Ie)no-complete] )) && [[ -r $comp_dir/_kitty ]]; then
        if (( $+functions[compdef] )); then
            # If compdef is defined, then either compinit has already run or it's
            # a shim that records all calls for the purpose of replaying them after
            # compinit. Either way we clobber the existing completion for kitty and
            # install our own.
            builtin unset "functions[_kitty]"
            builtin autoload -Uz -- $comp_dir/_kitty
            compdef _kitty kitty
            compdef _kitty clone-in-kitty
            compdef _kitty kitten
        fi

        # If compdef is not set, compinit has not run yet. In this case we must
        # add our completions directory to fpath so that _kitty gets picked up by
        # compinit.
        #
        # We extend fpath even if compinit has run because it might run again.
        # Without our completions directory in fpath compinit would our _comp
        # mapping.
        builtin typeset -ga fpath
        fpath=($comp_dir ${fpath:#$comp_dir})
    fi

    # Enable semantic markup with OSC 133.
    if (( ! opt[(Ie)no-prompt-mark] )); then
        _ksi_precmd() {
            builtin local -i cmd_status=$?
            builtin emulate -L zsh -o no_warn_create_global -o no_aliases

            # Don't write OSC 133 D when our precmd handler is invoked from zle.
            # Some plugins do that to update prompt on cd.
            if ! builtin zle; then
                # This code works incorrectly in the presence of a precmd or chpwd
                # hook that prints. For example, sindresorhus/pure prints an empty
                # line on precmd and marlonrichert/zsh-snap prints $PWD on chpwd.
                # We'll end up writing our OSC 133 D mark too late.
                #
                # Another failure mode is when the output of a command doesn't end
                # with LF and prompst_sp is set (it is by default). In this case
                # we'll incorrectly state that '%' from prompt_sp is a part of the
                # command's output.
                if (( _ksi_state == 1 )); then
                    # The last written OSC 133 C has not been closed with D yet.
                    # Close it and supply status.
                    builtin print -nu $_ksi_fd '\e]133;D;'$cmd_status'\a'
                    (( _ksi_state = 2 ))
                elif (( _ksi_state == 2 )); then
                    # There might be an unclosed OSC 133 C. Close that.
                    builtin print -nu $_ksi_fd '\e]133;D\a'
                fi
            fi

            builtin local mark1=$'%{\e]133;A\a%}'
            if [[ -o prompt_percent ]]; then
                builtin typeset -g precmd_functions
                if [[ ${precmd_functions[-1]} == _ksi_precmd ]]; then
                    # This is the best case for us: we can add our marks to PS1 and
                    # PS2. This way our marks will be printed whenever zsh
                    # redisplays prompt: on reset-prompt, on SIGWINCH, and on
                    # SIGCHLD if notify is set. Themes that update prompt
                    # asynchronously from a `zle -F` handler might still remove our
                    # marks. Oh well.
                    builtin local mark2=$'%{\e]133;A;k=s\a%}'
                    # Add marks conditionally to avoid a situation where we have
                    # several marks in place. These conditions can have false
                    # positives and false negatives though.
                    #
                    # - False positive (with prompt_percent): PS1="%(?.$mark1.)"
                    # - False negative (with prompt_subst):   PS1='$mark1'
                    [[ $PS1 == *$mark1* ]] || PS1=${mark1}${PS1}
                    # PS2 mark is needed when clearing the prompt on resize
                    [[ $PS2 == *$mark2* ]] || PS2=${mark2}${PS2}
                    (( _ksi_state = 2 ))
                else
                    # If our precmd hook is not the last, we cannot rely on prompt
                    # changes to stick, so we don't even try. At least we can move
                    # our hook to the end to have better luck next time. If there is
                    # another piece of code that wants to take this privileged
                    # position, this won't work well. We'll break them as much as
                    # they are breaking us.
                    precmd_functions=(${precmd_functions:#_ksi_precmd} _ksi_precmd)
                    # Plugins that invoke precmd hooks from zle do that before zle
                    # is trashed. This means that the cursor is in the middle of
                    # BUFFER and we cannot print our mark there. Prompt might
                    # already have a mark, so the following reset-prompt will write
                    # it. If it doesn't, there is nothing we can do.
                    if ! builtin zle; then
                        builtin print -rnu $_ksi_fd -- $mark1[3,-3]
                        (( _ksi_state = 2 ))
                    fi
                fi
            elif ! builtin zle; then
                # Without prompt_percent we cannot patch prompt. Just print the
                # mark, except when we are invoked from zle. In the latter case we
                # cannot do anything.
                builtin print -rnu $_ksi_fd -- $mark1[3,-3]
                (( _ksi_state = 2 ))
            fi
        }

        _ksi_preexec() {
            builtin emulate -L zsh -o no_warn_create_global -o no_aliases

            # This can potentially break user prompt. Oh well. The robustness of
            # this code can be improved in the case prompt_subst is set because
            # it'll allow us distinguish (not perfectly but close enough) between
            # our own prompt, user prompt, and our own prompt with user additions on
            # top. We cannot force prompt_subst on the user though, so we would
            # still need this code for the no_prompt_subst case.
            PS1=${PS1//$'%{\e]133;A\a%}'}
            PS2=${PS2//$'%{\e]133;A;k=s\a%}'}

            # This will work incorrectly in the presence of a preexec hook that
            # prints. For example, if MichaelAquilina/zsh-you-should-use installs
            # its preexec hook before us, we'll incorrectly mark its output as
            # belonging to the command (as if the user typed it into zle) rather
            # than command output.
            builtin print -nu "$_ksi_fd" -f '\e]133;C;cmdline=%q\a' -- "$1"
            (( _ksi_state = 1 ))
        }

        # the following two lines are commented out as currently kitty doesn't use B prompt marking
        # and hooking zle widgets in ZSH is a total minefield, see https://github.com/kovidgoyal/kitty/issues/4428
        # so we can at least tell users to use no-cursor and with that avoid hooking ZLE widgets at all
        # functions[_ksi_zle_line_init]+='
        #     builtin print -nu "$_ksi_fd" "\\e]133;B\\a"'
    fi

    # Enable reporting current working dir to terminal
    if (( ! opt[(Ie)no-cwd] )); then
        _ksi_report_pwd() { builtin print -nu $_ksi_fd '\e]7;kitty-shell-cwd://'"$HOST""$PWD"'\a'; }
        chpwd_functions=(${chpwd_functions[@]} "_ksi_report_pwd")
        # An executed program could change cwd and report the changed cwd, so also report cwd at each new prompt
        # as in this case chpwd_functions is insufficient. chpwd_functions is still needed for things like: cd x && something
        functions[_ksi_precmd]+="
            _ksi_report_pwd"
        _ksi_report_pwd
    fi

    # Enable terminal title changes.
    if (( ! opt[(Ie)no-title] )); then
        # We don't use `print -P` because it depends on prompt options, which
        # we don't control and cannot change.
        #
        # We use (V) in preexec to convert control characters to something visible
        # (LF becomes \n, etc.). This isn't necessary in precmd because (%) does it
        # for us.
        builtin local is_ssh_session="n"
        if [[ -n "$KITTY_PID" ]]; then
            # kitty running locally
        elif [[ -n "$SSH_TTY" || -n "$SSH2_TTY$KITTY_WINDOW_ID" ]]; then
            # connected to most SSH servers
            # or use ssh kitten to connected to some SSH servers that do not set SSH_TTY
            is_ssh_session="y"
        elif [[ -n "$(builtin command -v who)" ]]; then
            # the shell integration script is installed manually on the remote system
            # the environment variables are cleared after sudo
            # OpenSSH's sshd creates entries in utmp for every login so use those
            [[ "$(builtin command who -m 2> /dev/null)" =~ "\([a-fA-F.:0-9]+\)$" ]] && is_ssh_session="y"
        fi

        if [[ "$is_ssh_session" == "y" ]]; then
            functions[_ksi_precmd]+="
                builtin print -rnu $_ksi_fd \$'\\e]2;'\"\${(V)\${HOST-}/%.*/}: \${(%):-%(4~|…/%3~|%~)}\"\$'\\a'"
            functions[_ksi_preexec]+="
                builtin print -rnu $_ksi_fd \$'\\e]2;'\"\${(V)\${HOST-}/%.*/}: \${(V)1}\"\$'\\a'"
        else
            functions[_ksi_precmd]+="
                builtin print -rnu $_ksi_fd \$'\\e]2;'\"\${(%):-%(4~|…/%3~|%~)}\"\$'\\a'"
            functions[_ksi_preexec]+="
                builtin print -rnu $_ksi_fd \$'\\e]2;'\"\${(V)1}\"\$'\\a'"
        fi
    fi

    # Enable cursor shape changes depending on the current keymap.
    if (( ! opt[(Ie)no-cursor] )); then
        # This implementation leaks blinking block cursor into external commands
        # executed from zle. For example, users of fzf-based widgets may find
        # themselves with a blinking block cursor within fzf.
        _ksi_zle_line_init _ksi_zle_line_finish _ksi_zle_keymap_select() {
            case ${KEYMAP-} in
                # Blinking block cursor.
                vicmd|visual) builtin print -nu "$_ksi_fd" '\e[1 q';;
                # Blinking bar cursor.
                *)            builtin print -nu "$_ksi_fd" '\e[5 q';;
            esac
        }
        # Restore the blinking default shape before executing an external command
        functions[_ksi_preexec]+="
            builtin print -rnu $_ksi_fd \$'\\e[0 q'"
    fi

    # Some zsh users manually run `source ~/.zshrc` in order to apply rc file
    # changes to the current shell. This is a terrible practice that breaks many
    # things, including our shell integration. For example, Oh My Zsh and Prezto
    # (both very popular among zsh users) will remove zle-line-init and
    # zle-line-finish hooks if .zshrc is manually sourced. Prezto will also remove
    # zle-keymap-select.
    #
    # Another common (and much more robust) way to apply rc file changes to the
    # current shell is `exec zsh`. This will remove our integration from the shell
    # unless it's explicitly invoked from .zshrc. This is not an issue with
    # `exec zsh` but rather with our implementation of automatic shell integration.

    # In the ideal world we would use add-zle-hook-widget to hook zle-line-init
    # and similar widget. This breaks user configs though, so we have do this
    # horrible thing instead.
    builtin local hook func widget orig_widget flag
    for hook in line-init line-finish keymap-select; do
        func=_ksi_zle_${hook/-/_}
        (( $+functions[$func] )) || builtin continue
        widget=zle-$hook
        if [[ $widgets[$widget] == user:azhw:* &&
              $+functions[add-zle-hook-widget] -eq 1 ]]; then
            # If the widget is already hooked by add-zle-hook-widget at the top
            # level, add our hook at the end. We MUST do it this way. We cannot
            # just wrap the widget ourselves in this case because it would
            # trigger bugs in add-zle-hook-widget.
            add-zle-hook-widget $hook $func
        else
            if (( $+widgets[$widget] )); then
                # There is a widget but it's not from add-zle-hook-widget. We
                # can rename the original widget, install our own and invoke
                # the original when we are called.
                #
                # Note: The leading dot is to work around bugs in
                # zsh-syntax-highlighting.
                orig_widget=._ksi_orig_$widget
                builtin zle -A $widget $orig_widget
                if [[ $widgets[$widget] == user:* ]]; then
                    # No -w here to preserve $WIDGET within the original widget.
                    flag=
                else
                    flag=w
                fi
                functions[$func]+="
                    builtin zle $orig_widget -N$flag -- \"\$@\""
            fi
            builtin zle -N $widget $func
        fi
    done

    # run startup command
    if [[ -n "$krcs" ]]; then
        builtin print -nu "$_ksi_fd" -f '\e]2;%s\e\\' -- "${(V)krcs}"
        builtin eval "$krcs"
    fi

    if (( $+functions[_ksi_preexec] )); then
        builtin typeset -ag preexec_functions
        preexec_functions+=(_ksi_preexec)
    fi

    builtin typeset -ag precmd_functions
    if (( $+functions[_ksi_precmd] )); then
        precmd_functions=(${precmd_functions:/_ksi_deferred_init/_ksi_precmd})
        _ksi_precmd
    else
        precmd_functions=(${precmd_functions:#_ksi_deferred_init})
    fi

    if [ -n "${KITTY_IS_CLONE_LAUNCH}" ]; then
        builtin local orig_conda_env="$CONDA_DEFAULT_ENV"
        builtin eval "${KITTY_IS_CLONE_LAUNCH}"
        builtin hash -r 2> /dev/null 1> /dev/null
        builtin local venv="${VIRTUAL_ENV}/bin/activate"
        builtin local sourced=""
        _ksi_s_is_ok() {
            [[ -z "$sourced" && "$KITTY_CLONE_SOURCE_STRATEGIES" == *",$1,"* ]] && builtin return 0
            builtin return 1
        }

        if _ksi_s_is_ok "venv" && [[ -n "${VIRTUAL_ENV}" && -r "$venv" ]]; then
            sourced="y"
            builtin unset VIRTUAL_ENV
            builtin source "$venv"
        fi; if _ksi_s_is_ok "conda" && [[ -n "${CONDA_DEFAULT_ENV}" && (( $+commands[conda] )) && "${CONDA_DEFAULT_ENV}" != "$orig_conda_env" ]]; then
            sourced="y"
            conda activate "${CONDA_DEFAULT_ENV}"
        fi; if _ksi_s_is_ok "env_var" && [[ -n "${KITTY_CLONE_SOURCE_CODE}" ]]; then
            sourced="y"
            builtin eval "${KITTY_CLONE_SOURCE_CODE}"
        fi; if _ksi_s_is_ok "path" && [[ -r "${KITTY_CLONE_SOURCE_PATH}" ]]; then
            sourced="y"
            builtin source "${KITTY_CLONE_SOURCE_PATH}"
        fi
        builtin unfunction _ksi_s_is_ok
        # Ensure PATH has no duplicate entries
        builtin typeset -gxU PATH="$PATH"
    fi
    builtin unset KITTY_IS_CLONE_LAUNCH KITTY_CLONE_SOURCE_STRATEGIES

    builtin alias edit-in-kitty="kitten edit-in-kitty"

    if (( ! opt[(Ie)no-sudo] )) ; then
        if [[ -n "$TERMINFO" && ! ( -r "/usr/share/terminfo/x/xterm-kitty" || -r "/usr/share/terminfo/78/xterm-kitty" ) ]]; then
            sudo() {
                # Ensure terminfo is available in sudo
                builtin local is_sudoedit="n"
                for arg; do
                    if [[ "$arg" == "-e" || $arg == "--edit" ]]; then
                        is_sudoedit="y"
                        builtin break;
                    fi
                    [[ "$arg" != -* && "$arg" != *=* ]] && builtin break  # command found
                done
                if [[ "$is_sudoedit" == "y" ]]; then
                    builtin command sudo "$@";
                else
                    builtin command sudo TERMINFO="$TERMINFO" "$@";
                fi
            }
        fi
    fi

    # Map alt+left/right to move by word if not already mapped. This is expected behavior on macOS and I am tired
    # of answering questions about it.
    [[ $(builtin bindkey "^[[1;3C") == *" undefined-key" ]] && builtin bindkey "^[[1;3C" "forward-word"
    [[ $(builtin bindkey "^[[1;3D") == *" undefined-key" ]] && builtin bindkey "^[[1;3D" "backward-word"

    # Unfunction _ksi_deferred_init to save memory. Don't unfunction
    # kitty-integration though because decent public functions aren't supposed to
    # to unfunction themselves when invoked. Unfunctioning is done by calling code.
    builtin unfunction _ksi_deferred_init

}

_ksi_transmit_data() {
    builtin local data="${1//[[:space:]]}"
    builtin local pos=0
    builtin local chunk_num=0
    while [ $pos -lt ${#data} ]; do
        builtin local chunk="${data:$pos:2048}"
        pos=$(($pos+2048))
        builtin print -nu "$_ksi_fd" -f '\eP@kitty-%s|%s:%s\e\\' "${2}" "${chunk_num}" "${chunk}"
        chunk_num=$(($chunk_num+1))
    done
    # save history so it is available in new shell
    [ "$3" = "save_history" ] && builtin fc -AI
    builtin print -nu "$_ksi_fd" -f '\eP@kitty-%s|\e\\' "${2}"
}

clone-in-kitty() {
    builtin local data="shell=zsh,pid=$$,cwd=$(builtin printf "%s" "$PWD" | builtin command base64)"
    while :; do
        case "$1" in
            "") break;;
            -h|--help)
                builtin printf "%s\n\n%s\n" "Clone the current zsh session into a new kitty window." "For usage instructions see: https://sw.kovidgoyal.net/kitty/shell-integration/#clone-shell"
                builtin return
                ;;
            *) data="$data,a=$(builtin printf "%s" "$1" | builtin command base64)";;
        esac
        shift
    done
    builtin local env
    builtin local env_vars
    builtin local varname
    env_vars=(${(f)"$(builtin export)"})
    for i in $env_vars; do
        varname="${i%%=*}"
        env="${env}$(builtin printf "%s=%s\0" "$varname" "${(P)varname}")"
    done
    data="$data,env=$(builtin printf "%s" "$env" | builtin command base64)"
    _ksi_transmit_data "$data" "clone" "save_history"
}
```

[fish]

```
#!/bin/fish

# To use fish's autoloading feature, kitty prepends the vendored integration script directory to XDG_DATA_DIRS.
# The original paths needs to be restored here to not affect other programs.
# In particular, if the original XDG_DATA_DIRS does not exist, it needs to be removed.
if set -q KITTY_FISH_XDG_DATA_DIR
    if set -q XDG_DATA_DIRS
        set --global --export --path XDG_DATA_DIRS "$XDG_DATA_DIRS"
        if set --local index (contains --index "$KITTY_FISH_XDG_DATA_DIR" $XDG_DATA_DIRS)
            set --erase --global XDG_DATA_DIRS[$index]
            test -n "$XDG_DATA_DIRS" || set --erase --global XDG_DATA_DIRS
        end
        if set -q XDG_DATA_DIRS
            set --global --export --unpath XDG_DATA_DIRS "$XDG_DATA_DIRS"
        end
    end
    set --erase KITTY_FISH_XDG_DATA_DIR
end

status is-interactive || exit 0
not functions -q __ksi_schedule || exit 0
# Check fish version 3.3.0+ efficiently and fallback to check the minimum working version 3.2.0, exit on outdated versions.
# "Warning: Update fish to version 3.3.0+ to enable kitty shell integration.\n"
set -q fish_killring || set -q status_generation || string match -qnv "3.1.*" "$version"
or echo -en \eP@kitty-print\|V2FybmluZzogVXBkYXRlIGZpc2ggdG8gdmVyc2lvbiAzLjMuMCsgdG8gZW5hYmxlIGtpdHR5IHNoZWxsIGludGVncmF0aW9uLgo=\e\\ && exit 0 || exit 0

if test -n "$KITTY_SI_RUN_COMMAND_AT_STARTUP"
    printf '\e]2;%s\a' (string replace -ra '[\x00-\x1F\x7F]' '' -- "$KITTY_SI_RUN_COMMAND_AT_STARTUP")
    set --local _krcs "$KITTY_SI_RUN_COMMAND_AT_STARTUP"
    set --erase KITTY_SI_RUN_COMMAND_AT_STARTUP
    eval "$_krcs"
end

function __ksi_schedule --on-event fish_prompt -d "Setup kitty integration after other scripts have run, we hope"
    functions --erase __ksi_schedule
    test -n "$KITTY_SHELL_INTEGRATION" || return 0
    set --local _ksi (string split " " -- "$KITTY_SHELL_INTEGRATION")
    set --erase KITTY_SHELL_INTEGRATION
    if test -n "$SSH_KITTEN_KITTY_DIR"
        if not contains -- "$SSH_KITTEN_KITTY_DIR" "$PATH"
            if not type kitten 2> /dev/null > /dev/null
                set -gx PATH "$PATH" "$SSH_KITTEN_KITTY_DIR"
            end
        end
        set --erase SSH_KITTEN_KITTY_DIR
    end
    # Enable cursor shape changes for default mode and vi mode
    if not contains "no-cursor" $_ksi
        function __ksi_set_cursor --on-variable fish_key_bindings -d "Set the cursor shape for different modes when switching key bindings"
            if test "$fish_key_bindings" = fish_default_key_bindings
                function __ksi_bar_cursor --on-event fish_prompt -d "Set cursor shape to blinking bar on prompt"
                    echo -en "\e[5 q"
                end
                # Change the cursor shape on first run
                set -q argv[1]
                and __ksi_bar_cursor
            else
                functions --erase __ksi_bar_cursor
                contains "$fish_key_bindings" fish_vi_key_bindings fish_hybrid_key_bindings
                and __ksi_set_vi_cursor
            end
        end

        function __ksi_set_vi_cursor -d "Set the vi mode cursor shapes"
            # Set the vi mode cursor shapes only when none of them are configured
            set --local vi_modes fish_cursor_{default,insert,replace_one,visual}
            set -q $vi_modes
            test "$status" -eq 4 || return

            set --local vi_cursor_shapes block line underscore block
            for i in 1 2 3 4
                set --global $vi_modes[$i] $vi_cursor_shapes[$i] blink
            end

            # Change the cursor shape for current mode
            test "$fish_bind_mode" = "insert" && echo -en "\e[5 q" || echo -en "\e[1 q"
        end

        function __ksi_default_cursor --on-event fish_preexec -d "Set cursor shape to blinking default shape before executing command"
            echo -en "\e[0 q"
        end

        __ksi_set_cursor init
    end

    # Enable prompt marking with OSC 133
    if not contains "no-prompt-mark" $_ksi and not set -q __ksi_prompt_state
        set --local suffix ''
        if bind --function-names | string match -q forward-char-passive
            set suffix '-passive'
        end
        # fish 3.8 emits prompt markers, so we don't need to. It also is the
        # first version to define forward-char-passive so use that as a test to detect it
        if test "$suffix" = ""
            function __ksi_mark_prompt_start --on-event fish_prompt --on-event fish_cancel --on-event fish_posterror
                test "$__ksi_prompt_state" != prompt-start
                and echo -en "\e]133;D\a"
                set --global __ksi_prompt_state prompt-start
                echo -en "\e]133;A;special_key=1\a"
            end
            __ksi_mark_prompt_start

            function __ksi_mark_output_start --on-event fish_preexec
                set --global __ksi_prompt_state pre-exec
                printf '\e]133;C;cmdline_url=%s\a' (string escape --style=url -- "$argv")
            end

            function __ksi_mark_output_end --on-event fish_postexec
                set --global __ksi_prompt_state post-exec
                echo -en "\e]133;D;$status\a"
            end

            # With prompt marking, kitty clears the current prompt on resize,
            # so we need fish to redraw it.
            set --global fish_handle_reflow 1
        end

        # Binding for special key to move cursor on mouse click without triggering any
        # autocompletion or other effects
        for mode in (bind --list-modes | string match -v paste)  # bind in all modes except paste
            bind --preset -M "$mode" \e\[1u "forward-char$suffix"
            bind --preset -M "$mode" \e\[1\;1u "backward-char$suffix"
        end
    end

    # Enable CWD reporting
    if not contains "no-cwd" $_ksi
        # This function name is from fish and will override the builtin one, which is enabled by default for kitty in fish 3.5.0+.
        # We provide this to ensure that fish 3.2.0 and above will work.
        # https://github.com/fish-shell/fish-shell/blob/3.2.0/share/functions/__fish_config_interactive.fish#L275
        # An executed program could change cwd and report the changed cwd, so also report cwd at each new prompt
        function __update_cwd_osc --on-variable PWD --on-event fish_prompt -d "Report PWD changes to kitty"
            status is-command-substitution
            or echo -en "\e]7;kitty-shell-cwd://$hostname$PWD\a"
        end
        __update_cwd_osc
    end

    # Note that neither alias nor function is recursive in fish so if the user defines an alias/function
    # for sudo it will be clobbered by us, so only install this if sudo is not already function
    if not contains "no-sudo" $_ksi
        and test -n "$TERMINFO" -a "file" = (type -t sudo 2> /dev/null || echo "x")
        and not test -r "/usr/share/terminfo/x/xterm-kitty" -o -r "/usr/share/terminfo/78/xterm-kitty"
        # Ensure terminfo is available in sudo
        function sudo
            set --local is_sudoedit "n"
            for arg in $argv
                if string match -q -- "-e" "$arg" or string match -q -- "--edit" "$arg"
                    set is_sudoedit "y"
                    break
                end
                if not string match -r -q -- "^-" "$arg" and not string match -r -q -- "=" "$arg"
                    break  # reached the command
                end
            end
            if string match -q -- "$is_sudoedit" "y"
                command sudo $argv
            else
                command sudo TERMINFO="$TERMINFO" $argv
            end
        end
    end

    # Handle clone launches
    if test -n "$KITTY_IS_CLONE_LAUNCH"
        set --local orig_conda_env "$CONDA_DEFAULT_ENV"
        eval "$KITTY_IS_CLONE_LAUNCH"
        set --local venv "$VIRTUAL_ENV/bin/activate.fish"
        set --global _ksi_sourced
        function _ksi_s_is_ok
            test -z "$_ksi_sourced"
            and string match -q -- "*,$argv[1],*" "$KITTY_CLONE_SOURCE_STRATEGIES"
            and return 0
            return 1
        end
        if _ksi_s_is_ok "venv"
            and test -n "$VIRTUAL_ENV" -a -r "$venv"
            set _ksi_sourced "y"
            set --erase VIRTUAL_ENV _OLD_FISH_PROMPT_OVERRIDE  # activate.fish stupidly exports _OLD_FISH_PROMPT_OVERRIDE
            source "$venv"
        end
        if _ksi_s_is_ok "conda"
            and test -n "$CONDA_DEFAULT_ENV" -a "$CONDA_DEFAULT_ENV" != "$orig_conda_env"
            and functions -q conda
            set _ksi_sourced "y"
            conda activate "$CONDA_DEFAULT_ENV"
        end
        if _ksi_s_is_ok "env_var"
            and test -n "$KITTY_CLONE_SOURCE_CODE"
            set _ksi_sourced "y"
            eval "$KITTY_CLONE_SOURCE_CODE"
        end
        if _ksi_s_is_ok "path"
            and test -r "$KITTY_CLONE_SOURCE_PATH"
            set _ksi_sourced "y"
            source "$KITTY_CLONE_SOURCE_PATH"
        end
        set --erase KITTY_IS_CLONE_LAUNCH KITTY_CLONE_SOURCE_STRATEGIES _ksi_sourced
        functions --erase _ksi_s_is_ok

        # Ensure PATH has no duplicate entries
        set --local --path new_path
        for p in $PATH
            contains -- "$p" $new_path
            or set --append new_path "$p"
        end
        test (count $new_path) -eq (count $PATH)
        or set --global --export --path PATH $new_path
    end
end

function edit-in-kitty --wraps "kitten edit-in-kitty" -d "Edit the specified file in a kitty overlay window with your locally installed editor"
    kitten edit-in-kitty $argv
end

function __ksi_transmit_data -d "Transmit data to kitty using chunked DCS escapes"
    set --local data (string replace --regex --all -- "\s" "" "$argv[1]")
    set --local data_len (string length -- "$data")
    set --local pos 1
    set --local chunk_num 0
    while test "$pos" -le $data_len
        printf \eP@kitty-%s\|%s:%s\e\\ "$argv[2]" "$chunk_num" (string sub --start $pos --length 2048 -- "$data")
        set pos (math $pos + 2048)
        set chunk_num (math $chunk_num + 1)
    end
    printf \eP@kitty-%s\|\e\\ "$argv[2]"
end

function clone-in-kitty -d "Clone the current fish session into a new kitty window"
    set --local data
    for a in $argv
        if contains -- "$a" -h --help
            echo "Clone the current fish session into a new kitty window."
            echo
            echo "For usage instructions see: https://sw.kovidgoyal.net/kitty/shell-integration/#clone-shell"
            return
        end
        set --local ea (printf "%s" "$a" | base64)
        set --append data "a=$ea"
    end
    set --local envs
    for e in (set --export --names)
        set --append envs "$e=$$e"
    end
    set --local b64_envs (string join0 -- $envs | base64)
    set --local b64_cwd (printf "%s" "$PWD" | base64)
    set --prepend data "shell=fish" "pid=$fish_pid" "cwd=$b64_cwd" "env=$b64_envs"
    __ksi_transmit_data (string join "," -- $data) "clone"
end
```

[bash]

```
#!/bin/bash

if [[ "$-" != *i* ]] ; then builtin return; fi  # check in interactive mode
if [[ -z "$KITTY_SHELL_INTEGRATION" ]]; then builtin return; fi

# Load the normal bash startup files
if [[ -n "$KITTY_BASH_INJECT" ]]; then
    builtin declare kitty_bash_inject="$KITTY_BASH_INJECT"
    builtin declare ksi_val="$KITTY_SHELL_INTEGRATION"
    builtin unset KITTY_SHELL_INTEGRATION  # ensure manual sourcing of this file in bashrc does not have any effect
    builtin unset KITTY_BASH_INJECT ENV
    if [[ -z "$HOME" ]]; then HOME=~; fi
    if [[ -z "$KITTY_BASH_ETC_LOCATION" ]]; then KITTY_BASH_ETC_LOCATION="/etc"; fi

    _ksi_sourceable() {
        [[ -f "$1" && -r "$1" ]] && builtin return 0; builtin return 1;
    }

    if [[ -n "$ksi_val" && "$ksi_val" != *no-sudo* && -n "$TERMINFO" && ! ( -r "/usr/share/terminfo/x/xterm-kitty" || -r "/usr/share/terminfo/78/xterm-kitty" ) ]]; then
        # this must be done before sourcing user bashrc otherwise aliasing of sudo does not work
        sudo() {
            # Ensure terminfo is available in sudo
            builtin local is_sudoedit="n"
            for arg; do
                if [[ "$arg" == "-e" || $arg == "--edit" ]]; then
                    is_sudoedit="y"
                    builtin break;
                fi
                [[ "$arg" != -* && "$arg" != *=* ]] && builtin break  # command found
            done
            if [[ "$is_sudoedit" == "y" ]]; then
                builtin command sudo "$@";
            else
                builtin command sudo TERMINFO="$TERMINFO" "$@";
            fi
        }
    fi

    if [[ "$kitty_bash_inject" == *"posix"* ]]; then
        _ksi_sourceable "$KITTY_BASH_POSIX_ENV" && {
            builtin source "$KITTY_BASH_POSIX_ENV"
            builtin export ENV="$KITTY_BASH_POSIX_ENV"
        }
    else
        builtin set +o posix
        builtin shopt -u inherit_errexit 2>/dev/null  # resetting posix does not clear this
        if [[ -n "$KITTY_BASH_UNEXPORT_HISTFILE" ]]; then
            builtin export -n HISTFILE
            builtin unset KITTY_BASH_UNEXPORT_HISTFILE
        fi

        # See run_startup_files() in shell.c in the Bash source code
        if builtin shopt -q login_shell; then
            if [[ "$kitty_bash_inject" != *"no-profile"* ]]; then
                _ksi_sourceable "$KITTY_BASH_ETC_LOCATION/profile" && builtin source "$KITTY_BASH_ETC_LOCATION/profile"
                for _ksi_i in "$HOME/.bash_profile" "$HOME/.bash_login" "$HOME/.profile"; do
                    _ksi_sourceable "$_ksi_i" && { builtin source "$_ksi_i"; break; }
                done
            fi
        else
            if [[ "$kitty_bash_inject" != *"no-rc"* ]]; then
                # Linux distros build bash with -DSYS_BASHRC. Unfortunately, there is
                # no way to probe bash for it and different distros use different files
                # Arch, Debian, Ubuntu use /etc/bash.bashrc
                # Fedora uses /etc/bashrc sourced from ~/.bashrc instead of SYS_BASHRC
                # Void Linux uses /etc/bash/bashrc
                for _ksi_i in "$KITTY_BASH_ETC_LOCATION/bash.bashrc" "$KITTY_BASH_ETC_LOCATION/bash/bashrc" ; do
                    _ksi_sourceable "$_ksi_i" && { builtin source "$_ksi_i"; break; }
                done
                if [[ -z "$KITTY_BASH_RCFILE" ]]; then KITTY_BASH_RCFILE="$HOME/.bashrc"; fi
                _ksi_sourceable "$KITTY_BASH_RCFILE" && builtin source "$KITTY_BASH_RCFILE"
            fi
        fi
    fi
    builtin unset KITTY_BASH_RCFILE KITTY_BASH_POSIX_ENV KITTY_BASH_ETC_LOCATION
    builtin unset -f _ksi_sourceable
    builtin export KITTY_SHELL_INTEGRATION="$ksi_val"
    builtin unset _ksi_i ksi_val kitty_bash_inject
fi

if [ "${BASH_VERSINFO:-0}" -lt 4 ]; then
    builtin unset KITTY_SHELL_INTEGRATION
    builtin printf "%s\n" "Bash version ${BASH_VERSION} too old, kitty shell integration disabled" > /dev/stderr
    builtin return
fi

if [ -v "_ksi_prompt[sourced]" ]; then
    # we have already run
    builtin unset KITTY_SHELL_INTEGRATION
    builtin return
fi

# this is defined outside _ksi_main to make it global without using declare -g
# which is not available on older bash
builtin declare -A _ksi_prompt
_ksi_prompt=(
    [cursor]='y' [title]='y' [mark]='y' [complete]='y' [cwd]='y' [sudo]='y' [ps0]='' [ps0_suffix]='' [ps1]='' [ps1_suffix]='' [ps2]=''
    [hostname_prefix]='' [sourced]='y' [last_reported_cwd]=''
)

_ksi_main() {
    builtin local ifs="$IFS" i
    IFS=" "
    for i in ${KITTY_SHELL_INTEGRATION[@]}; do
        case "$i" in
            "no-cursor") _ksi_prompt[cursor]='n';;
            "no-title") _ksi_prompt[title]='n';;
            "no-prompt-mark") _ksi_prompt[mark]='n';;
            "no-complete") _ksi_prompt[complete]='n';;
            "no-cwd") _ksi_prompt[cwd]='n';;
            "no-sudo") _ksi_prompt[sudo]='n';;
        esac
    done
    IFS="$ifs"

    builtin unset KITTY_SHELL_INTEGRATION
    if [[ -n "$SSH_KITTEN_KITTY_DIR" ]]; then
        if [[ ! "$PATH" =~ (^|:)${SSH_KITTEN_KITTY_DIR}(:|$) ]] && [[ -z "$(builtin command -v kitten)" ]]; then
            builtin export PATH="${PATH}:${SSH_KITTEN_KITTY_DIR}"
        fi
        builtin unset SSH_KITTEN_KITTY_DIR
    fi
    builtin local krcs="$KITTY_SI_RUN_COMMAND_AT_STARTUP"
    builtin unset KITTY_SI_RUN_COMMAND_AT_STARTUP

    _ksi_debug_print() {
        # print a line to STDERR of parent kitty process
        builtin local b
        b=$(builtin command base64 <<< "${@}")
        builtin printf "\eP@kitty-print|%s\e\\" "${b//[[:space:]]}}"
    }

    _ksi_set_mark() {
        _ksi_prompt["${1}_mark"]="\[\e]133;k;${1}_kitty\a\]"
    }

    _ksi_set_mark start
    _ksi_set_mark end
    _ksi_set_mark start_secondary
    _ksi_set_mark end_secondary
    _ksi_set_mark start_suffix
    _ksi_set_mark end_suffix
    builtin unset -f _ksi_set_mark
    _ksi_prompt[secondary_prompt]="\n${_ksi_prompt[start_secondary_mark]}\[\e]133;A;k=s\a\]${_ksi_prompt[end_secondary_mark]}"

    _ksi_prompt_command() {
        # we first remove any previously added kitty code from the prompt variables and then add
        # it back, to ensure we have only a single instance
        if [[ -n "${_ksi_prompt[ps0]}" ]]; then
            PS0=${PS0//\\\[\\e\]133;k;start_kitty\\a\\\]*end_kitty\\a\\\]}
            PS0="${_ksi_prompt[ps0]}$PS0"
        fi
        if [[ -n "${_ksi_prompt[ps0_suffix]}" ]]; then
            PS0=${PS0//\\\[\\e\]133;k;start_suffix_kitty\\a\\\]*end_suffix_kitty\\a\\\]}
            PS0="${PS0}${_ksi_prompt[ps0_suffix]}"
        fi
        # restore PS1 to its pristine state without our additions
        if [[ -n "${_ksi_prompt[ps1]}" ]]; then
            PS1=${PS1//\\\[\\e\]133;k;start_kitty\\a\\\]*end_kitty\\a\\\]}
            PS1=${PS1//\\\[\\e\]133;k;start_secondary_kitty\\a\\\]*end_secondary_kitty\\a\\\]}
        fi
        if [[ -n "${_ksi_prompt[ps1_suffix]}" ]]; then
            PS1=${PS1//\\\[\\e\]133;k;start_suffix_kitty\\a\\\]*end_suffix_kitty\\a\\\]}
        fi
        if [[ -n "${_ksi_prompt[ps1]}" ]]; then
            if [[ "${_ksi_prompt[mark]}" == "y" && ( "${PS1}" == *"\n"* || "${PS1}" == *$'\n'* ) ]]; then
                builtin local oldval
                oldval=$(builtin shopt -p extglob)
                builtin shopt -s extglob
                # bash does not redraw the leading lines in a multiline prompt so
                # mark the last line as a secondary prompt. Otherwise on resize the
                # lines before the last line will be erased by kitty.
                # the first part removes everything from the last \n onwards
                # the second part appends a newline with the secondary marking
                # the third part appends everything after the last newline
                PS1=${PS1%@('\n'|$'\n')*}${_ksi_prompt[secondary_prompt]}${PS1##*@('\n'|$'\n')}
                builtin eval "$oldval"
            fi
            PS1="${_ksi_prompt[ps1]}$PS1"
        fi
        if [[ -n "${_ksi_prompt[ps1_suffix]}" ]]; then
            PS1="${PS1}${_ksi_prompt[ps1_suffix]}"
        fi
        if [[ -n "${_ksi_prompt[ps2]}" ]]; then
            PS2=${PS2//\\\[\\e\]133;k;start_kitty\\a\\\]*end_kitty\\a\\\]}
            PS2="${_ksi_prompt[ps2]}$PS2"
        fi

        if [[ "${_ksi_prompt[cwd]}" == "y" ]]; then
            # unfortunately bash provides no hooks to detect cwd changes
            # in particular this means cwd reporting will not happen for a
            # command like cd /test && cat. PS0 is evaluated before cd is run.
            if [[ "${_ksi_prompt[last_reported_cwd]}" != "$PWD" ]]; then
                _ksi_prompt[last_reported_cwd]="$PWD"
                builtin printf "\e]7;kitty-shell-cwd://%s%s\a" "$HOSTNAME" "$PWD"
            fi
        fi
    }

    if [[ "${_ksi_prompt[cursor]}" == "y" ]]; then
        _ksi_prompt[ps1_suffix]+="\[\e[5 q\]"  # blinking bar cursor
        _ksi_prompt[ps0_suffix]+="\[\e[0 q\]"  # blinking default cursor
    fi

    if [[ "${_ksi_prompt[title]}" == "y" ||  "${_ksi_prompt[mark]}" ]]; then
        _ksi_get_current_command() {
            builtin local last_cmd
            last_cmd=$(HISTTIMEFORMAT= builtin history 1)
            last_cmd="${last_cmd#*[[:digit:]]*[[:space:]]}"  # remove leading history number
            last_cmd="${last_cmd#"${last_cmd%%[![:space:]]*}"}"  # remove remaining leading whitespace
            if [[ "${_ksi_prompt[title]}" == "y" ]]; then
                builtin printf "\e]2;%s%s\a" "${_ksi_prompt[hostname_prefix]@P}" "${last_cmd//[[:cntrl:]]}" # removes any control characters
            fi
            if [[ "${_ksi_prompt[mark]}" == "y" ]]; then
                builtin printf "\e]133;C;cmdline=%q\a" "$last_cmd"
            fi
        }
        _ksi_prompt[ps0]+='$(_ksi_get_current_command > /dev/tty)';
    fi

    if [[ "${_ksi_prompt[title]}" == "y" ]]; then
        if [[ -z "$KITTY_PID" ]]; then
            if [[ -n "$SSH_TTY" || -n "$SSH2_TTY$KITTY_WINDOW_ID" ]]; then
                # connected to most SSH servers
                # or use ssh kitten to connected to some SSH servers that do not set SSH_TTY
                _ksi_prompt[hostname_prefix]="\h: "
            elif [[ -n "$(builtin command -v who)" && "$(builtin command who -m 2> /dev/null)" =~ "\([a-fA-F.:0-9]+\)$" ]]; then
                # the shell integration script is installed manually on the remote system
                # the environment variables are cleared after sudo
                # OpenSSH's sshd creates entries in utmp for every login so use those
                _ksi_prompt[hostname_prefix]="\h: "
            fi
        fi
        # see https://www.gnu.org/software/bash/manual/html_node/Controlling-the-Prompt.html#Controlling-the-Prompt
        # we use suffix here because some distros add title setting to their bashrc files by default
        _ksi_prompt[ps1_suffix]+="\[\e]2;${_ksi_prompt[hostname_prefix]}\w\a\]"
        if [[ "$HISTCONTROL" == *"ignoreboth"* ]] || [[ "$HISTCONTROL" == *"ignorespace"* ]]; then
            _ksi_debug_print "ignoreboth or ignorespace present in bash HISTCONTROL setting, showing running command will not be robust"
        fi
    fi

    if [[ "${_ksi_prompt[mark]}" == "y" ]]; then
        # this can result in multiple D prompt marks or ones that dont
        # correspond to a cmd but kitty handles this gracefully, only
        # taking into account the first D after a C.
        _ksi_prompt[ps1]+="\[\e]133;D;\$?\a\e]133;A\a\]"
        _ksi_prompt[ps2]+="\[\e]133;A;k=s\a\]"
    fi

    builtin alias edit-in-kitty="kitten edit-in-kitty"

    if [[ "${_ksi_prompt[complete]}" == "y" ]]; then
        _ksi_completions() {
            builtin local src
            builtin local limit
            # Send all words up to the word the cursor is currently on
            builtin let limit=1+$COMP_CWORD
            src=$(builtin printf "%s\n" "${COMP_WORDS[@]:0:$limit}" | builtin command kitten __complete__ bash)
            if [[ $? == 0 ]]; then
                builtin eval "${src}"
            fi
        }
        builtin complete -F _ksi_completions kitty
        builtin complete -F _ksi_completions edit-in-kitty
        builtin complete -F _ksi_completions clone-in-kitty
        builtin complete -F _ksi_completions kitten
    fi

    # wrap our prompt additions in markers we can use to remove them using
    # bash's anemic pattern substitution
    if [[ -n "${_ksi_prompt[ps0]}" ]]; then
        _ksi_prompt[ps0]="${_ksi_prompt[start_mark]}${_ksi_prompt[ps0]}${_ksi_prompt[end_mark]}"
    fi
    if [[ -n "${_ksi_prompt[ps0_suffix]}" ]]; then
        _ksi_prompt[ps0_suffix]="${_ksi_prompt[start_suffix_mark]}${_ksi_prompt[ps0_suffix]}${_ksi_prompt[end_suffix_mark]}"
    fi
    if [[ -n "${_ksi_prompt[ps1]}" ]]; then
        _ksi_prompt[ps1]="${_ksi_prompt[start_mark]}${_ksi_prompt[ps1]}${_ksi_prompt[end_mark]}"
    fi
    if [[ -n "${_ksi_prompt[ps1_suffix]}" ]]; then
        _ksi_prompt[ps1_suffix]="${_ksi_prompt[start_suffix_mark]}${_ksi_prompt[ps1_suffix]}${_ksi_prompt[end_suffix_mark]}"
    fi
    if [[ -n "${_ksi_prompt[ps2]}" ]]; then
        _ksi_prompt[ps2]="${_ksi_prompt[start_mark]}${_ksi_prompt[ps2]}${_ksi_prompt[end_mark]}"
    fi
    # BASH aborts the entire script when doing unset with failglob set, somebody should report this upstream
    builtin local oldval
    oldval=$(builtin shopt -p failglob)
    builtin shopt -u failglob
    builtin unset _ksi_prompt[start_mark] _ksi_prompt[end_mark] _ksi_prompt[start_suffix_mark] _ksi_prompt[end_suffix_mark] _ksi_prompt[start_secondary_mark] _ksi_prompt[end_secondary_mark]
    builtin eval "$oldval"

    # install our prompt command, using an array if it is unset or already an array,
    # otherwise append a string. We check if _ksi_prompt_command exists as some shell
    # scripts stupidly export PROMPT_COMMAND making it inherited by all programs launched
    # from the shell
    builtin local pc
    pc='builtin declare -F _ksi_prompt_command > /dev/null 2> /dev/null && _ksi_prompt_command'
    if [[ -z "${PROMPT_COMMAND[*]}" ]]; then
        PROMPT_COMMAND=([0]="$pc")
    elif [[ $(builtin declare -p PROMPT_COMMAND 2> /dev/null) =~ 'declare -a PROMPT_COMMAND' ]]; then
        PROMPT_COMMAND+=("$pc")
    else
        builtin local oldval
        oldval=$(builtin shopt -p extglob)
        builtin shopt -s extglob
        PROMPT_COMMAND="${PROMPT_COMMAND%%+([[:space:]])}"
        PROMPT_COMMAND="${PROMPT_COMMAND%%+(;)}"
        builtin eval "$oldval"
        PROMPT_COMMAND+="; $pc"
    fi
    if [ -n "${KITTY_IS_CLONE_LAUNCH}" ]; then
        builtin local orig_conda_env="$CONDA_DEFAULT_ENV"
        builtin eval "${KITTY_IS_CLONE_LAUNCH}"
        builtin hash -r 2> /dev/null 1> /dev/null
        builtin local venv="${VIRTUAL_ENV}/bin/activate"
        builtin local sourced=""
        _ksi_s_is_ok() {
            [[ -z "$sourced" && "$KITTY_CLONE_SOURCE_STRATEGIES" == *",$1,"* ]] && builtin return 0
            builtin return 1
        }

        if _ksi_s_is_ok "venv" && [ -n "${VIRTUAL_ENV}" -a -r "$venv" ]; then
            sourced="y"
            builtin unset VIRTUAL_ENV
            builtin source "$venv"
        fi; if _ksi_s_is_ok "conda" && [ -n "${CONDA_DEFAULT_ENV}" ] && builtin command -v conda >/dev/null 2>/dev/null && [ "${CONDA_DEFAULT_ENV}" != "$orig_conda_env" ]; then
            sourced="y"
            conda activate "${CONDA_DEFAULT_ENV}"
        fi; if _ksi_s_is_ok "env_var" && [[ -n "${KITTY_CLONE_SOURCE_CODE}" ]]; then
            sourced="y"
            builtin eval "${KITTY_CLONE_SOURCE_CODE}"
        fi; if _ksi_s_is_ok "path" && [[ -r "${KITTY_CLONE_SOURCE_PATH}" ]]; then
            sourced="y"
            builtin source "${KITTY_CLONE_SOURCE_PATH}"
        fi
        builtin unset -f _ksi_s_is_ok
        # Ensure PATH has no duplicate entries
        if [ -n "$PATH" ]; then
            builtin local old_PATH=$PATH:; PATH=
            while [ -n "$old_PATH" ]; do
                builtin local x
                x=${old_PATH%%:*}
                case $PATH: in
                    *:"$x":*) ;;
                    *) PATH=$PATH:$x;;
                esac
                old_PATH=${old_PATH#*:}
            done
            PATH=${PATH#:}
        fi
    fi
    builtin unset KITTY_IS_CLONE_LAUNCH KITTY_CLONE_SOURCE_STRATEGIES
    if [[ -n "$krcs" ]]; then builtin
        builtin printf "\e]2;%s\a" "${krcs//[[:cntrl:]]}" # removes any control characters
        eval "$krcs";
    fi
}
_ksi_main
builtin unset -f _ksi_main

case :$SHELLOPTS: in
  *:posix:*) ;;
  *)

_ksi_transmit_data() {
    builtin local data
    data="${1//[[:space:]]}"
    builtin local pos=0
    builtin local chunk_num=0
    while [ $pos -lt ${#data} ]; do
        builtin local chunk="${data:$pos:2048}"
        pos=$(($pos+2048))
        builtin printf '\eP@kitty-%s|%s:%s\e\\' "${2}" "${chunk_num}" "${chunk}"
        chunk_num=$(($chunk_num+1))
    done
    # save history so it is available in new shell
    [ "$3" = "save_history" ] && builtin history -a
    builtin printf '\eP@kitty-%s|\e\\' "${2}"
}

clone-in-kitty() {
    builtin local bv="${BASH_VERSINFO[0]}.${BASH_VERSINFO[1]}.${BASH_VERSINFO[2]}"
    builtin local data="shell=bash,pid=$$,bash_version=$bv,cwd=$(builtin printf "%s" "$PWD" | builtin command base64),envfmt=bash,env=$(builtin export | builtin command base64)"
    while :; do
        case "$1" in
            "") break;;
            -h|--help)
                builtin printf "%s\n\n%s\n" "Clone the current bash session into a new kitty window." "For usage instructions see: https://sw.kovidgoyal.net/kitty/shell-integration/#clone-shell"
                builtin return
                ;;
            *) data="$data,a=$(builtin printf "%s" "$1" | builtin command base64)";;
        esac
        shift
    done
    _ksi_transmit_data "$data" "clone" "save_history"
}

      ;;
esac
```

# Shell integration over SSH[¶](#shell-integration-over-ssh "Link to this heading")

The easiest way to have shell integration work when SSHing into remote systems
is to use the [ssh kitten](../kittens/ssh/). Simply run:

```
kitten ssh hostname
```

And, by magic, you will be logged into the remote system with fully functional
shell integration. Alternately, you can [setup shell integration manually](#manual-shell-integration), by copying the kitty shell integration scripts to
the remote server and editing the shell rc files there, as described below.

# Shell integration in a container[¶](#shell-integration-in-a-container "Link to this heading")

Install the kitten [standalone binary](https://github.com/kovidgoyal/kitty/releases/latest/download/kitten-linux-amd64) in the container
somewhere in the PATH, then you can log into the container with:

```
docker exec -ti container-id kitten run-shell --shell=/path/to/your/shell/in/the/container
```

The kitten will even take care of making the kitty terminfo database available
in the container automatically.

# Clone the current shell into a new window[¶](#clone-the-current-shell-into-a-new-window "Link to this heading")

You can clone the current shell into a new kitty window by simply running the
**clone-in-kitty** command, for example:

```
clone-in-kitty
clone-in-kitty --type=tab
clone-in-kitty --title "I am a clone"
```

This will open a new window running a new shell instance but with all
environment variables and the current working directory copied. This even works
over SSH when using [Truly convenient SSH](../kittens/ssh/).

The **clone-in-kitty** command takes almost all the same arguments as the
[launch](../launch/) command, so you can open a new tab instead or a new OS
window, etc. Arguments of launch that can cause code execution or that don’t
make sense when cloning are ignored. Most prominently, the following options are
ignored: [`--allow-remote-control`](../launch/#cmdoption-launch-allow-remote-control),
[`--copy-cmdline`](../launch/#cmdoption-launch-copy-cmdline), [`--copy-env`](../launch/#cmdoption-launch-copy-env), [`--stdin-source`](../launch/#cmdoption-launch-stdin-source),
[`--marker`](../launch/#cmdoption-launch-marker) and [`--watcher`](../launch/#cmdoption-launch-watcher).

**clone-in-kitty** can be configured to source arbitrary code in the
cloned window using environment variables. It will automatically clone virtual
environments created by the [Python venv module](https://docs.python.org/3/library/venv.html) or [Conda](https://conda.io/). In addition, setting the
env var [`KITTY_CLONE_SOURCE_CODE`](../glossary/#envvar-KITTY_CLONE_SOURCE_CODE) to some shell code will cause that
code to be run in the cloned window with `eval`. Similarly, setting
[`KITTY_CLONE_SOURCE_PATH`](../glossary/#envvar-KITTY_CLONE_SOURCE_PATH) to the path of a file will cause that file to
be sourced in the cloned window. This can be controlled by
[`clone_source_strategies`](../conf/#opt-kitty.clone_source_strategies).

**clone-in-kitty** works by asking the shell to serialize its internal
state (mainly CWD and env vars) and this state is transmitted to kitty and
restored by the shell integration scripts in the cloned window.

# Edit files in new kitty windows even over SSH[¶](#edit-files-in-new-kitty-windows-even-over-ssh "Link to this heading")

```
edit-in-kitty myfile.txt
edit-in-kitty --type tab --title "Editing My File" myfile.txt
# open myfile.txt at line 75 (works with vim, neovim, emacs, nano, micro)
edit-in-kitty +75 myfile.txt
```

The **edit-in-kitty** command allows you to seamlessly edit files
in your default [`editor`](../conf/#opt-kitty.editor) in new kitty windows. This works even over
SSH (if you use the [ssh kitten](../kittens/ssh/)), allowing you
to easily edit remote files in your local editor with all its bells and
whistles.

The **edit-in-kitty** command takes almost all the same arguments as the
[launch](../launch/) command, so you can open a new tab instead or a new OS
window, etc. Not all arguments are supported, see the discussion in the
[Clone the current shell into a new window](#clone-shell) section above.

In order to avoid remote code execution, kitty will only execute the configured
editor and pass the file path to edit to it.

Note

To edit files using sudo the best method is to set the
`SUDO_EDITOR` environment variable to `kitten edit-in-kitty` and
then edit the file using the `sudoedit` or `sudo -e` commands.

# Using shell integration in sub-shells, containers, etc.[¶](#using-shell-integration-in-sub-shells-containers-etc "Link to this heading")

Added in version 0.29.0.

To start a sub-shell with shell integration automatically setup, simply run:

```
kitten run-shell
```

This will start a sub-shell using the same binary as the currently running
shell, with shell-integration enabled. To start a particular shell use:

```
kitten run-shell --shell=/bin/bash
```

To run a command before starting the shell use:

```
kitten run-shell ls .
```

This will run `ls .` before starting the shell.

This will even work on remote systems where kitty itself is not installed,
provided you use the [SSH kitten](../kittens/ssh/) to connect to the system.
Use `kitten run-shell --help` to learn more.

# Manual shell integration[¶](#manual-shell-integration "Link to this heading")

The automatic shell integration is designed to be minimally intrusive, as such
it won’t work for sub-shells, terminal multiplexers, containers, etc.
For such systems, you should either use the [run-shell](#run-shell) command described above or
setup manual shell integration by adding some code to your shells startup files to load the shell integration script.

First, in `kitty.conf` set:

```
shell_integration disabled
```

Then in your shell’s rc file, add the lines:

zsh

```
if test -n "$KITTY_INSTALLATION_DIR"; then
    export KITTY_SHELL_INTEGRATION="enabled"
    autoload -Uz -- "$KITTY_INSTALLATION_DIR"/shell-integration/zsh/kitty-integration
    kitty-integration
    unfunction kitty-integration
fi
```

fish

```
if set -q KITTY_INSTALLATION_DIR
    set --global KITTY_SHELL_INTEGRATION enabled
    source "$KITTY_INSTALLATION_DIR/shell-integration/fish/vendor_conf.d/kitty-shell-integration.fish"
    set --prepend fish_complete_path "$KITTY_INSTALLATION_DIR/shell-integration/fish/vendor_completions.d"
end
```

bash

```
if test -n "$KITTY_INSTALLATION_DIR"; then
    export KITTY_SHELL_INTEGRATION="enabled"
    source "$KITTY_INSTALLATION_DIR/shell-integration/bash/kitty.bash"
fi
```

The value of [`KITTY_SHELL_INTEGRATION`](../glossary/#envvar-KITTY_SHELL_INTEGRATION) is the same as that for
[`shell_integration`](../conf/#opt-kitty.shell_integration), except if you want to disable shell integration
completely, in which case simply do not set the
[`KITTY_SHELL_INTEGRATION`](../glossary/#envvar-KITTY_SHELL_INTEGRATION) variable at all.

In a container, you will need to install the kitty shell integration scripts
and make sure the [`KITTY_INSTALLATION_DIR`](../glossary/#envvar-KITTY_INSTALLATION_DIR) environment variable is set
to point to the location of the scripts.

# Integration with other shells[¶](#integration-with-other-shells "Link to this heading")

There exist third-party integrations to use these features for various other
shells:

* Jupyter console and IPython via a patch ([#4475](https://github.com/kovidgoyal/kitty/issues/4475))
* [xonsh](https://github.com/xonsh/xonsh/issues/4623)
* [Nushell](https://github.com/nushell/nushell/discussions/12065): Set `$env.config.shell_integration = true` in your `config.nu` to enable it.

# Notes for shell developers[¶](#notes-for-shell-developers "Link to this heading")

The protocol used for marking the prompt is very simple. You should consider
adding it to your shell as a builtin. Many modern terminals make use of it, for
example: kitty, iTerm2, WezTerm, DomTerm

Just before starting to draw the PS1 prompt send the escape code:

```
<OSC>133;A<ST>
```

Just before starting to draw the PS2 prompt send the escape code:

```
<OSC>133;A;k=s<ST>
```

Just before running a command/program, send the escape code:

```
<OSC>133;C<ST>
```

Optionally, when a command is finished its “exit status” can be reported as:

```
<OSC>133;D;exit status as base 10 integer<ST>
```

Here `<OSC>` is the bytes `0x1b 0x5d` and `<ST>` is the bytes `0x1b
0x5c`. This is exactly what is needed for shell integration in kitty. For the
full protocol, that also marks the command region, see [the iTerm2 docs](https://iterm2.com/documentation-escape-codes.html).

kitty additionally supports several extra fields for the `<OSC>133;A` command
to control its behavior, separated by semi-colons. They are:

`redraw=0`
:   this tells kitty that the shell will not redraw the prompt on
    resize so it should not erase it

`special_key=1`
:   this tells kitty to use a special key instead of arrow keys
    to move the cursor on mouse click. Useful if arrow keys have side-effects
    like triggering auto complete. The shell integration script then binds the
    special key, as needed.

`k=s`
:   this tells kitty that the secondary (PS2) prompt is starting at the
    current line.

`click_events=1`
:   this tells kitty that the shell is capable of handling
    mouse click events. kitty will thus send a click event to the shell when
    the user clicks somewhere in the prompt. The shell can then move the cursor
    to that position or perform some other appropriate action. Without this,
    kitty will instead generate a number of fake key events to move the cursor
    to the clicked location, which is not fully robust.

kitty also optionally supports sending the cmdline going to be executed with `<OSC>133;C` as:

```
<OSC>133;C;cmdline=cmdline encoded by %q<ST>
or
<OSC>133;C;cmdline_url=cmdline as UTF-8 URL %-escaped text<ST>
```

Here, *encoded by %q* means the encoding produced by the %q format to printf in
bash and similar shells. Which is basically shell escaping with the addition of
using [ANSI C quoting](https://www.gnu.org/software/bash/manual/html_node/ANSI_002dC-Quoting.html#ANSI_002dC-Quoting)
for control characters (`$''` quoting).