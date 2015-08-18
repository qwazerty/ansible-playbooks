#################################
# dotzshrc config file          #
# by Kevin "qwazerty" Houdebert #
#################################

# Set the editor to vim
export EDITOR='vim'

# Set the pager to vimpager if exist
if [ -e /usr/bin/vimpager ]; then
    export PAGER='vimpager'
else
    export PAGER='less'
fi

# Set language to en_US.utf8
export LANG=en_US.UTF-8

# Set TERMINAL for i3-sensible-terminal
export TERMINAL=urxvt

if [ -n "$TMUX" ]; then
    export TERM=screen-256color
fi

# Set NNTP Server for epita newsgroups (slrn)
export NNTPSERVER=news.epita.fr

# History file path
export HISTFILE=~/.histfile

# Zsh session history size
export HISTSIZE=10000

# History file size
export SAVEHIST=10000

# Color for less
export LESS_TERMCAP_mb=$(printf "\e[0;31m")
export LESS_TERMCAP_md=$(printf "\e[0;31m")
export LESS_TERMCAP_me=$(printf "\e[0m")
export LESS_TERMCAP_se=$(printf "\e[0m")
export LESS_TERMCAP_so=$(printf "\e[0;44;33m")
export LESS_TERMCAP_ue=$(printf "\e[0m")
export LESS_TERMCAP_us=$(printf "\e[0;32m")

# Source ssh-agent
[ -e ~/.ssh/ssh_${HOST}_${USER}.agent ] && . ~/.ssh/ssh_${HOST}_${USER}.agent

# Common aliases
case $(uname -s) in
    Linux|CYGWIN_NT*)
        alias ls='ls --color'
        alias l='ls'
        alias la='ls -la'
        alias ll='ls -l'
        alias am='alsamixer'
        ;;
    FreeBSD)
        alias ls='ls -G'
        alias l='ls'
        alias la='ls -la'
        alias ll='ls -l'
        alias am='rexima'
        ;;
esac

alias cdo='cd $_'
alias cdb='cd -'

alias e='vim'
alias u='ls'
alias o='cd'
alias j='jobs'
alias mk='mkdir -p'

alias wm_name='xprop | grep WM_CLASS'
alias chmox='chmod +x'
alias tmux='tmux -2'

alias g='git'
alias z='i3lock -c 424242'

alias red='redshift -l 48.8566:2.3522'
alias ..='source ~/.zshrc'
epath() { export PATH=$PATH:$1 }
alias dog='highlight -O ansi'
ss() { /usr/bin/ss $@ | column -t }

# Setxkbmap aliases
alias us='setxkbmap us'
alias usi='setxkbmap us_intl'
alias fr='setxkbmap fr'
alias dv='setxkbmap us dvorak-alt-intl'

# Makefile aliases
alias m='make'
alias nake='make'
alias cm='./configure && make'
alias bcm='make distclean; ./bootstrap && ./configure && make'
alias bcdm='make distclean; ./bootstrap && ./configure -with-debug && make'
alias mclm='make clean && make'

# Haha.
alias emacs='emacs -nw'

# Programming aliases
alias valgrindfull='valgrind -v --leak-check=full --show-reachable=yes \
    --track-fds=yes --track-origins=yes'
# Dat flags
alias gppf='g++ -W -Wall -Wextra -Werror -std=c++0x -pedantic'
alias gccf='gcc -std=c99 -pedantic -Wall \
    -Wno-missing-braces -Wextra -Wno-missing-field-initializers -Wformat=2 \
    -Wswitch-default -Wswitch-enum -Wcast-align -Wpointer-arith \
    -Wbad-function-cast -Wstrict-overflow=5 -Wstrict-prototypes -Winline \
    -Wundef -Wnested-externs -Wcast-qual -Wshadow -Wunreachable-code \
    -Wlogical-op -Wfloat-equal -Wstrict-aliasing=2 -Wredundant-decls \
    -Wold-style-definition -Werror \
    -ggdb3 -g \
    -O0 \
    -fno-omit-frame-pointer -ffloat-store -fno-common -fstrict-aliasing'
alias retag='ctags --tag-relative -Rf.git/tags'

# Start ssh-agent
alias ssha='ssh-agent -t 12h | grep -v echo > ~/.ssh/ssh_${HOST}_${USER}.agent && source ~/.ssh/ssh_${HOST}_${USER}.agent && ssh-add'
alias sshk='eval $(ssh-agent -k); rm ~/.ssh/ssh_${HOST}_${USER}.agent'
alias sshr='ssh-keygen -R'
alias venv='source venv/bin/activate'

# UNsafe SSH
alias unssh='ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no'
alias unscp='scp -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no'

