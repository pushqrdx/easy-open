<p align="center">
  <img width="710" height="454" src="Media/Screenie.png?raw=true"></img>
</p>

## Easy Open - a MacOS Finder Utility

Easy Open is an Automator workflow that makes it easy to open current `Finder` directory in your favorite tool, currently supporting `Terminal` and `Visual Studio Code` but is easily customizable.

## How to use:

- Pull this repository anywhere on your disk.
- Double click `Easy Open.workflow`, it will ask whether you want to install, click install.
- Assign a keyboard shortcut in `System Preferences > Keyboard > Shortcuts > Services > General` for easy access.
- Open a folder in finder, hit the shortcut, choose an app and hit enter.

## Notes:

- After you specify the application to launch, the script will grap the directory path from the _top most_ `Finder` window and pass it as an argument to the destination app. 
This behavior can be easily modified. Just right click the `Easy Open` entry where you assigned the shortcut and hit `Open in Automator`, there you'll find the apple script for this utility and can easily edit it to suit your own workflow.

- To add more applications or change the default app, look for this line and modify it as you wish. eg: changing Terminal to iTerm.
    ```as
    set SelectedApplication to (choose from list {"Terminal", "Visual Studio Code"} with prompt "Please make your selection" default items {"Terminal"}) as string
    ```

- To disable the select dialog replace the script with this one: 
    ```as
    tell application "Finder"
        if not (exists window 1) then
            return beep
        end if
        
        set WorkingDirectory to POSIX path of ((target of front Finder window) as text)
        
        if WorkingDirectory is not equal to "" then
            do shell script "open -a Terminal " & quoted form of WorkingDirectory
        end if
    end tell
    ```
