## AppleScript examples for [Bloom](https://bloomapp.club)

#### Frontmost window

```applescript
tell application "Bloom"
	-- Get the name of the frontmost window
	set windowName to name of front window

	-- Get the currently selected items in the frontmost window
	set windowSelection to selection of front window

	-- Get the current directory of the frontmost window
	set windowRootURL to rootURL of front window	
end tell
```

#### Windows
```applescript
tell application "Bloom"
	-- Get all open windows
	set windowList to windows

	-- Iterate through each window and access its properties
	repeat with windowItem in windowList
		set windowName to name of windowItem
		set windowSelection to selection of windowItem
		set windowURL to rootURL of windowItem
	end repeat
end tell
```

#### Tabs

```applescript
tell application "Bloom"
	-- Get all tabs in the frontmost window
	set windowTabs to tabs of front window

	-- Tabs are basically windows, so they have the same properties as windows
	repeat with windowTab in windowTabs
		set tabName to name of windowTab
		set tabURL to rootURL of windowTab
		set tabSelection to selection of windowTab
	end repeat
end tell
```

#### Panes

```applescript
tell application "Bloom"
	-- Get all panes in the frontmost window
	set thePanes to panes of front window

	repeat with thePane in thePanes
		-- Get the name of the pane
		set paneName to name of thePane

		-- Get the root URL (directory path) of the pane
		set paneURL to rootURL of thePane

		-- Get the currently selected items in the pane
		set paneSelection to selection of thePane
	end repeat
end tell	
```

#### Open folders

```applescript
tell application "Bloom"
	set desktopPath to POSIX path of (path to desktop folder)
	-- Find the pane that has already opened this folder, or open the folder in a new window
	open URL "file://" & desktopPath
end tell
```

#### Open folders in specific windows

```applescript
tell application "Bloom"
	set desktopPath to POSIX path of (path to desktop folder)
	-- Open the folder in the frontmost window
	set rootURL of front window to desktopPath

	-- Open the folder in the first tab of the frontmost window
	set rootURL of tab 1 of front window to desktopPath
	
	-- Absolute paths are also supported
	set rootURL of front window to "/Users/xxx/Desktop/"
end tell
```

#### Create new windows/tabs

```applescript
tell application "Bloom"
	-- Create a new window or tab using the default workspace
	make new window
	make new tab

	-- Create a new window and open a specific folder
	make new window with url "/Users/xxx/Downloads/"
	
	-- Create a new tab and open a specific folder
	make new tab with url "/Users/xxx/Library"

	-- Create a new window with workspaces
	make new window with workspace "Default Workspace"

	-- Create a new tab with workspaces
	make new window with workspace "Default Workspace"
end tell
```

#### Manage workspaces

```applescript
tell application "Bloom"
	-- Create new workspaces. The possible values for layout are single, l1r1, t1b1, l1m1r1, t1m1b1, h4x1, v4x1, l1r2, l2r1, t1b2, t2b1, g2x2.
	make new workspace using name "New Workspace" with layout "l1r1" with urls {"/Users/xxx/Documents", "/Users/xxx/Movies"}
	-- Remove workspace
	remove workspace "Workspace Name"
	-- Duplicate a workspace
	duplicate workspace "Workspace" with name "New Workspace"
end tell
```

#### Select files

```applescript
tell application "Bloom"
	-- Select files in the frontmost window
	tell front window to select files {"/path_to_the_file"}

	-- Select files in tabs
	tell tab 2 of front window to select files {"/path_to_the_file"}

	-- Select files in panes(not supported yet)
	tell pane 2 of tab 2 of front window to select files {"/path_to_the_file_1", "/path_to_the_file_2"}
end tell
```

