### Scenario: "Saint John": what is writing to this log file?

### Level: Easy

**Description**: A developer created a testing program that is continuously writing to a log file **/var/log/bad.log** and filling up disk. You can check for example with **tail -f /var/log/bad.log**.
This program is no longer needed. Find it and terminate it. Do not delete the log file.

**Solution** - 
* Check the testing program which is continously running and generating the logs.

```python
#!/usr/bin/python3
# test logging
import random
import time
from datetime import datetime

with open('/var/log/bad.log', 'w') as f:
    while True:
        r = random.randrange(2147483647)
        print(str(datetime.now()) + ' token: ' + str(r), file=f)
        f.flush()
        time.sleep(0.3)
```

* Go to the log file **/var/log/bad.log**.
  
```shell
2026-02-09 18:00:42.604411 token: 361422547
2026-02-09 18:00:42.904846 token: 912432450
2026-02-09 18:00:43.205297 token: 875713819
2026-02-09 18:00:43.505752 token: 285756740
2026-02-09 18:00:43.806184 token: 152238596
2026-02-09 18:00:44.106619 token: 516426483
2026-02-09 18:00:44.407067 token: 1702444453
2026-02-09 18:00:44.707519 token: 1373183557
2026-02-09 18:00:45.007957 token: 1482951458
2026-02-09 18:00:45.308404 token: 263206428
2026-02-09 18:00:45.608861 token: 1560335646
2026-02-09 18:00:45.909335 token: 909708757
2026-02-09 18:00:46.209816 token: 1617209844
2026-02-09 18:00:46.510288 token: 1712896917
2026-02-09 18:00:46.810778 token: 2101640947
2026-02-09 18:00:47.111253 token: 2063756973
2026-02-09 18:00:47.411731 token: 486371717
2026-02-09 18:00:47.712192 token: 1640584632
2026-02-09 18:00:48.012666 token: 1124530575
2026-02-09 18:00:48.313179 token: 291890518
2026-02-09 18:00:48.613666 token: 1488946599
2026-02-09 18:00:48.914111 token: 966005676
2026-02-09 18:00:49.214585 token: 184307033
```

* The log file generates the log continously through program, must be there is a process for that.
  
```shell
ps -ef | grep python
```
```swift
root@ip-10-1-11-20:/home/admin# ps -ef | grep python
admin       594     1  0 17:59 ?        00:00:00 /usr/bin/python3 /home/admin/badlog.py
root        606     1  0 17:59 ?        00:00:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
admin       676   671  0 17:59 pts/0    00:00:00 /usr/bin/python3 /usr/bin/asciinema rec -t /ip-10-1-11-20 -q -i 2 /var/log/cast/ip-10-1-11-20
admin       679   676  0 17:59 pts/0    00:00:00 /usr/bin/python3 /usr/bin/asciinema rec -t /ip-10-1-11-20 -q -i 2 /var/log/cast/ip-10-1-11-20
root        723   693  0 18:01 pts/1    00:00:00 grep python
root@ip-10-1-11-20:/home/admin#
```

* Find the process ID and terminate the process.
  
```swift
root@ip-10-1-11-20:/home/admin# kill -9 594
root@ip-10-1-11-20:/home/admin# ps -ef | grep python
root        606     1  0 17:59 ?        00:00:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
admin       676   671  0 17:59 pts/0    00:00:00 /usr/bin/python3 /usr/bin/asciinema rec -t /ip-10-1-11-20 -q -i 2 /var/log/cast/ip-10-1-11-20
admin       679   676  0 17:59 pts/0    00:00:00 /usr/bin/python3 /usr/bin/asciinema rec -t /ip-10-1-11-20 -q -i 2 /var/log/cast/ip-10-1-11-20
root        736   693  0 18:02 pts/1    00:00:00 grep python
root@ip-10-1-11-20:/home/admin#
```

Problem Solved!!!!!








