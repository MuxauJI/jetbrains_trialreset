# jetbrains_trialreset
For Windows
```
@echo off
for %%a in (PhpStorm WebStorm PyCharm Idea Rider Clion DataGrip RubyMine GoLand) do (
	for /d %%b in ("%USERPROFILE%\AppData\Roaming\JetBrains\*%%a*") do (
		rd /s /q "%%b\eval"
		copy /y %%b\options\other.xml %%b\options\other.xml.bak
		findstr /V "evlsprt" %%b\options\other.xml.bak > %%b\options\other.xml
	)
	reg delete "HKEY_CURRENT_USER\Software\JavaSoft\Prefs\jetbrains\%%a" /f
)
```
For Linux
```
#!/bin/bash
for v in PhpStorm WebStorm PyCharm Idea Rider Clion DataGrip RubyMine GoLand
do
	rm -rf ~/.config/JetBrains/*$v*/eval
	rm -rf ~/.java/.userPrefs/jetbrains/${v,,}
	sed -i '/evlsprt/d' ~/.config/JetBrains/*$v*/options/other.xml 2> /dev/null
done

```