# Ping test
alias pt='ping www.google.com'
alias ptt='ping www.acu.epita.fr'
alias myip='curl ifconfig.co'

# Binding emacs mode bindings keys
bindkey -e
bindkey '^[Od' emacs-backward-word
bindkey '^[Oc' emacs-forward-word
bindkey '^B' emacs-backward-word
bindkey '^F' emacs-forward-word

# The following lines were added by compinstall
zstyle :compinstall filename '/home/qwazerty/.zshrc'

autoload -U compinit promptinit vcs_info
compinit
promptinit
# End of lines added by compinstall

# Disable beep sound
unsetopt beep

# Disable matching
unsetopt nomatch

# Disable extented globing
unsetopt extendedglob

# Ignore duplicate in history
setopt histignoredups

zstyle ':completion:*' verbose true
zstyle ':completion:*' menu select=1
zstyle ':vcs_info:*' enable git svn

autoload -U colors && colors
setopt prompt_subst

prompt_char() {
    echo -n "%(?.%{$fg[blue]%}.%{$fg[red]%})"
    if [ $UID -eq 0 ]; then echo -n "#"; else echo -n $; fi
    echo -n "%{$reset_color%}"
}

vcs_precmd() {
    vcs_info
    zstyle ':vcs_info:*' formats '%b'
    zstyle ':vcs_info:*' enable git hg
}

parse_git_branch() {
    VCS_INFO="${vcs_info_msg_0_}"
    [ -n "$VCS_INFO" ] && echo "%{$fg[red]%}(%{$fg[cyan]%}$VCS_INFO%{$fg[red]%})%{$reset_color%} "
}

clock() {
    echo "%(?.%{$fg[blue]%}.%{$fg[red]%})%*%{$reset_color%}"
}

prompt_preexec() {
    CALCTIME=1
    CMDSTARTTIME=$SECONDS
}

prompt_precmd() {
    if (( CALCTIME )); then
        TIMER_SHOW=$(($SECONDS-$CMDSTARTTIME))
    fi
    CALCTIME=0
}

timer_show() {
    timer=$TIMER_SHOW
    if [ "$timer" -ne 0 ]; then
        tmp=$timer
        timer=$(($tmp / 60)):$(printf "%02d" $(($tmp % 60)))
        echo "%{$fg[red]%}(%{$fg[cyan]%}$timer%{$fg[red]%}) "
    fi
}

prompt_ssh() {
    if [ -n "$SSH_CONNECTION" ]; then
        echo "%{$fg[magenta]%}"
    else
        echo "%{$fg[red]%}"
    fi
}

prompt_ssh_agent() {
    [ -n "$SSH_AGENT_PID" ] && echo "%{$fg[red]%}(%{$fg[cyan]%}ssh%{$fg[red]%}) %{$reset_color%}"
}

prompt_openstack() {
    if [ -n "$OS_USERNAME" ]; then
        echo "%{$fg[red]%}(%{$fg[cyan]%}os:$OS_USERNAME%{$fg[red]%}) %{$reset_color%}"
    fi
}

add-zsh-hook precmd prompt_precmd
add-zsh-hook precmd vcs_precmd
add-zsh-hook preexec prompt_preexec

export PROMPT='%(!.$(prompt_ssh).%{$fg[yellow]%}%n$(prompt_ssh)@)%m %{$fg[blue]%}%~ $(prompt_char)%{$reset_color%} '
export RPROMPT='$(timer_show)$(prompt_openstack)$(prompt_ssh_agent)$(parse_git_branch)$(clock)'

# Set the current command as title
# Jobs display thanks to Chmool

title_jobs() {
    TITLE_JOBS=$(jobs | wc -l 2>/dev/null)
    [ $TITLE_JOBS -ne 0 ] && echo "($TITLE_JOBS) "
}

title_path() {
    if [[ "$PWD" =~ ^"$HOME"(/|$) ]]; then
        echo "[~${PWD#$HOME}]"
    else
        echo "[$PWD]"
    fi
}

title_ssh() {
    [ -n "$SSH_CONNECTION" ] && echo "[ssh] "
}

set_title() {
    echo -n "\e]2;$(title_ssh)$(title_jobs)$(title_path) $1\a\a"
}

set_title_precmd() {
    set_title "${JOBS}${USER}@${HOST}"
}

set_title_preexec() {
    set_title $1
}

if [ "$TERM" != "linux" ]; then
    add-zsh-hook precmd set_title_precmd
    add-zsh-hook preexec set_title_preexec
fi

# Load custom conf file
[ -e ~/.myzshrc ] && source ~/.myzshrc
[ -d ~/.zsh/ ] && for i in ~/.zsh/*; do source $i; done

if [ "$TTY" = "/dev/tty1" ]; then
    exec startx
fi

true
