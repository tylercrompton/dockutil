#dockutil

##Introduction

dockutil is a command line utility for managing Mac OS X dock items. It is written in Python and makes use of the plistlib module included in Mac OS X.

- Compatible with Mac OS X 10.4.x thru 10.9.x.
- Add, List, Move, Find, Remove Dock Items
- Supports Applications, Folders, Stacks, URLs. 
- Can act on a specific dock plist or every dock plist in a folder of home directories

##License

[Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0)

##Change Log

###Version 2.0.0

- Added Python 3 support. Now supports Python 2.6.0a2 and up.
- Adding an item that ends in "app" that is not an application now works.
- Various other bug fixes

###Version 1.1.4

- Restart cfprefsd before restarting Dock to ensure settings are read

###Version 1.1.3

- fix issue with missing labels and removals

###Version 1.1.2

- fix issue with replacing a url dock item
- add legacy support --hupdock option for backward compatibility
- fix paths with spaces when passing full path to plist


###Version 1.1

- fixes many issues with paths (should now work with Default User Template)
- adds option to not restart the dock (--no-restart)
- fixes issue where item would be added multiple times
(use --replacing to update an existing item)
- resolves deprecation warnings
- adds option to remove all items (--remove all)
- fix issue with removals when a url exists in a dock
- adds option --version to output version

##Usage

    $ dockutil -h
    $ dockutil --add (<path to item> | <url>)
        [--label <label>]
        [folder_options]
        [position]
        [plist_location_specification]
        [--no-restart]
    $ dockutil --remove (<dock item label> | all)
        [plist_location_specification]
        [--no-restart]
    $ dockutil --move <dock item label> position [plist_location_specification]
    $ dockutil --find <dock item label> [plist_location_specification]
    $ dockutil --list [plist_location_specification]
    $ dockutil --version

###folder_options

- `--view [grid | fan | list | automatic]`
- `--display [folder | stack]`
- `--sort [name | dateadded | datemodified | datecreated | kind]`

###position
- `--replacing <dock item label name>`
- `--position [index_number | beginning | end | middle]`
- `--after <dock item label name>`
- `--before <dock item label name>`
- `--section [apps | others]`

###plist_location_specifications

- <path to a specific plist>
- <path to a home directory>
- `--allhomes`
- `--homeloc`

##Examples

The following adds TextEdit to the end of the current user's dock:

    $ dockutil --add /Applications/TextEdit.app`

The following replaces Time Machine with TextEdit in the current user's dock:

    $ dockutil --add /Applications/TextEdit.app --replacing 'Time Machine'`

The following adds TextEdit after the item Time Machine in every user's dock on that machine:

    $ dockutil --add /Applications/TextEdit.app --after 'Time Machine' --allhomes`

The following adds `~/Downloads` as a grid stack displayed as a folder for every user's dock on that machine:

    $ dockutil --add '~/Downloads' --view grid --display folder --allhomes`

The following adds a url dock item after the Downloads dock item for every user's dock on that machine:

    $ dockutil --add vnc://miniserver.local --label 'Mini VNC' --after Downloads --allhomes`

The following removes System Preferences from every user's dock on that machine:

    $ dockutil --remove 'System Preferences' --allhomes`

The following moves System Preferences to the second slot on every user's dock on that machine:

    $ dockutil --move 'System Preferences' --position 2 --allhomes`

The following finds any instance of iTunes in the specified home directory's dock:

    $ dockutil --find iTunes /Users/jsmith`

The following lists all dock items for all home directories at homeloc in the form of `item<tab>path<tab><section>tab<plist>`:

    $ dockutil --list --homeloc /Volumes/RAID/Homes --allhomes`

The following adds Firefox after Safari in the Default User Template without restarting the Dock:

    $ dockutil --add /Applications/Firefox.app --after Safari --no-restart '/System/Library/User Template/English.lproj'`

##Notes

When specifying a relative path like `~/Documents` with the `--allhomes` option, `~/Documents` must be quoted like `'~/Documents'` to get the item relative to each home.

##Limitations and Dependencies

- Python 2.6.0a2+
- plistlib

##Bugs

Names containing special characters like accent marks will fail.

##Contact

Please send bug reports and comments to kcrwfrd at gmail.