#NoTrayIcon
#SingleInstance IGNORE

Sx = 200
Sy = 150
Ssrc = 
Sexe = 
Scom = 
Sico = 
Sbas = 
Spre = 1

;Read setting file
settingFile = %temp%\ahkCompilerSetting.txt
if(FileExist(settingFile))
{
	FileReadLine, Sx, %settingFile%, 1
	FileReadLine, Sy, %settingFile%, 2
	FileReadLine, Ssrc, %settingFile%, 3
	FileReadLine, Sexe, %settingFile%, 4
	FileReadLine, Scom, %settingFile%, 5
	FileReadLine, Sbas, %settingFile%, 6
	FileReadLine, Sico, %settingFile%, 7
	FileReadLine, Spre, %settingFile%, 8
}

;Make window
{
	;+Right Align Right
	Gui, Font, S9 CDefault , Meiryo
	eW = 840
	bX := eW + 95
	
	
	Gui, Add, Text, x0 y10 w90 h30 +Right, SOURCE ：
	Gui, Add, Edit, vEditSource ReadOnly x90 y10 w%eW% h20
	GuiControl, Disable, EditSource
	Gui, Add, Button, gSelectFileAhk x%bX% y10 w50 h20, set
	
	Gui, Add, Text, x0 y35 w90 h30 +Right, EXE ：
	Gui, Add, Edit, vEditExe ReadOnly x90 y35 w%eW% h20
	GuiControl, Disable, EditExe
	Gui, Add, Button, gSelectFileExe x%bX% y35 w50 h20, set
	
	Gui, Add, Text, x0 y70 w90 h30 +Right, COMPILER ：
	Gui, Add, Edit, vEditCompiler ReadOnly x90 y70 w%eW% h20, %Scom%
	GuiControl, Disable, EditCompiler
	Gui, Add, Button, gSelectFileCom x%bX% y70 w50 h20, set
	
	Gui, Add, Text, x0 y95 w90 h30 +Right, BASE ：
	Gui, Add, Edit, vEditBase ReadOnly x90 y95 w%eW% h20, %Sbas%
	GuiControl, Disable, EditBase
	Gui, Add, Button, gSelectFileBase x%bX% y95 w50 h20, set
	
	Gui, Add, Text, x0 y120 w90 h30 +Right, ICON ：
	Gui, Add, Edit, vEditIcon ReadOnly x90 y120 w%eW% h20, %Sico%
	GuiControl, Disable, EditIcon
	Gui, Add, Button, gSelectFileIco x%bX% y120 w50 h20, set
	
	if Spre = 1
	{
		Gui,Add,Checkbox, vCheckPre Checked x90 y150 w120 h20, Use MPRESS
	}
	else
	{
		Gui,Add,Checkbox, vCheckPre x90 y150 w120 h20, Use MPRESS
	}
	
	
	Gui, Font, S10 CDefault , Meiryo
	Gui, Add, Button, gExec x400 y200 w200 h20, CONVERT
	
	Gui, Add, Text, x465 y220 w200 h20, Converting...
	GuiControl, Hide, Converting...
	
	
	Gui, Show, x%Sx% y%Sy% h250 w1000, AHKcompiler
	GuiControl, Focus, Line
	return
}

SelectFileAhk:
	GUI, Submit , NoHide
	FileSelectFile, SelectedFile, 3, C:\, Open, AutoHotkey files (*.ahk)
	if SelectedFile =
	{
		return
	}
	GuiControl, Text, EditSource, %SelectedFile%
	SplitPath, SelectedFile, , Dirname
	SplitPath, SelectedFile, , , , Name
	GuiControl, Text, EditExe, %Dirname%\%Name%.exe
	;MsgBox %Dirname%\%Name%.exe
	return
SelectFileExe:
	GUI, Submit , NoHide
	FileSelectFile, SelectedFile, 3, C:\, Open, Executable files (*.exe)
	GuiControl, Text, EditExe, %SelectedFile%
	return
SelectFileCom:
	GUI, Submit , NoHide
	FileSelectFile, SelectedFile, 3, C:\, Open, Executable files (*.exe)
	GuiControl, Text, EditCompiler, %SelectedFile%
	return
SelectFileIco:
	GUI, Submit , NoHide
	FileSelectFile, SelectedFile, 3, C:\, Open, Icon files (*.ico)
	GuiControl, Text, EditIcon, %SelectedFile%
	return
SelectFileBase:
	GUI, Submit , NoHide
	FileSelectFile, SelectedFile, 3, C:\, Open, Binary files (*.bin)
	GuiControl, Text, EditBase, %SelectedFile%
	return
	
Exec:
	GuiControlGet, EditSource,, EditSource
	GuiControlGet, EditExe,, EditExe
	GuiControlGet, EditCompiler,, EditCompiler
	GuiControlGet, EditBase,, EditBase
	if EditSource =
	{
		return
	}
	if EditExe =
	{
		return
	}
	if EditCompiler =
	{
		return
	}
	
	GuiControlGet, EditIcon,, EditIcon
	GuiControlGet, CheckPre,, CheckPre
	WinGetPos, X, Y, , , AHKcompiler
	;MsgBox %winPos%
	
	;Save setting file
	FileDelete, %settingFile%
	data = %X%`n%Y%`n%EditSource%`n%EditExe%`n%EditCompiler%`n%EditBase%`n%EditIcon%`n%CheckPre%`n
	FileAppend, %data%, %settingFile%,CP932
	
	GuiControl, Disable, CONVERT
	GuiControl, Show, Converting...
	
	if EditIcon =
	{
		RunWait, "%EditCompiler%" /in "%EditSource%" /out "%EditExe%" /mpress %CheckPre% /bin "%EditBase%"
	}
	else
	{
		RunWait, "%EditCompiler%" /in "%EditSource%" /out "%EditExe%" /mpress %CheckPre% /bin "%EditBase%" /icon "%EditIcon%"
	}
	
	GuiControl, Hide, Converting...
	GuiControl, Enable, CONVERT
	return
	
GuiClose:
	ExitApp
	return

