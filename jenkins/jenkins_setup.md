Create and Ubuntu EC2 service
Steps
install Jenkins (can use online tools to install it)
must have java 17 to work with the lastes jenkins
Steps
intalling nginx (can get the installing steps on line)
Steps
Important for using NGINX
configure reverse proxy. this makes it possible to use the host ip to point to jenkins without the port number

`sudo nano /etc/nginx/sites-available/jenkins`

`server {
    listen 80;
    server_name <your-domain> or <your-public-ip>;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    error_page 404 /404.html;

    # Add security headers
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";
}`

	Link the Configuration:
Link the configuration file to the sites-enabled directory:
`sudo ln -s /etc/nginx/sites-available/jenkins /etc/nginx/sites-enabled/`

Remove the Default Configuration:
If the default Nginx configuration is enabled, disable it:
`sudo rm /etc/nginx/sites-enabled/default`

Test (this will be testing for syntax errors)
`sudo nginx -t`

Knowing that I do not have permanent public ip for my server