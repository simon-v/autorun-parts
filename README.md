# autorun-parts: A reverse task scheduler

`autorun-parts` is a crude, deficient, bug-ridden reimplementation of cron.

Well, not really. More accurately, it's a kind of "reverse task scheduler"; What it does is iterate through a directory with scripts and execute the ones that "want" to be executed. A script is considered "wanting" to be executed when the system time matches a cron-like schedule string inside the script. The syntax of the cron-string is as follows:

`#@ minute hour day month weekday`

Where all values are numeric (including `weekday`, which is the weekday number as printed by `date +%w`) and `#@` is a literal `#@`. A small subset of cron notation is supported: using `*` as "any" and passing several alternate field values in a comma-separated list.

After you have added the cron-string to your script files, have `autorun-parts` execute with your preferred scheduler, with the paths of your script directories as the arguments.

To indicate to `autorun-parts` that you are executing it less frequently than every minute and that some of the time marks in the cron-string should not be taken into account when deciding whether it is time to run a script, specify one of the following frequency flags as the first argument:

    -h    hourly (minutes are ignored)
    -d    daily (hours and minutes are ignored)
    -m    monthly (days, hours and minutes are ignored)

The `weekday` mark is always honored.
