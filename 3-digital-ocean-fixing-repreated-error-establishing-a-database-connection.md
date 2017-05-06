I Created a Droplet on Digital Ocean which was of the ones that comes preloaded with Wordpress. 

After a while I constantly received an error upon visiting the page which constantly said "Error Establishing a Database Connection". 

At first, this error seemed to be due to the fact that there wasn't enough memory to handle the application. Wordpress kept dying after an hour or so. Metrics didn't really show that it was under any load, but I still tried to upgrade the droplet. 

The error persisted, and one of the only remedies was to repeatedly restart `Apache` and `mysqld`. 

Most of the results online for remedies to this didn't really seem to apply to me. I found one that assumed there was something malicious going on. As mentioned in the forum post [here](https://www.digitalocean.com/community/questions/error-establishing-a-database-connection-wordpress):

```
...These attacks exploit the XML-RPC functionality in WordPress, as described on Securi.net

You can see if you are being taken down by this attack by running one of the following two commands on your droplet, depending on which webserver you're running:

Apache:
grep xmlrpc /var/log/apache2/access.log
Nginx:
grep xmlrpc /var/log/nginx/access.log
```

Alright, `grep` to look for suspicious requests in the log: 

<img src="/content/images/2017/logoutput.png"></img>

Dang!

The post goes on:
```
If you get any results there, it should be easy to fix this issue. If you've spun up a WordPress One-Click install droplet since Dec 2015, there's a small config file which you can enable to block such attacks. We don't enable it by default because it breaks some commonly used plugins (like Jetpack).... 

Here are the commands:
sudo a2enconf block-xmlrpc
sudo service apache2 restart
```

See more info on this method of attack [here](https://www.digitalocean.com/community/tutorials/how-to-protect-wordpress-from-xml-rpc-attacks-on-ubuntu-14-04).