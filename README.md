# csharpcmd
C#( or, actually, any .NET) cmd file header

Allows to create Windows .cmd from any runable c# file. When started, will compile , run and then delete executable file.

Very similar thing could be found on internet - it is there for a pretty long time. Advantage of this one is that it looks for most recent csc compiler in registry, whichever it is, instead of going through list of predefined  .NET versions.

Example:   
anyreasonablename.cmd

```cmd
/*
@echo off && cls
set NetReg=reg query "HKLM\SOFTWARE\Microsoft\NET Framework Setup\NDP" /s
for /f "tokens=2,3*" %%i in ('%NetReg% ^| find "InstallPath"')  do Set csc=%%j
if "%csc%" == ""   (
echo No .NET path found.  Compilation Failed.
goto:eof )

set csc="%_NetInstallPath:~0,-1%\csc.exe"
%csc% /nologo /out:"%~0.exe" %0
"%~0.exe" %1
del "%~0.exe"
exit
*/
```
```c#
using System;

namespace Test
{
  class TestClass
  {
    static void Main(string[] args)
    {
      if (args.Length == 1)
        Console.WriteLine("Done.Xo-xo-xo.");
      else
        Console.WriteLine("Done.Run it again.");
    }
  }
}
```
