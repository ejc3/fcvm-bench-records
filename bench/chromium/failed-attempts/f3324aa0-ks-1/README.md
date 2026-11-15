# Campaign f3324aa0, Kitesurf step, first attempt (not measured)

The step stopped at start-up: wrangler failed with
`EACCES: permission denied, mkdir '$HOME/.config/.wrangler'` (`step.log`,
`record/kitesurf/wrangler-logs/`). On that host `$HOME/.config` was owned by root,
read at 06:15 UTC with `ls -ld`:

    drwxr-xr-x 4 root   root   4096 Nov 15 05:39 $HOME/.config
    drwx------ 3 root   root   4096 Nov 15 05:39 $HOME/.config/chromium
    drwxrwxr-x 2 ubuntu ubuntu 4096 Nov 14 22:29 $HOME/.config/fcvm

`$HOME/.config/chromium/Crash Reports` (05:39) was made by the 2 vCPU scale run's
host-control Chromium, which ran as root with the user's HOME; its log's first line is
05:39:07 (`reqbench-f3324aa0-s2/scale-*/logs/host-control-chromium.log`). The owner of
`$HOME/.config` was restored and the step ran again at the same commit as `kitesurf-t2`,
imported as `corpusextra-f3324aa0-ks`. Fixed in ejc3/fcvm#1913.
