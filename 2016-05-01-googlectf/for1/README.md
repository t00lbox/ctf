## For1 (Forensics, 100 points)
	tl;dr Find mspaint.exe in memory, inspect it as raw data in gimp

We're presented with a Win10x64 memory dump, let's start by inspecting current processes using volatility:

`volatility --profile Win10x64 -f dump1.raw pslist`.

There are 2 particularly interesting lines:

```
Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start
mspaint.exe            4092   2336      3        0      1      0 2016-04-04 16:13:21 
notepad.exe            2012   2336      1        0      1      0 2016-04-04 16:14:49                        
```

Both of these programs look like a good place to hide the flag. However, we should've gotten the text from notepad using strings, so we'll start with paint.

`volatility -f dump1.raw memdump -p 4092 --dump-dir=dump`

Produces a 1.8GB file, not very helpful...

It turns out that gimp handles raw data pretty well, we can select size, algorithm and offset.

We started tweaking those values to get a meaningful image. 

After some fun we're surprised with:

![alt](scr1.png)

