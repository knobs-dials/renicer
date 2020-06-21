# renicer

Wrapper that eases renice+ionice. Reads from /proc, /etc/passwd.

Example use:

``` 
 # renicer -l relion

'relion_refine_m'  (PID 32439) matches
  running:   'ionice -n 7 -p 32439'
  running:   'renice -n 10 -p 32439'
32439 (process ID) old priority 0, new priority 10

'relion_refine_m'  (PID 32440) matches
  running:   'ionice -n 7 -p 32440'
  running:   'renice -n 10 -p 32440'
32440 (process ID) old priority 0, new priority 10

# usage 

```
Usage: renicer [options]

Options:
  -h, --help            show this help message and exit
  -n NICE, --nice=NICE  Niceness to set. Default is not to change. Example: 5
                        to set lower-than-average
  -i IONICE, --ionice=IONICE
                        Ioniceness to set within class. Default is not to
                        change. Range is 1 (higher priority) to 7 (lower), 4
                        being default on a process.
  -l, --lazy            For lazy typers: short for -n 10 -i 7  (overrides
                        -n/-i if also specified)
  -z, --zero            For lazy typers: short for -n 0 -i 0  (overrides -n/-i
                        if also specified). Useful to cancel out an earlier
                        -n/-i/-l
  -c IOCLASS, --ionice--class=IOCLASS
                        Ioniceness class to set. Best effort (default) is 2, 3
                        is for idle, 1 for realtime. WARNING: realtime steals
                        from everything, idle gets trampled over, so when only
                        looking to rebalance a bit, use only -i.
  -u USER, --user=USER  Restrict our selection to a specific specific user's
                        processes (exact username).
  -d, --dry-run         Just print what we would do, don't actually do it.
```
