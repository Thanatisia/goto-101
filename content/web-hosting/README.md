# Web-Hosting 101

## Information

## Steps
- Design and Plannings
    - Questions
        - Is your website a static or a dynamic website?
            - Static website: Does not require a database
            - Dynamic website: Requires a database and server API support
        - Types of web hosting required
            - Shared Hosting
                - Shared Web Hosting services are essentially web hosting services like Vercel, GitHub Pages, Heroku which lets you push your website into the server
                    + and the service will provide you with a domain name, but thats about it
                    + Requiring Dynamic websites that requires databases will require extra pricing and packages
            - VPS Hosting (Recommended)
                - Get a Virtual Private Server (VPS) for your website
                    + This is a remote server/location that you are not physically handling, such that there is a separation of responsibility
                    - Do this if you wish to host your website using your own server instead of a standalone Web Hosting service such as 
                        + Cloudflare Pages
                        + GitHub Pages
                        + Shopify
                        - Vercel : Specializes in static site hosting and serverless functions; 
                            - i.e. 
                                + Portfolio websites, standalone projects; 
                                - Supports: 
                                    + Frontend projects and frameworks like React
                        + Heroku
                    - Examples includes
                        + Amazon AWS
                        + DigitalOcean
                        + Linode (currently Akamai)
                + You will get your own VPS and setup the webserver and website to use on the VPS
                + You will own a webserver and a dedicated IP addresss tied to your VPS that you can link to a domain name
                - This means that 
                    + You wont reveal your home public IP network
                    + to update your website, you should setup a FTP server for easy push to production from your personal, home development environment
                    + However, you will also need to pay for their services
            - Managed Hosting
                + The web hosting platform will help manage the updating, backup and caching of your website
            - Dedicated Hosting
                + You will own the entire server dedicated to the website

- Get a domain name for your server's IP address
    + This can be on your VPS, or an alias pointing to an existing domain name
    - You can obtain a domain name from Domain Registrars
        - such as
            + Cloudflare
            + Domain.com
            + GoDaddy
            + Namecheap
            + Register.com
            + DuckDNS : This has a forced 'duckdns.org' domain appended to your domain name

- Connect your domain to your web host/VPS
    - In your Domain Registrar
        + Find your DNS Management or Name Server Settings
        + Find Name Server Settings

    - Web Hosting Service
        + Obtain your Web Hosting Provider's Name Servers
        + Set the Name Servers to the Web Hosting Provider's Name Servers
        + Update your Name Servers
        + Click Save
        + Obtain your domain name
        + Verify the Connection
            - Checking Website URL
                ```console
                nslookup [website-url]
                ```
            - Checking Domain and Nameserver
                ```console
                nslookup [your-domain-name] [nameserver]
                ```

    - VPS Web Server
        + Obtain your public IP address provided
        + Obtain your domain name
        - Set the Domain Name Servers to your obtained VPS Public IP Address using the A record
            - Lookup the current DNS Name server (NS) records
                ```console
                dig NS +short [domain-name]
                ```
            - Modify the A record type in your current DNS zone
                - Find an existing A and CNAME record type in the DNS Zone
                    +  Replace their values with your VPS Public IP Address
        - Verify the Connection
            - Checking Website URL
                ```console
                nslookup [website-url]
                ```
            - Checking Domain and Nameserver
                ```console
                nslookup [your-domain-name] [nameserver]
                ```
            - Using dig
                ```console
                dig A +short [domain-name]
                ```

- Perform Web Development

- Setup and prepare Web Server
    - Pre-Requisites
        - Update packages
            - Using apt
                ```console
                apt update && apt upgrade
                ```
        - Prepare Firewall
            - Install
                - Using apt
                    ```console
                    apt install ufw
                    ```
            - Enable the firewall so that unconfigured services will not be exposed (the IP ranges of VM providers are frequently scanned for not fully configured servers)
                - Allow Port 22
                    ```console
                    ufw allow 22
                    ```
                - Disable Logging
                    ```console
                    ufw logging off
                    ```
                - Enable Firewall
                    ```console
                    ufw enable
                    ```
                - Check status
                    ```console
                    ufw status
                    ```
        - Prepare SSL Certificate
            - Install certbot
                - Using apt
                    ```console
                    apt install certbot        
                    ```
            - Setup HTTPS
                ```console
                certbot --nginx
                ```
        - Select Web Server examples
            + Apache
            - Nginx
                ```console
                sudo apt install nginx
                ```
        + Setup a FTP server to move files
    - Edit Web Server configuration files
        - Nginx
            + Edit '/etc/nginx/sites-enabled/default'
            ```conf
            server {
         	# return 404 both via IPv4/6 when no other configuration handles the host
	        # '[::]:80' is neccessary for IPv6 - see https://serverfault.com/a/842515
         	listen 80 default_server;
	        listen [::]:80 default_server;
        	return 404;
            }
            ```
    - Move your Site pages into your Web server directories and locations
        + Generally in linux, it is '/var/www'
    - Restart Webserver
        - Apache
            ```console
            sudo systemctl restart apache
            ```
        - Nginx
            ```console
            sudo systemctl restart nginx
            ```

## Resources

## References
+ [ralfebert - tutorials - Nginx Static Website with HTTPS](https://www.ralfebert.com/tutorials/nginx-static-website-with-https/)

## Remarks