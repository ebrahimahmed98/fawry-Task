# fawry-Task
devops fawry task
q1 

![hello](https://github.com/user-attachments/assets/8c5c79a2-a7f7-47ba-8c73-8ace2ba78687)

here is the output of the command of ./mygrep.sh hello testfile.txt



![-n ](https://github.com/user-attachments/assets/bacdd056-5542-4f89-ac55-7bd0e117c4cc)

screenshot to get the count of lines with command ./mygrep.sh -n hello testfile.txt




![-nv](https://github.com/user-attachments/assets/bc4c67ce-4e67-4323-9bf4-9527a42b3313)

the commpination of multi attripute 
./mygrep.sh -vn hello testfile.txt



![-v error](https://github.com/user-attachments/assets/2f2ec641-c9f5-499c-9696-6eeb1938939e)

how to handle errors in screen when excuting command :
./mygrep.sh -v testfile.txt


**Q2**

**firest we need to check the DNS records by command **
_cat /etc/resolv.conf_

**then we need to Test resolution with system DNS**
_nslookup internal.example.com
dig internal.example.com_


**also test the esolution with Google DNS**
_nslookup internal.example.com 8.8.8.8
dig internal.example.com @8.8.8.8_

If both fail: DNS record may be missing or propagation issue

If system DNS fails but 8.8.8.8 works: Local DNS misconfiguration

If system DNS works but 8.8.8.8 fails: Internal-only DNS record



**after we are having the IP from dig command **
say its 192.168.1.110
**then we have to ceck the connectivity by telnet command on web ports **
http port : 80 
https port : 443

_telnet 192.168.1.110 80
telnet 192.168.1.110 443_

**we need aslo the Check if service is listening by : **
_sudo netstat -tulnp | grep ':80\|:443'_


**IN a preif the possible cases that leads to thi issue is :-**

**DNS Record Missing**
we need to Compare dig output from authoritative DNS vs recursive
and the solution is : Update DNS zone
_sudo rndc reload example.com_

**DNS Cache Issues**
we have to Clear cache and retest by flushing DNS 
_sudo systemd-resolve --flush-caches_
or
_sudo systemctl restart nscd
_

**Local /etc/hosts Override**
Check for existing servers or hosts and Remove or correct any internal.example.com matches the same one 
_sudo nano /etc/hosts_














