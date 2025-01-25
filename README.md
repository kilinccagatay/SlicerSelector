3D Printing Slicer Selector for macOS

This is a simple AppleScript that allows you to choose your preferred slicer (e.g., Bambu Studio, PrusaSlicer, OrcaSlicer, or Creality Print) when opening .3mf or .stl files on macOS. Instead of manually opening slicer applications, this script provides a convenient way to select the slicer at the time of file opening.

Features

Custom Slicer Selection: Choose from a list of slicers when opening 3MF or STL files.
Easy to Customize: Modify the script to include additional slicers or change the default selection.
Streamlined Workflow: No need to open slicers manually—save time and stay organized.
How It Works

Install the Script: Save the script as an application using Script Editor on macOS.
Open Your Files: When you double-click a .3mf or .stl file, the script will prompt you to choose a slicer from a predefined list.
Seamless Execution: The selected slicer automatically opens with your chosen file.
Setup Instructions

## Step 1: Open Script Editor
Open **Script Editor** on your Mac.
Copy and paste the code below into a new document:

```applescript
on open (theFiles)
    set slicerList to {"BambuStudio", "Creality Print", "OrcaSlicer", "PrusaSlicer"}
    set chosenSlicer to choose from list slicerList with prompt "Select a slicer to open the 3MF file:" default items {"BambuStudio"}
    
    if chosenSlicer is false then
        return
    else
        set chosenSlicer to item 1 of chosenSlicer
        set slicerPaths to {¬
            {"OrcaSlicer", "/Applications/OrcaSlicer.app"}, ¬
            {"PrusaSlicer", "/Applications/Original Prusa Drivers/PrusaSlicer.app"}, ¬
            {"BambuStudio", "/Applications/BambuStudio.app"}, ¬
            {"Creality Print", "/Applications/Creality Print.app"}}
        
        set slicerApp to ""
        repeat with slicer in slicerPaths
            if item 1 of slicer is chosenSlicer then
                set slicerApp to item 2 of slicer
                exit repeat
            end if
        end repeat
        
        if slicerApp is not "" then
            repeat with fileToOpen in theFiles
                do shell script "open -a " & quoted form of slicerApp & " " & quoted form of POSIX path of fileToOpen
            end repeat
        else
            display dialog "No matching slicer found." buttons {"OK"}
        end if
    end if
end open
```


## Step 2: Save as Application
Go to **File > Export** in Script Editor.
Set the format to Application.
Save the application to your Applications folder.

## Step 3: Associate File Types
Right-click any `.3mf` or `.stl` file and select Get Info.
In the "Open with" section, select your saved application.
Click Change All to apply the setting to all files of the same type.
Customization

You can modify the slicerList and slicerPaths in the code to:

Add new slicers by including their names and file paths.
Change the default slicer by updating the default items list.


Example

When you open a .3mf or .stl file, you’ll see a prompt like this:

<img width="358" alt="image" src="https://github.com/user-attachments/assets/126beea4-b458-4049-a876-98899e12b7f6" />

Choose a slicer, and it will automatically open the file in the selected application.

Important Notes

Ensure that the paths to your slicer applications are correct.
Every character in the script is crucial—double-check for typos if something doesn’t work.
If you encounter issues, feel free to open an issue on this repository or ask for help.
License

This project is licensed under the MIT License. Feel free to use, modify, and share it.

