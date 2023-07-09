# Python - Code to Test Telnet Connection

```py
import sys
import telnetlib
from collections import defaultdict

def testTelnetConnection(fromServer, toHost, toPort):
    response = ""
    try:
        conn = telnetlib.Telnet(toHost, toPort)
        response = fromServer + ',' + toHost + ',' + toPort + ',' +'Success' + '\n'
    except:
        response = fromServer + ',' + toHost + ',' + toPort + ',' +'Failed' + '\n'
    finally:
        print(response)
        file1.write(response)


toHostPortList = [("xyz.com","80"), ("xyz.com","443"),
("xyz.com","21001"),("xyz.com","21002"),
("xyz.com","21003")]

file1 = open('output.txt', 'w')

for toHost, toPort in toHostPortList:
  testTelnetConnection('primary', toHost, toPort)

file1.close()
```

## Shell Script - Code to test Telnet Connection
- Note : Need to rework for failed one's

```sh
#!/bin/bash
servers=(
	xyz:80
	xyz:443
	xyz.com:21001
	xyz.com:21002
	xyz.com:21003
)

for each in ${servers[@]} ;do
        host=$(echo $each | cut -d ':' -f1)
        port=$(echo $each | cut -d ':' -f2)
        echo "Connecting ${host}:${port} .."
        telnet $host $port & WPID=$!
        sleep 5

        if ps -p $WPID > /dev/null ;then
                        echo "FAILED TO REACH ($WPID is running)"
                        kill $! 2>&1 >/dev/null
                        wait $WPID 2>&1 >/dev/null
                        echo "$host,$port,Fail, Failed to Connect" >> output.txt
        else
					echo "$host,$port,Pass, Connected Successfully" >> output.txt
        fi
done

```
