### Scenario: "Saint John": what is writing to this log file?

### Level: Easy

**Description**: A developer created a testing program that is continuously writing to a log file **/var/log/bad.log** and filling up disk. You can check for example with **tail -f /var/log/bad.log**.
This program is no longer needed. Find it and terminate it. Do not delete the log file.

**Solution** - 
* Check the testing program which is continously running and generating the logs.
  
<img width="579" height="224" alt="testing_program" src="https://github.com/user-attachments/assets/0a1bc7f7-6c40-4ddd-83de-6c454809b2d4" />

* Go to the log file **/var/log/bad.log**.

<img width="530" height="373" alt="badlog" src="https://github.com/user-attachments/assets/6737dd3e-c722-4150-add6-54ba2bead254" />

* The log file generates the log continously through program, must be there is a process for that.
  
```shell
ps -ef | grep python
```
<img width="720" height="263" alt="process" src="https://github.com/user-attachments/assets/47fc47d7-6632-4308-ace6-fb603d0012bc" />

* Find the process ID and terminate the process.

<img width="717" height="173" alt="terminate" src="https://github.com/user-attachments/assets/aa450ac5-775c-41d7-9e41-e50ad1732f8a" />

Problem Solved!!!!!

<img width="412" height="456" alt="Awesome" src="https://github.com/user-attachments/assets/e2222b67-38e7-4550-b725-abbd34010a11" />








