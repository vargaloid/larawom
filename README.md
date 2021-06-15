# larawom
Larawom is from Laravel Workers Manager. Bash-script designed to help you to manage Laravel workers with SystemD.

*You could use this script not only for Laravel workers. It's suitable for using with any scripts or workers which you want to run more than one instance with multiple SystemD unit.*

## requirments
* Linux
* SystemD
* bash
* git

## installing
1. Clone project from GitHub repository
```bash
git clone https://github.com/vargaloid/larawom.git
```
2. Copy SystemD service and target to `/etc/systemd/system`
```bash
cp -r systemd_units/* /etc/systemd/system
```
3. Copy **larawom** to `/usr/bin` or `/usr/local/bin`
```bash
cp larawom /usr/local/bin
```
## configuring
1. In file **`laravel-worker@.service`**

In line `ExecStart` you should define full path to your interpreter and full path to run worker.

*Example:*
```
ExecStart=/usr/bin/php8.0 /var/www/example.com/artisan queue:work --sleep=3 --tries=3
```
or
```
ExecStart=/usr/bin/python3 /var/www/example.com/your-python-script.py
```
In lines `User` and `Group` you should define your web server user

*Example:*
```
User=www-data
Group=www-data
```
or
```
User=apache
Group=apache
```

2. In file **`larawom`**
You should define `worker` variable with your unique worker or script name
*Example:*
```
worker='artisan queue:work'
```
or
```
worker='your-python-script.py'
```

## using
```Bash
user@localhost:[/home/user]$ larawom argument

change    - change workers quantity. Example:  larawom change 5 
start     - Start all workers. Example:  larawom start 
status    - Status all workers. Example:  larawom status 
quantity  - Show workers quantity. Example:  larawom quantity
restart   - Restart all workers. Example:  larawom restart 
stop      - Stop all workers. Example:  larawom stop
```
