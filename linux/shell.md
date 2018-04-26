
# Bash

## Shell prompt

in .bashrc or whatever:

```
# set a fancy prompt (non-color, unless we know we "want" color)
case "$TERM" in
    xterm-color|*-256color) color_prompt=yes;;
esac

# uncomment for a colored prompt, if the terminal has the capability; turned
# off by default to not distract the user: the focus in a terminal window
# should be on the output of commands, not on the prompt
#force_color_prompt=yes

if [ -n "$force_color_prompt" ]; then
    if [ -x /usr/bin/tput ] && tput setaf 1 >&/dev/null; then
        # We have color support; assume it's compliant with Ecma-48
        # (ISO/IEC-6429). (Lack of such support is extremely rare, and such
        # a case would tend to support setf rather than setaf.)
        color_prompt=yes
    else
        color_prompt=
    fi
fi
    
if [ "$color_prompt" = yes ]; then
    PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ '
else
    PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi

# enable color support of ls and also add handy aliases
if [ -x /usr/bin/dircolors ]; then
    test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
    alias ls='ls --color=auto'
    alias grep='grep --color=auto'
    alias fgrep='fgrep --color=auto'
    alias egrep='egrep --color=auto'
fi

```

## Epoch timestamp to human date

    date -d @1499568328

## Loop through series of dates

```
DATE=2017-01-01
ENDDATE=2018-01-01
while [ "$DATE" != "$ENDDATE" ]; do 
  echo $DATE
  DATE=$(date -I -d "$DATE + 1 day")
done
```

# Grep

## Count all instances (multiple per line)

    grep -o string filename

## Count instances per line, sort by counts

single file:

    grep -on searchterm file | cut -d: -f1 | uniq -c | sort -n

many files:

    grep -on searchterm files* | cut -d: -f1,2 | uniq -c | sort -n

# Rename file

Rename a group of files via a regex, e.g. to remove a common prefix:

    rename 's/someprefixtoremove//' *.csv

# Split line by char

Sed:

    sed 's/pattern/\n/g'

tr:

    tr ',' $'\n'
    
# Add column of numbers

    cat numbers.txt | paste -sd+ - | bc
