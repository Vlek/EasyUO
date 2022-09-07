# EasyUO

## Table of Contents:




## Variables

### Types

All variables are dynamically typed and are of type string unless they are used
in specific situations where they are parsed as numbers or booleans.

### Declaration

### User-generated

### Built-in Variables

## Expressions

## Operators

## Control Structures

## Built-in Subroutines

### Miscellaneous:
#### display [ok | okcancel | yesno | yesnocancel] [message]

Displays a standard Windows messagebox with a set of buttons of your choice.

Note: Use `$` to create a new line.

<details>
  <summary>Example</summary
  
  ```
  display yesno You have run out of ingots. Do you want to end the script?
  if #disRes = yes
  {
  halt
  }
  ```
</details>

#### execute [filename] (argument...)

Executes an external command with the arguments given.

<details>
  <summary>Example 1</summary
  
  ```
  execute EasyUO.exe healthWatch.euo
  ```
</details>

<details>
  <summary>Example 2</summary
  
  ```
  execute cmd.exe /c echo gosub railtask move %task %guardzone #charPosX #charPosY #charPosZ %tileid >>rail.txt
  ```
</details>

#### linesPerCycle [linespercycle]

Sets the number of lines that the EasyUO parser runs through every cycle. The
default value is 10 and is reset when the main script is stopped.

20 cycles per second, 10 lines per cycle, or 200 lines per second is the
default.

From developer Cheffe:
```
"EUO has 20 cycles per second and in each cycle it executes 10 lines (default). Some commands have built in waits so that the script speed slows down considerably.

You can't say that one command is faster than the other. EUO gives away most of the available processing time so that the UO client can have it.

EUO doesn't know the difference between a processing intensive task such as "finditem *" at WBB or a simple "set %x 3". While 10 lines per cycle is already too fast if you have 10 finditems in a row you could execute hundreds of set instructions in the same time without stressing the CPU."

Read here: http://www.easyuo.com/forum/viewtopic.php?p=21269
```

<details>
  <summary>Example</summary
  
  ```
  linespercycle 10
  ```
</details>


#### set [! | % | * | #] [variableName] (expression) (abs)

Sets a variable to what an expression evaluates to. If the abs option is
specified, the absolute (mathimatically) value will be assigned. Omitting the
expression will set the variable to a blank string.

Scopes:
- namespace: !
- standard: %
- persistent: *
- system: #

<details>
  <summary>Example</summary
  
  ```
  set %a 2
  set %b $a ;we can use hexadecimal too
  set %c ( %a * %b ) + 1 ;%c is 21
  set %d %a * ( %b + 1 ) ;%d is 22
  set %e %a * %b + 1 ;%e is 21
  set %f ;set %f to a blank string
  set %varname 0 ;initializing a variable to 0
  halt
  ```
</details>

#### send [HTTPPost(port) | DebugHTTPPost(port)] [site] [path] [post data]

Sends an HTTP request to a web server and executes the code that is returned.

<details>
  <summary>Example</summary>
  
  ```
  ;******************************
  ; EUO Chat V1.0 by Cheffe
  ;******************************
  ;
  ; Allow send must be enabled!!!

  menu Clear
  menu Window Size 245 120
  menu Window Title EUO Chat V1.0
  menu Show 200 200
  menu HideEUO

  menu Text 1 20 20 Please enter your nickname:
  menu Font BGColor White
  menu Edit 2 20 40 200
  menu Font BGColor BtnFace
  menu Button 3 130 70 90 25 OK

  set #menuButton 0
  N1:
    if #menuButton = closed
      halt
    if #menuButton <> 3
  goto N1

  menu Get 2
  set %nickname #menuRes

  ;******************************

  menu Clear
  menu Window Size 500 230
  menu Font BGColor White
  menu Edit e1 20 180 360
  menu Font BGColor BtnFace
  menu Button b1 400 180 80 25 Send!

  set #menuButton 0
  N2:
    N3:
      if #scnt2 > 30
      {
        send HTTPPost www.easyuo.com /webscripts/euochat.pl R
        set #scnt2 0
      }

      if #menuButton = CLOSED
        halt

      if #menuButton <> b1
    goto N3
    set #menuButton 0

    menu Get e1
    send HTTPPost www.easyuo.com /webscripts/euochat.pl S %nickname , : #menuRes
    menu Activate e1

  goto N2
  ```
</details>

#### shutDown ["force"]

Shuts down the computer. With the force option given, will close even if some
applications are unresponsive.

<details>
  <summary>Example</summary>
  
  ```
  if #charGhost = YES
  {
  shutDown
  }
  ```
</details>

#### sound (filename)

Plays a wave file or the system default beep.

Relative paths are usable for directories within the user's PATH variable,
otherwise absolute paths are required.

<details>
  <summary>Example</summary>
  
  ```
  sound ; plays the default beep
  sound chimes.wav ; plays a default sound within PATH variable
  sound c:\windows\media\chimes.wav ; plays sound with absolute path.
  ```
</details>

#### str {Sub-command} [string] (Args)

Sub-commands:
- Len [string]
  - Stores the length of a string in the #strRes system variable.
  - <details>
      <summary>Example</summary>
      
      ```
      set %string HELLO
      str Len %string ; #strRes = 5
      ```
    </details>

- Pos [string] [sub-string] [index]
  - Stores the position of the sub-string in the #strRes system variable.
    `index` tells which occurence to return (if there's more than one).
- Left [string] [length]
  - Stores a part of the string taken from the left in #strRes
- Right [string] [length]
  - Stores a part of the string taken from the right in #strRes
- Mid [string] [start] [length]
  - Stores a part of the string taken from the middle in #strRes
- Lower [string]
  - Stores a lower-case version of the string in #strRes
- Ins [string] [sub-string] [start]
  - Inserts a string into the string and stores it in the #strRes variable
- Del [string] [start] [length]
  - Deletes a part of the string and stores it in the #strRes variable
- Count [string] [substring]
  - Returns the number of occurences of substring in string.



