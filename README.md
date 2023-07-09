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
