Name
====

lua-resty-signal - Lua library for killing or sending signals to Linux processes

Table of Contents
=================

* [Name](#name)
* [Synopsis](#synopsis)
* [Functions](#functions)
    * [kill](#kill)
    * [signum](#signum)
* [Author](#author)
* [Copyright & Licenses](#copyright--licenses)

Synopsis
========

```lua
local resty_signal = require "resty.signal"
local pid = 12345

local ok, err = resty_signal.kill(pid, "TERM")
if not ok then
    ngx.log(ngx.ERR, "failed to kill process of pid ", pid, ": ", err)
    return
end

-- send the signal 0 to check the existence of a process
local ok, err = resty_signal.kill(pid, "NONE")

local ok, err = resty_signal.kill(pid, "HUP")

local ok, err = resty_signal.kill(pid, "KILL")
```

Functions
=========

kill
----

**syntax:** `ok, err = resty_signal.kill(pid, signal_name_or_num)`

Sends a signal with its name string or number value to the process of the
specified pid.

All signal names accepted by [signum](#signum) are supported, like `HUP`,
`KILL`, and `TERM`.

Signal numbers are also supported when specifying nonportable system-specific
signals is desired.

[Back to TOC](#table-of-contents)

signum
------

**syntax:** `num = resty_signal.signum(sig_name)`

Maps the signal name specified to the system-specific signal number. Returns
`nil` if the signal name is not known.

All the POSIX and BSD signal names are supported:

```
HUP
INT
QUIT
ILL
TRAP
ABRT
BUS
FPE
KILL
USR1
SEGV
USR2
PIPE
ALRM
TERM
CHLD
CONT
STOP
TSTP
TTIN
TTOU
URG
XCPU
XFSZ
VTALRM
PROF
WINCH
IO
PWR
EMT
SYS
INFO
```

The special signal name `NONE` is also supported, which is mapped to zero (0).

[Back to TOC](#table-of-contents)


