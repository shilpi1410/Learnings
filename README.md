shilpi@Shilpi:~$ sudo systemctl start nginx
Error:

Failed to start nginx.service: Unit nginx.service is masked.




sudo systemctl unmask nginx
Enter hidden password and press enter.



This usually happens when:
Nginx configuration has syntax errors


Another service (like Apache) is already using port 80


A corrupted/missing configuration file

Running this to see the real reason behind the failure:
sudo journalctl -xeu nginx.service


shilpi@Shilpi:~$ sudo systemctl status nginx



Thanks for sharing the output. The error you're seeing:
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
means that port 80 is already in use, most likely by Apache or another web service.

On doing this -  sudo lsof -i :80 got
apache2 292     root    4u  IPv6   2673      0t0  TCP *:http (LISTEN)

 If Apache is running, stop and disable it:

sudo systemctl stop apache2
sudo systemctl disable apache2

Then check again:
sudo lsof -i :80

It should now return nothing.
 Disable Apache
sudo systemctl stop apache2
sudo systemctl disable apache2
Step 5.) Configure the Firewall
sudo ufw allow 'Nginx HTTP'
sudo netstat -tulpn | grep :80
sudo ufw status
sudo ufw allow 80/tcp
sudo ufw reload
Tree structure of Nginx
/
├── etc/
│   └── nginx/
│       ├── nginx.conf               # Main configuration file
│       ├── sites-available/        # Custom virtual hosts go here
│       ├── sites-enabled/          # Symlinks to active sites
│       └── snippets/               # Reusable config blocks
│
├── usr/
│   └── sbin/nginx                  # Main Nginx binary
│
├── var/
│   ├── www/
│   │   └── html/                   # Web root directory
│   │       └── index.html          # Your website’s homepage
│   └── log/
│       └── nginx/
│           ├── access.log          # All HTTP requests
│           └── error.log           # Errors from Nginx


