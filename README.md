# AppleScript-Install-Audio-Plugin
A simple AppleScript workflow to install audio plugins directly from Finder. Currently supports VST3, VST, AU, LV2 and CLAP.


<img width="637" alt="Screenshot 2023-03-09 at 12 39 35" src="https://user-images.githubusercontent.com/44585538/224012454-18a21915-e7d2-43eb-b84b-0f7ddd3f5330.png">


You can download a pre-built workflow from the release section, which you can install by clicking on it.


The script is as following:

```
on run {input, parameters}
	set pLoc to POSIX path of input as text
	set pLoc to text 1 thru -2 of pLoc
	set pLoc to quoted form of pLoc as string
	
	set thePath to input as text
	set saveTID to AppleScript's text item delimiters
	set AppleScript's text item delimiters to {"."}
	set theExt to last text item of thePath
	set AppleScript's text item delimiters to saveTID
	if theExt ends with ":" then set theExt to text 1 thru -2 of theExt
	
	if theExt is "component" then
		do shell script "sudo cp -rf " & pLoc & " /Library/Audio/Plug-Ins/Components" with administrator privileges
	else if theExt is "vst" then
		do shell script "sudo cp -rf " & pLoc & " /Library/Audio/Plug-Ins/VST" with administrator privileges
	else if theExt is "vst3" then
		do shell script "sudo cp -rf " & pLoc & " /Library/Audio/Plug-Ins/VST3" with administrator privileges
	else if theExt is "lv2" then
		do shell script "sudo cp -rf " & pLoc & " /Library/Audio/Plug-Ins/LV2" with administrator privileges
	else if theExt is "clap" then
		do shell script "sudo cp -rf " & pLoc & " /Library/Audio/Plug-Ins/CLAP" with administrator privileges
	else
		set errorMessage to "Not a audio plugin format:" & theExt
		display dialog errorMessage
	end if
end run
```
