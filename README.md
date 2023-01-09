There may be differences per port (board family), but I think this is generally how it shakes out. In both cases, code.py restarts, but onboard RTC is retained. I'll edit this post later if I find other differences.

supervisor.reload():
• alarm.sleep_memory is retained
• "equivalent to hitting Ctrl-D at the REPL)."

microcontroller.reset():
• executes boot.py before code.py
• pretty much like pressing the reset button
• alarm.sleep_memory is lost
• comes with a Warning:
This may result in file system corruption when connected to a host computer. Be very careful when calling this! Make sure the device “Safely removed” on Windows or “ejected” on Mac OSX and Linux.