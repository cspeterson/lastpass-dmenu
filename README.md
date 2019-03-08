Lastpass-dmenu
==============

Pop-up LastPass desktop quick-search. Puts the selection into the clipboard or has xdotool type it out for you.

# Install

This will work on Ubuntu, but will look really similar on other distros:

```sh
# Lastpass cli is the lastpass cli client from LastPass themselves
# Dmenu is the utility that does the pop-up selection
sudo apt-get install dmenu lastpass-cli
wget -O /path/to/where/you/want/this/script https://raw.githubusercontent.com/cspeterson/lastpass-dmenu/master/lastpass-dmenu
chmod +x /path/to/where/you/want/this/script
# Login to lastpass-cli one time and it will remember your email for the
# future
lpass login myuser@ias.edu
```

# Usage

```sh
Usage:
	lastpass-dmenu [OPTIONS]... [copy|type]

Options:
	-n, --enable-notes
			Enable the return of secure notes. When this option is set, this
			script will try to return the secure note from a selection if the
			password is not present. Default: disabled

Positional arguments:
	[copy|type]
			Specify what to do with the selected password/note: copy to the
			clipboard, or have xdotool type it for you.
```

##  Examples

```sh
Put the password into the clipboard:
		lastpass-dmenu copy

Have the script type out the password for you:
		lastpass-dmenu type

Put the password into the clipboard OR if there is no password field for
the selection, try to copy any secure note attached to the selection:
		lastpass-dmenu --enable-notes copy
```

#  Security

```sh
Please make copy mode more secure by limiting X selection requests on the
clipboard. Lpass-cli can do this by setting the environment variable
`LPASS_CLIPBOARD_COMMAND` as per lastpass-cli documentation.

xclip can do this by limiting the number of paste requests that can come
from this selection:
		export LPASS_CLIPBOARD_COMMAND="xclip -selection clipboard -in -l 1"

xsel cannot limit paste requests, but can time out the selection (ms):
		export LPASS_CLIPBOARD_COMMAND="xsel -t 5000 --input --clipboard"
```
