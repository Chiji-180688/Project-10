# Project-10 Documentation

Step 1: Registering for a domain name and linking it to route 53 and load balancer
1. Creating an Ubuntu ec2 instance named load balancer
2. Creating hosted zone
![hosted zone](./Project-10%20Images/creating%20hosted%20zone.png)
![hosted zone2](./Project-10%20Images/creating%20hosted%20zone2.png)
3. Creating name server
![name server](./Project-10%20Images/creating%20name%20servers.png)
![name server2](./Project-10%20Images/creating%20name%20servers2.png)
![name server](./Project-10%20Images/creating%20name%20servers3.png)
4. Creating records
![records](./Project-10%20Images/creating%20records.png)
![records](./Project-10%20Images/creating%20records2.png)

Step 2: Openning portals 80 and 443
![editing inbound rules](./Project-10%20Images/port%2080%20and%20443%20opened%20for%20lb.png)

Step 3: Installing nginx and configuring it as a load balancer to point traffic to the resolvable DNS names of the webservers
`sudo apt update`
`sudo apt install nginx`
2. Confirming domain name in browser
[domain name in browser](http://igomo.online)
![domain name in browser](./Project-10%20Images/domain%20to%20nginx.png)
`sudo vi /etec/hosts`
![configuring host](./Project-10%20Images/configuring%20etc%20hosts.png)
`sudo vi /etc/nginx/nginx.conf`
![configuring nginx.conf](./Project-10%20Images/updating%20nginx.conf%20file.png)
3. Removing nginx test page
`sudo rm -f /etc/nginx/sites-enabled/default`
`sudo nginx -t`
![confirming nginx configuration](./Project-10%20Images/removing%20nginx%20test%20page.png)
`sudo systemctl restart nginx`
`sudo systemctl status nginx`
![nginx status](./Project-10%20Images/nginx%20active%20and%20running.png)
4. Linking nginx.conf to sites-available
`cd /etc/nginx/sites-enabled/`
`sudo ln -s ../sites-available/load_balancer.conf .`
`ls`
![lb.conf linked](./Project-10%20Images/load_balancer.conf%20file%20linked.png)
`ll`
![lb.conf linked](./Project-10%20Images/load_balancer.conf%20file%20linked2.png)
5. Reload nginx
`sudo systemctl reload nginx`
6. Reloading domain name in browser
![lb redirected to web server](./Project-10%20Images/load%20balancer%20redirected%20to%20web%20server.png)

Step 4: Configuring secure connections using ssl/tsl
1. Installing certbot
`sudo apt install certbot -y`
![certbot installed](./Project-10%20Images/certbot%20installed.png)
2. Installing dependencies
`sudo apt install python3-certbot-nginx -y`
![python3 installed](./Project-10%20Images/python3-certbot-nginx%20installed.png)
3. Check syntax
`sudo nginx -t`
![confirming configuration](./Project-10%20Images/removing%20nginx%20test%20page.png)
4. Reloading nginx
`sudo systemctl reload nginx`
5. Creating certificate
`sudo certbot --nginx -d igomo.online -d www.igomo.online`
![creating cert](./Project-10%20Images/registering%20my%20certificate.png)
![creating cert2](./Project-10%20Images/registering%20my%20certificate2.png)
![creating cert3](./Project-10%20Images/certificate%20successfully%20registered.png)
![certificate details](./Project-10%20Images/certificate%20details.png)
6. Setting up periodical renewal of my SSL/TLS certificate
`crontab -e`
![crontab setup](./Project-10%20Images/setting%20up%20periodical%20renewal%20of%20certificate.png)
![crontab setup2](./Project-10%20Images/setting%20up%20periodical%20renewal%20of%20certificate2.png)
