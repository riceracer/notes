# Debug High IO

Run iostat to see which device is busy (command below shows stats every 1 second for 10,000 times):

    sudo iostat -x 1 10000

Run iotop to see which process is causing the problem:

    sudo iotop

Run this loop to see which process has a 'D' interupt - blocked waiting for IO:

    while true; do date; ps auxf | awk '{if($8=="D") print $0;}'; sleep 1; done

Run hdparm to time cached reads and buffered reads. Cached reads will be much faster.

    sudo hdparm -tT /dev/sda

(Laptop) check APM (Advanced Power Management) features - see man page for hdparm, but it can be used to prevent the drive from spinning down on a power save mode.

    sudo hdparm -B /dev/sda

Use smartctl to print information about the device:

     sudo smartctl -a /dev/sda

Run tests in smartctl

    sudo smartctl -t short /dev/sda
