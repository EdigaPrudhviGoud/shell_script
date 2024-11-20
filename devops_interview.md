Monitor a network connectivity of a server & log the results if server is unreachable;
#!/bin/bash
IP=localhost
LOG_FILE=/var/log/network_check.log
DATE=$(date +%Y%m%d-%H%M%S)

while true;do
  ping -c 1 $IP > /dev/null 2>&1
  if($? -ne 0);then
    echo "Server not reachable at $DATE" >> $LOG_FILE
  fi
  sleep 60;
done


2.mysql backup
#!/bin/bash
MYSQL_HOST="localhost"
MYSQL_USER="root"
MYSQL_PASSWORD="passsword"
DATABASE="mifos"
#DATE=$(date +%Y%m%d-%H%M%S)
DATE=$(date)
FILENAME="mifos-$Date.sql"
mysqldump -h $MYSQL_HOST -u $MYSQL_USER -p $MYSQL_PASSWORD $DATABASE > $FILENAME

3.Create a script to check the available free memory on the system and alert the user if it falls below a threshold (e.g., 10%).
#!/bin/bash
# Set memory threshold (in percentage)
THRESHOLD=10
# Get the total and free memory using the 'free' command  Mem total used free
TOTAL_MEMORY=$(free -m | grep Mem | awk '{print $2}')
FREE_MEMORY=$(free -m | grep Mem | awk '{print $4}')
# Calculate the free memory percentage
FREE_MEMORY_PERCENTAGE=$(( (FREE_MEMORY * 100) / TOTAL_MEMORY ))
# Check if the free memory percentage is below the threshold
if [ $FREE_MEMORY_PERCENTAGE -lt $THRESHOLD ]; then
  # Send an alert (e.g., send an email or display a message)
  echo "Warning: Free memory is below the threshold! Only $FREE_MEMORY_PERCENTAGE% free memory left." | mail -s "Memory Alert" user@example.com
  # You can replace the email command with a custom action, e.g., logging or printing a message.
  echo "Warning: Free memory is below the threshold! Only $FREE_MEMORY_PERCENTAGE% free memory left."
fi




