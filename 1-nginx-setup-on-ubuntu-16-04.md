This is a barebones, quick and dirty post on how to install nginx and setup a server block for a sample html page; for the people like myself who can't ever remember how to do it, yet need to every once in a while. View the last, optional section for more detailed info.

Before doing anything, update:
```
sudo apt-get update
```

Install Nginx:
```
sudo apt-get install nginx
```

Use your preferred web browser and navigate to localhost:80, or the IP address of your VPS. Part of the content of the resulting web page should include "Welcome to nginx!" If this isn't the case, you have a problem. Google is your friend.


Now create a path for your site and a sample html page:
```
mkdir -p /var/www/mysite; echo "my website" > /var/www/mysite/index.html
```

Next, let's modify the Nginx configs to serve our index page. The default configuration is at `/etc/nginx/sites-available` and is usually named `default`. Save a backup somewhere, because we're going to edit it to look like the content below.
```
server {
       listen 80 default_server;
       listen [::]:80 default_server;

       server_name _;

       root /var/www/mysite;
       index index.html;

       location / {
       		try_files $uri $uri/ =404;
	}
}
```

Take note of the lines that start with `root` and `index`. With the first directive, `root`, we tell nginx where the website content lives. In the second directive, we tell nginx the default page to serve. 

Note that the line starting with `root` was the only change made from the original `default` config. Anything starting with `#` in a config is regarded as a comment.


Finally, restart nginx:
```
service nginx restart
```

Navigate to the page once again (localhost:80 or `<IP address>`:80). You should be seeing `my website`. BOOOOM.



--- 

#Extras

#### Setting Up a Second Engine Block with a Domain Name

Paste the following content into the new config at `/var/www/sites-available` and be sure to replace the self descriptive parts in between the angle brackets (<>) with the correct values (remove the brackets too):
```
server {
       listen 80:
       listen [::]:80;

       server_name <MY AWESOME DOMAIN NAME.COM>;

       root /var/www/<DIRECTORY OF MY AWESOME SITE>;
       index index.html;

       location / {
       		try_files $uri $uri/ =404;
	}
}
```
One notable change in contrast to the config up above is that the first two server block statements (begins with `listen`) DO NOT have `default_server` at the end. Only one server block gets to be default.

In addition to the changes, the `server_name` clause contains domain name information. Also, the `index` clause can be given a value other than index.html. Just something to be aware of, index.html is standard anyways.

To enable the config, it actually needs to be in sites-enabled. You can be ridiculous and copy it over, OR do it the more proper way and create a symlink from where it lives in `/etc/nginx/sites-available`:
```
# Format: ln -s <PATH OF SOURCE CONFIG> <PATH OF SYMLINK>
$ ln -s /etc/nginx/sites-available/<MYWEBSITE> /etc/nginx/sites-enabled/<MYWEBSITE>
```

This wasn't done in the earlier example because `default` was already enabled.

Voila! When you want to disable the config, remove the symlink and restart nginx.

