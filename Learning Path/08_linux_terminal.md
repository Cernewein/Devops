# Classic linux terminal utilities

## Process monitoring
In Linux each process is identified by a unique number caller a process ID (PID). This number is unique and is automatically assigned when a process is created in the system. The most common commands used for process monitoring are:

### ps

The ps utility displays a snapshot of the current running processes. All processes can be displayed using:

```bash
ps aux
```

### top
This utility periodically displays a sorted list of system processes. The default sorting key is PID but it can be sorted differently as well. For example using shift + m sorts by memory usage. See this [cheat sheet](https://gist.github.com/ericandrewlewis/4983670c508b2f6b181703df43438c37) for details on how it can be used.

### htop
htop is very similary to top byt allows for more interaction, for example scrolling and pointing with a mouse. The processes can be selected and acted upon. See this [cheat sheet](https://www.maketecheasier.com/power-user-guide-htop/) for more.

### lsof
lsof lists on the standard output file information about files opened by processes. There are several options for the command, for example filtering by user. See this [cheat sheet](https://neverendingsecurity.wordpress.com/2015/04/13/lsof-commands-cheatsheet/) for more.

## Performance monitoring
Multiple tools are available for system performance monitoring. Here are some of the most popular.

### nmon
This is a fully interactive performance monitoring command-line utility tool for Linux. It displays performance metrics about the cpu, memory, disks, network etc...
It needs to be installed first. See [https://www.geeksforgeeks.org/linux-nmon/](https://www.geeksforgeeks.org/linux-nmon/) for more.

### iostat
This command is used for monitoring system input/output for devices and partitions. It monitors the time the devices are active as well as the transfer rates. It also needs to be installed first. See this [command guide](https://www.geeksforgeeks.org/iostat-command-in-linux-with-examples/) for more.

### vmstat
The Virtual Memory statistics (vmstat) reporter is a command line tool for Unix taht reports various information around the virtual memory management, such as memory usage, paging, I/O, CPU and disk.
See this [tutorial](https://www.geeksforgeeks.org/vmstat-command-in-linux-with-examples/) for more details.

# Resources

* [roadmap.sh - Devops roadmap - Process monitoring, performance monitoring, text manipulation](https://roadmap.sh/devops)