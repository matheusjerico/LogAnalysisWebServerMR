## How use this?

I am using VirtualBox with VM Cloudera Quickstart 5.13.0.

## Objective

Find out how many connections by IP.

## Log

Log files are a standard tool for computer systems developers and administrators. They record the (W5) “what happened when by whom, where and why happened” of the system. This information can record faults and help their diagnosis.

## Log format

The Common Log Format also is known as the *NCSA* Common log format. Each line in a file stored has the following syntax: **[host; ident; authuser; date; request; status; bytes]**

Ex: 10.223.157.186 - - [15/Jul/2009:15:50:51 -0700] "GET / HTTP/1.1" 200 9157

1. **10.223.157.186** is the IP address of the client (remote host);
2. **User-identifier** is the RFC 1413 identity of the client; ***missing data***
3. **authuser** is the user id of the person requesting the document; ***missing data***
4. **[15/Jul/2009:15:50:51 -0700]** is the date, time, and time zone that the request was received; 
5. **“GET / HTTP/1.1”** is the request line from the client;
6. **200** is the HTTP status code returned to the client;
7. **9157** is the size of the object returned to the client, measured in bytes.

A “–” in a field indicates missing data.

## Dataset

## Usage

Create directory in hdfs for move dataset and check:
``` bash
$ hdfs dfs -mkdir /mapred
$ hdfs dfs -ls /
```
Create directory in local for dataset:
``` bash
$ mkdir dataset;
```
Unzip dataset:
``` bash
$ cd dataset; unzip web_server.lob.zip
```
Move dataset to hdfs in directory /mapred:
``` bash
$ hdfs dfs -put web_server.log /mapred
$ cd ..
```

Create mapper.py:
``` python
#!/usr/bin/env python
import sys

for line in sys.stdin:
    data = line.strip().split(" ")
    if len(data) == 10:
        ip, id, authuser, datetime, timezone, method, path, proto, status, size = data
        print ip
```

Create reducer.py:
``` python
#!/usr/bin/env python

import sys

current_ip_count = 0
current_ip = None


for line in sys.stdin:
    new_ip = line.strip().split()
    if len(new_ip) != 1:
        continue

    if current_ip and current_ip != new_ip:
        print "{0}\t{1}".format(current_ip, current_ip_count)
        current_ip_count = 0

    current_ip = new_ip
    current_ip_count += 1

if current_ip != None:
    print "{0}\t{1}".format(current_ip, current_ip_count)
```

Change files permission
``` bash
$ chmod 777 mapper.py; chmod 777 reducer.py
```
Execute map reduce:
```bash
$ hadoop jar /usr/lib/hadoop-0.20-mapreduce/contrib/streaming/hadoop-streaming-2.6.0-mr1-cdh5.13.0.jar -file mapper.py -mapper mapper.py -file reducer.py -reducer reducer.py -input /mapred/web_server.log -output /output
```
## Author

[Matheus Jericó](http://linkedin.com/in/matheusjerico)

## License

MIT
