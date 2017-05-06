For applications that need to run forever, supervisord is awesome. It can monitor processes and automatically restart them if necessary. In addition, it can also provide log rotating and so much more. There's more to it, of course. Google is your friend.

Anyways, start by grabbing easy_install which will be used to get `supervisord` (credits to SaltyCrane Blog for the [source](http://www.saltycrane.com/blog/2010/02/how-install-pip-ubuntu/):
```
$ sudo apt-get install python-pip python-dev build-essential 
$ sudo pip install --upgrade pip 
$ sudo pip install --upgrade virtualenv
```

Now, get supervisord (for more detailed docs on installation, checkout the source [here](http://supervisord.org/installing.html)):
```
easy_install supervisor
```

Check your installation, the following command should output a bunch of text: 
```
$ echo_supervisord_conf
```

Create a configuration file:
```
echo_supervisord_conf > /etc/supervisord.conf
```

Add this to the end:
```
[program:foo]
command=/bin/cat
```

We are effectively creating a `program` which `supervisord` will manage.

Start `supervisord` (for official documentation, see [here](http://supervisord.org/running.html):
```
supervisord -c /etc/supervisord.conf
```

`supervisorctl` allows you to manipulate processes managed by `supervisord`. Check the current processes:
```
$ supervisorctl status all
```

Stop or start all processes (substitute the content within the [] with the following options):
```
$ supervisorctl [stop|start] [<program name>|all]
```

# BOOOOOOM.

--- 

#### Notes and Extras

- `supervisord` is a process and thus must be managed by some kind of init.d bootup script like Upstart. Google is your friend.

Here's a slightly more sophisticated `program` block:
```
[program:yousosalty]
command=/var/www/yousosalty/yousosalty
autostart=true
autorestart=true
startretries=100
directory=/var/www/yousosalty
```
That's the `program` definition for my side project, [You So Salty](yousosalty.com).

Here's my `program` definition for a ghost blog:
```
[program:ghost]
command=node /var/www/ghost/index.js
autostart=true
autorestart=true
startretries=100
directory=/var/www/ghost
user = ghost
stdout_logfile = /var/log/supervisor/ghost.log
stderr_logfile = /var/log/supervisor/ghost_err.log
environment = NODE_ENV="production"
```

---

#### Useful Links
- http://supervisord.org/installing.html
- http://serverfault.com/questions/96499/how-to-automatically-start-supervisord-on-linux-ubuntu
- http://centos-vn.blogspot.com/2014/06/daemon-showdown-upstart-vs-runit-vs.html
- https://elithrar.github.io/article/running-go-applications-in-the-background/
- https://kuntalchandra.wordpress.com/2016/03/24/supervisord-parallel-child-process-spawning-and-monitoring/