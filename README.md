# xubuntu-alps-touchpad-toggle

This is a simple bash script to toggle the state of touchpad. Tested for  AlpsPS/2 ALPS DualPoint TouchPad.

The script :
------------------------------------------------------------------------------------------------------------
		killall notify-osd
		tpid=`xinput list | grep Alp | sed 's/.*id\=\([0-9]\+\).*/\1/g'`
		if [ $(xinput list-props $tpid | grep 'Device Enabled' | awk '{ print $4 }')  -eq 1 ]; then
			xinput disable $tpid  
			notify-send "Deactivated" --icon='touchpad-disabled-symbolic'

		else
			killall notify-osd
			xinput enable $tpid
			notify-send  "Activated" --icon='input-touchpad-symbolic'
		fi
		
	
For other touchpad devices, try replacing Apl in the second line with the name of the touchpad retrievable by entering `xinput` in the terminal.
Other input devices can also be enabled toggled by this process, by capturing correct output provided by `xinput list`. This will be functional but will require changing the icon for notification in `icon=NEW_ICON_NAME`.
For ease, add a keyboard shortcut and bind it to `bash filename`
