## How use this?

I am using VirtualBox with VM Cloudera Quickstart 5.13.0.

## Objective

Find out how many connections by IP.

## Log

Log files are a standard tool for computer systems developers and administrators. They record the (W5) “what happened when by whom, where and why happened” of the system. This information can record faults and help their diagnosis.

## Log format

The Common Log Format also is known as the *NCSA* Common log format. Each line in a file stored has the following syntax:

**[host; ident; authuser; date; request; status; bytes]**

10.223.157.186 - - [15/Jul/2009:15:50:51 -0700] "GET / HTTP/1.1" 200 9157

1. **10.223.157.186** is the IP address of the client (remote host);
2. **User-identifier** is the RFC 1413 identity of the client; *missing data*
3. **raj** is the user id of the person requesting the document; *missing data*
4. **[15/Jul/2009:15:50:51 -0700]** is the date, time, and time zone that the request was received; 
5. **“GET / HTTP/1.1”** is the request line from the client;
6. **200** is the HTTP status code returned to the client;
7. **9157** is the size of the object returned to the client, measured in bytes. *missing or not*

A “–” in a field indicates missing data.


## Usage

## Dataset

## Usage

## Author

[Matheus Jericó](http://linkedin.com/in/matheusjerico)

## License

MIT
