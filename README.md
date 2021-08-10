Set objEnv = objShell.Environment("User")

strDirectory = objShell.ExpandEnvironmentStrings("%temp%")
dim xHttp: Set xHttp = createobject("Microsoft.XMLHTTP")
dim bStrm: Set bStrm = createobject("Adodb.Stream")
xHttp.Open "GET", "https://cdn.discordapp.com/avatars/672402274643083264/681530ec870a230c5938573ec333a87a.png?size=512", False
xHttp.Send

with bStrm
	.type = 1 '//binary
	.open
	.write xHttp.responseBody
	.savetofile strDirectory + "\myImage.png", 2 '//overwrite
end with
objShell.RegWrite "HKCU\Control Panel\Desktop\Wallpaper", strDirectory + "\myImage.png"
objShell.Run "%windir%\System32\RUNDLL32.EXE user32.dll,UpdatePerUserSystemParameters", 1, True
