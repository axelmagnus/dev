There may be differences per port (board family), but I think this is generally how it shakes out. In both cases, code.py restarts, but onboard RTC is retained. I'll edit this post later if I find other differences.
```
supervisor.reload():
• "equivalent to hitting Ctrl-D at the REPL"
• alarm.sleep_memory is retained
• supervisor.get_previous_traceback() is not reset to None

microcontroller.reset():
• pretty much like pressing the reset button
• executes boot.py before code.py
• alarm.sleep_memory is lost
• supervisor.get_previous_traceback() is reset to None
```

• comes with a Warning:
This may result in file system corruption when connected to a host computer. Be very careful when calling this! Make sure the device “Safely removed” on Windows or “ejected” on Mac OSX and Linux.

there's also 
```
supervisor.get_previous_traceback()
```
 (after reload, not reset) https://docs.circuitpython.org/en/latest/shared-bindings/supervisor/index.html#supervisor.get_previous_traceback

there's 
```
supervisor.runtime.usb_connected #=True if connected
supervisor.runtime.serial_connected
```

https://docs.circuitpython.org/en/latest/shared-bindings/supervisor/index.html

web workflow 
[1:40 AM]
writing to file needs SD or some external storage if the host computer is also expecting to be able to edit files on CIRCUITPY, and switching back and forth to which can write requires a reset and running boot.py
[1:40 AM]
(nvm could work, but it's a good bit of data to pack)
[1:44 AM]
since it's a strong recommendation to use an editor that auto-flushes edits immediately, the microcontroller.reset() Warning is for those edge cases where you may be editing code while code is running and issuing a microcontroller.reset(), or perhaps something else on your host computer is pinging the CIRCUITPY disk (you may not know if auto-reload is off)
