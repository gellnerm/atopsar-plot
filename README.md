# Atopsar-Plot

This is a mirror of the original repository at https://codeberg.org/mgellner/atopsar-plot/

Graphically represent the system resource consumption like CPU, disk, swap and network usage in a terminal.

```
$ atopsar-plot --day 0 --disk sda --iface 0s31f6

                       %CPU_idle                  
      ┌──────────────────────────────────────────┐
1586.0┤▄▄▄█████▄▄▄▖       ▖   ▐█▄▄▄▄▄▄█▟█▙▄▄▄▄▄▄▄│
1532.0┤████████████▙▄▄▄▄▄▟█▖  ▟██████████████████│
1478.0┤█████████████████████▖▗███████████████████│
1424.0┤█████████████████████▙████████████████████│
      └┬────────┬────────┬──────────┬───────────┬┘
       09:57  10:37    11:07      12:07     13:07 

                      %DSK_busy                   
    ┌────────────────────────────────────────────┐
36.0┤                      ▟▄                    │
24.0┤                     ▟██▌                   │
12.0┤▄▄                  ▗████                   │
 0.0┤█████▄▄▄▄▄▄▄▄▄▄▄▄▟█▄█████████▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│
    └┬────────┬────────┬──────┬──────┬──────────┬┘
     09:57  10:27    11:07  11:57  12:17    13:07 

                      MB_SWP_free                 
      ┌──────────────────────────────────────────┐
8192.0┤████████████████████▙▄▄                   │
8186.7┤███████████████████████▙▖                 │
8181.3┤██████████████████████████▄▄              │
8176.0┤█████████████████████████████▙▄▄▄▄▄▄▄▄▄▄▄▄│
      └┬────────┬────────┬──────────┬───────────┬┘
       09:57  10:37    11:07      12:07     13:07 

                      NET_iMbps                   
    ┌────────────────────────────────────────────┐
73.0┤                     ▄█                     │
48.7┤                    ▗██▖                    │
24.3┤                    ▐██▌                    │
 0.0┤▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄█████████▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄│
    └┬────────┬────────┬──────┬──────┬──────────┬┘
     09:57  10:27    11:07  11:57  12:17    13:07 

                      NET_oMbps                   
     ┌───────────────────────────────────────────┐
151.0┤                             ▗▟            │
100.7┤                           ▗▟██▖           │
 50.3┤                          ▄████▌           │
  0.0┤▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄▄███████▄▄▄▄▄▄▄▄▄▄▄│
     └┬─────────┬───────┬───────────┬───────────┬┘
      09:57   10:37   11:07       12:07     13:07 
```

## Features

ATOPSAR-PLOT allows graphing various historic system information directly in the terminal. It is based on logs written 
by [atop](https://github.com/Atoptool/atop). The following information can be plotted:

* %CPU_idle: CPU idle time in percent
* %DSK_busy: Disk activity in percent (see --disk flag)
* MB_SWP_free: Megabytes of free swap space
* NET_iMbps: Megabits per second of incoming network traffic (see --iface flag)
* NET_oMbps: Megabits per second of outgoing network traffic (see --iface flag)

Plots for previous days can be plotted with the parameter --day -1, --day -2, ...

### Resource usage alerts

Resource usage alerts can be sent by specifying an --alert-mail. For this to work, the package mailx must be installed
and configured to allow sending mails. You may create a cron job for alerts. Keep in mind that atop averages resource
consumption over the whole time granularity (default is 10 minutes). With the default --alert-threshold (30) an alert
will be generated if any of the monitored resources exceeds 70% of its maximum capacity.

    # crontab -e
    */10 * * * * /path/to/atopsar-plot --alert-mail alert@example.com

## Installing

### Install atop

Download and install [atop](https://www.atoptool.nl/downloadatop.php) and netatop on a debian based system

    sudo apt install zlib1g-dev zlib1g libncurses5-dev
    wget https://www.atoptool.nl/download/netatop-3.1.tar.gz
    tar -xzf netatop*.gz
    cd netatop*/
    make -j4
    sudo make install
    sudo systemctl start netatop
    sudo systemctl enable netatop
    cd ..
    git clone https://github.com/Atoptool/atop
    cd atop
    make -j4
    sudo make install

### Install atopsar-plot and PIP dependencies

    pip install -U plotext
    pip install -U git+https://codeberg.org/mgellner/atopsar-plot

## Contributing

When contributing to this repository, please first discuss the change you wish to make via issue

## License

This project is licensed under the Apache-2.0 License - see the [LICENSE](LICENSE) file for details

## Contact

See [https://www.miaplan.de/](https://www.miaplan.de/)

## Similar projects

* [https://github.com/fnep/aplot](https://github.com/fnep/aplot)
* [https://github.com/shuyufu/atop-plot](https://github.com/shuyufu/atop-plot)
