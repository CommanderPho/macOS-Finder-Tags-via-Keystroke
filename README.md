# Assign macOS Finder Tags via Keystroke  
Use keyboard shortcuts to assign tags to items in macOS Finder.  
I have tried intermittently to enable this functionality since Mavericks, and was extremely happy to get this working last year.  I post this on the off chance that anyone else has an irrational need to have "keystroke = tag" capability.  

### Made possible by the "tag" command    
Portland's own [James Berry](https://github.com/jdberry) made a very useful command line tool (_[tag](https://github.com/jdberry/tag)_) that can, among other things, add/remove tags to/from Finder items.  

- It can add tags:  
	`tag -a YourTagHere`  

- It can remove tags:  
	`tag -r YourTagHere`

More in the _tag_ [README](https://github.com/jdberry/tag).  

### Automator workflow (saved as a Service)
The example Automator workflows I have included here are one way to trigger _tag_ to act on the selected finder items via keyboard shortcut. (This functionality is probably available using LaunchBar, Alfred, Keyboard Maestro, etc., but I wanted to assign tags via keyboard w/o needing any other apps running.)  


#### Running Shell Scripts from keyboard shortcuts  
The _tag_ command is used in a tiny Bash script. Note: The Automator action requires including the path to the command.

    for f in "$@"  
    do  
    /usr/local/bin/tag -a YourTagHere "$f"  
    done  

1. The Bash script is contained in an Automator action in a workflow  
2. The workflow is saved as a macOS Service  
3. A keyboard shortcut is assigned to the Service  

Note: Services can be assigned a keyboard shortcut in _System Preferences -> Keyboard -> Shortcuts -> Services._  

### Toggling a tag on or off (on an item)  
I currently toggle a "flag" tag in the most simple manner:  
1. "cmd-shift-L" ADDS the "flag" tag  
2. "cmd-opt-shift-L" REMOVES the "flag" tag.  

Further ideas: It could be useful in some circumstances to:
1. Read the state of the tag on the file  
2. Use a _single_ key command to toggle that state.  

### Note: Setting up _tag_ using homebrew in macOS terminal  
Requirements (from the [readme.md](https://github.com/jdberry/tag/blob/master/README.md))  
1. 10.9 Mavericks and above  
2. You must have Xcode or the Command Line Tools installed to build/install.  

Installation of _tag_  
1. Install [Homebrew](https://github.com/Homebrew/brew/) on your Mac.  
2. Install the _tag_ package via the command line.  
`brew install tag`  
