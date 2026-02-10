#### Scenario: "Saskatoon": counting IPs.

##### Level: Easy

**Description**: There's a web server access log file at **/home/admin/access.log**. The file consists of one line per HTTP request, with the requester's IP address at the beginning of each line (first column).

Find what's the IP address that has the most requests in this file (there's no tie; the IP is unique). Write the solution into a file **/home/admin/highestip.txt**. For example, if your solution is "1.2.3.4", you can do echo **"1.2.3.4" > /home/admin/highestip.txt**

NOTE: The solution IP shows 482 times, ie **grep -c -F -f highestip.txt access.log** returns 482, if your solution has a different (lower) number you got the wrong most common IP.

##### 1. access.log file

```sh
45.77.23.10 - - [10/Jan/2025:14:01:01 +0000] "GET /index.html HTTP/1.1" 200 532
45.77.23.10 - - [10/Jan/2025:14:01:02 +0000] "GET /style.css HTTP/1.1" 200 2048
45.77.23.10 - - [10/Jan/2025:14:01:03 +0000] "GET /script.js HTTP/1.1" 200 3567
45.77.23.10 - - [10/Jan/2025:14:01:04 +0000] "GET /logo.png HTTP/1.1" 200 12567
45.77.23.10 - - [10/Jan/2025:14:01:05 +0000] "GET /dashboard HTTP/1.1" 200 890

10.0.0.1 - - [10/Jan/2025:14:10:01 +0000] "GET /contact HTTP/1.1" 200 421
172.16.0.5 - - [10/Jan/2025:14:10:02 +0000] "POST /login HTTP/1.1" 302 112
192.168.1.44 - - [10/Jan/2025:14:10:03 +0000] "GET /products HTTP/1.1" 200 2304
10.0.0.2 - - [10/Jan/2025:14:10:04 +0000] "GET /blog HTTP/1.1" 200 3102
```

##### 2. How we solve it

**Step 1 — Extract the first column (the IP)**

```sh
awk '{print $1}' access.log
```
**Step 2 — Count how many times each IP occurs**

We use an AWK associative array c[], When we see an IP, we increment its counter.

```sh
c[$1]++
```
**Step 3 — After reading all lines, print counts**

```sh
END { for (i in c) print c[i], i }
```
**Step 4 — Sort numerically, highest first**

```sh
sort -nr
```
**Step 5 — Take only the top result (most frequent)**

```sh
head -1
```
**Step 6 — Extract just the IP (second column)**

```sh
cut -d' ' -f2
```

##### Final

```sh
awk '{c[$1]++} END{for(i in c)print c[i],i}' /home/admin/access.log | sort -nr | head -1 | cut -d' ' -f2 > /home/admin/highestip.txt
```
##### Result

```sh
grep -c -F -f /home/admin/highestip.txt /home/admin/access.log
```

Problem Resolved!!!!
