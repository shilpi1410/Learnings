# virtual machine is ubuntu-pc with the username="user" and password user1234
Step 1.) Update System
         sudo apt update 
![vm_nginx1](https://github.com/user-attachments/assets/8dfb0d8c-a30b-4abb-af61-9805da1784c2)
Step 2.) Install nginx
         sudo apt install nginx
![vm_nginx2](https://github.com/user-attachments/assets/95b67f09-944a-489e-b134-2a2c4ab75b04)
Step 3.) Start nginx
         sudo systemctl start nginx
got error here 
![vm_nginx_error](https://github.com/user-attachments/assets/00a2e658-85a6-4f8d-984a-e599f3967a22)
It usually means port 80 is already in use by another process(apache2)
![vm_nginx3](https://github.com/user-attachments/assets/644c2660-9b80-4a40-bff1-6474649136f8)
so now Stop and Disable Apache
Step 4.) Stop and Disable Apache
       sudo systemctl stop apache2
       sudo systemctl disable apache2
       sudo systemctl start nginx
       sudo systemctl status nginx 
![vm_nginx4](https://github.com/user-attachments/assets/9d14592a-dcf6-4536-8a97-4c0799188547)   
Step 5.) Configure the Firewall
     sudo ufw allow 'Nginx HTTP'
     sudo netstat -tulpn | grep :80
     sudo ufw status
     sudo ufw allow 80/tcp
     sudo ufw reload
![vm_nginx5](https://github.com/user-attachments/assets/6c25ffc3-e87e-42fb-b4a1-ef03e24d7f4b)
Step 6.)sudo systemctl status nginx.service
step 7.) Test the Default Web Page   

http://localhost
http://192.168.1.10






       
