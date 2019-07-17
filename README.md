# QuitAllApps
Applescript for quit all apps
#
--by Ael
display dialog "Quit all applications" buttons {"Cancel", "OK"} default button {"OK"}
if button returned of result = "OK" then
	do shell script "cd `getconf DARWIN_USER_DIR`
rm -rf com.apple.notificationcenter
killall usernoted; killall NotificationCenter"
	tell application "System Events"
		set theVisibleApps to (name of application processes where visible is true)
	end tell
	repeat with thisApp in theVisibleApps
		try
			tell application thisApp
				try
					quit every document
					quit every window
				on error
					killall
				end try
			end tell
		end try
	end repeat
end if
