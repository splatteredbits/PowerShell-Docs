---
title: PowerShell.exe Command-Line Help
ms.custom: na
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1ab7b93b-6785-42c6-a1c9-35ff686a958f
---
# PowerShell.exe Command-Line Help
Starts a Windows PowerShell session. You can use PowerShell.exe to start a Windows PowerShell session from the command line of another tool, such as Cmd.exe, or use it at the Windows PowerShell command line to start a new session. Use the parameters to customize the session.

## Syntax

```
PowerShell[.exe]
       [-EncodedCommand <Base64EncodedCommand>]
       [-ExecutionPolicy <ExecutionPolicy>]
       [-InputFormat {Text | XML}] 
       [-Mta]
       [-NoExit]
       [-NoLogo]
       [-NonInteractive] 
       [-NoProfile] 
       [-OutputFormat {Text | XML}] 
       [-PSConsoleFile <FilePath> | -Version <Windows PowerShell version>]
       [-Sta]
       [-WindowStyle <style>]
       [-File <FilePath> [<Args>]]
       [-Command { - | <script-block> [-args <arg-array>]
                     | <string> [<CommandParameters>] } ]

PowerShell[.exe] -Help | -? | /?
```

## Parameters

### \-EncodedCommand <Base64EncodedCommand>
Accepts a base\-64\-encoded string version of a command. Use this parameter to submit commands to Windows PowerShell that require complex quotation marks or curly braces.

### \-ExecutionPolicy <ExecutionPolicy>
Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable. This parameter does not change the Windows PowerShell execution policy that is set in the registry. For information about Windows PowerShell execution policies, including a list of valid values, see about\_Execution\_Policies (http:\/\/go.microsoft.com\/fwlink\/?LinkID\=135170).

### \-File <FilePath> \[<Parameters>]
Runs the specified script in the local scope ("dot\-sourced"), so that the functions and variables that the script creates are available in the current session. Enter the script file path and any parameters. **File** must be the last parameter in the command, because all characters typed after the **File** parameter name are interpreted as the script file path followed by the script parameters and their values.

You can include the parameters of a script, and parameter values, in the value of the **File** parameter. For example: `-File .\Get-Script.ps1 -Domain Central`

Typically, the switch parameters of a script are either included or omitted. For example, the following command uses the **All** parameter of the Get\-Script.ps1 script file: `-File .\Get-Script.ps1 -All`

In rare cases, you might need to provide a Boolean value for a switch parameter. To provide a Boolean value for a switch parameter in the value of the **File** parameter, enclose the parameter name and value in curly braces, such as the following: `-File .\Get-Script.ps1 {-All:$False}`

### \-InputFormat {Text | XML}
Describes the format of data sent to Windows PowerShell. Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).

### \-Mta
Starts Windows PowerShell using a multi\-threaded apartment. [!INCLUDE[ps_sdk_paramintrodps3](../Token/ps_sdk_paramintrodps3_md.md)] In [!INCLUDE[psversion3](../Token/psversion3_md.md)], single\-threaded apartment (STA) is the default. In [!INCLUDE[psversion2](../Token/psversion2_md.md)], multi\-threaded apartment (MTA) is the default.

### \-NoExit
Does not exit after running startup commands.

### \-NoLogo
Hides the copyright banner at startup.

### \-NonInteractive
Does not present an interactive prompt to the user.

### \-NoProfile
Does not load the Windows PowerShell profile.

### \-OutputFormat {Text | XML}
Determines how output from Windows PowerShell is formatted. Valid values are "Text" (text strings) or "XML" (serialized CLIXML format).

### \-PSConsoleFile <FilePath>
Loads the specified Windows PowerShell console file. Enter the path and name of the console file. To create a console file, use the [Export-Console](assetId:///4bab1c02-9e61-4aaf-9957-11d1934ef4ef) cmdlet in Windows PowerShell.

### \-Sta
Starts Windows PowerShell using a single\-threaded apartment. In [!INCLUDE[psversion3](../Token/psversion3_md.md)], single\-threaded apartment (STA) is the default. In [!INCLUDE[psversion2](../Token/psversion2_md.md)], multi\-threaded apartment (MTA) is the default.

### \-Version <Windows PowerShell Version>
Starts the specified version of Windows PowerShell. The version that you specify must be installed on the system. If [!INCLUDE[psversion3](../Token/psversion3_md.md)] is installed on the computer, valid values are "2.0" and "3.0". The default value is "3.0".

If [!INCLUDE[psversion3](../Token/psversion3_md.md)] is not installed, the only valid value is "2.0". Other values are ignored.

For more information, see "Installing Windows PowerShell" in the [Getting Started with Windows PowerShell [OLD MSDN]](assetId:///69555d95-b481-43e1-86e7-b46d68b3e2dd).

### \-WindowStyle <Window style>
Sets the window style for the session. Valid values are Normal, Minimized, Maximized and Hidden.

### \-Command
Executes the specified commands (and any parameters) as though they were typed at the Windows PowerShell command prompt, and then exits, unless the NoExit parameter is specified.

The value of Command can be "\-", a string. or a script block. If the value of Command is "\-", the command text is read from standard input.

Script blocks must be enclosed in braces ({}). You can specify a script block only when running PowerShell.exe in Windows PowerShell. The results of the script are returned to the parent shell as deserialized XML objects, not live objects.

If the value of Command is a string, **Command** must be the last parameter in the command , because any characters typed after the command are interpreted as the command arguments.

To write a string that runs a Windows PowerShell command, use the format:

```
"& {<command>}"
```

where the quotation marks indicate a string and the invoke operator (&) causes the command to be executed.

### \-Help, \-?, \/?
Shows this message. If you are typing a PowerShell.exe command in Windows PowerShell, prepend the command parameters with a hyphen (\-), not a forward slash (\/). You can use either a hyphen or forward slash in Cmd.exe.

> [!NOTE]
> Troubleshooting Note: In Windows PowerShell 2.0, starting some programs in the Windows PowerShell console fails with a LastExitCode of 0xc0000142.

## EXAMPLES

```
PowerShell -PSConsoleFile sqlsnapin.psc1

PowerShell -Version 2.0 -NoLogo -InputFormat text -OutputFormat XML

PowerShell -Command {Get-EventLog -LogName security}

PowerShell -Command "& {Get-EventLog -LogName security}"

# To use the -EncodedCommand parameter:
$command = "dir 'c:\program files' "
$bytes = [System.Text.Encoding]::Unicode.GetBytes($command)
$encodedCommand = [Convert]::ToBase64String($bytes)
powershell.exe -encodedCommand $encodedCommand
```

