Monitor a network connectivity of a server & log the results if server is unreachable;
#!/bin/bash
IP=localhost
LOG_FILE=/var/log/network_check.log
DATE=$(date +%Y%m%d-%H%M%S)

while true;do
  ping -c 1 $IP 
  if($? -ne 0);then
    echo "Server not reachable at $DATE" >> $LOG_FILE
  fi
  sleep 60;
done
