---
layout: post
title:      "Javascript Scripting in Photoshop! "
date:       2021-03-14 23:32:57 +0000
permalink:  javascript_scripting_in_photoshop
---

![](https://media.giphy.com/media/LmNwrBhejkK9EFP504/giphy.gif)


Hidden Photoshop Script EASILY Creates Random Fills!

https://www.youtube.com/watch?v=BFxeIJZGUSg&list=PLEFkCJHu8Yx22ewMe9ueIb3cXhSf6T5-x&index=12

Photoshop supports external automation through scripting. In Windows, you can use scripting languages that support COM automation, such as VB Script. In Mac OS, you can use languages such as AppleScript that allow you to send Apple events. These languages are not cross-platform but can control multiple applications such as Adobe Photoshop, Adobe Illustrator, and Microsoft Office. In Mac OS, you can also use Apple’s Photoshop Actions for Automator to control tasks in Photoshop.

****You can also use JavaScript on either platform. JavaScript support lets you write Photoshop scripts that run on either Windows or Mac OS.

Note:

Refer to the scripting documentation installed in the Photoshop CS5/Scripting/Documents folder and also here. The Scriptlistener Plug-In can be found in Photoshop CS5/Scripting/Utilities and is also available here.

**Run a JavaScript
**Choose File > Scripts and then select the script from the list. The scripts list includes all the script files saved with a .js or .jsx extension and saved in the Photoshop CS5/Presets/Scripts folder. To run a script saved in another location, choose File > Scripts > Browse and navigate to the script.
Set scripts and actions to run automatically
You can have an event, such as opening, saving, or exporting a file in Photoshop, trigger a JavaScript or a Photoshop action. Photoshop provides several default events, or you can have any scriptable Photoshop event trigger the script or action. See the Photoshop Scripting Guide for more information on scriptable events.

Choose File > Scripts > Script Events Manager.
Select Enable Events To Run Scripts/Actions.
From the Photoshop Event menu, choose the event that will trigger the script or action.
Select either Script or Action, and then choose the script or action to run when the event occurs.
Photoshop has several sample scripts you can choose. To run a different script, choose Browse and then navigate to the script. For actions, choose the action set from the first pop-up menu and an action from that set in the second menu. The action must be loaded in the Actions panel to appear in these menus.

Click Add. The event and its associated script or action are listed in the dialog box.
To disable and remove individual events, select the event in the list and click Remove. To disable all events, but keep them in the list, deselect Enable Events To Run Scripts/Actions.

