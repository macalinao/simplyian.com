---
layout: post
title: "Setting up Virtual Hosts in Apache"
date: 2014-04-15 23:17:35 -0500
comments: true
categories: [Apache, Linux]
---

Today, I wanted to put my downloads on a different domain from my screenshots. Not wanting to manage multiple servers for no reason, I set up virtual hosts, also known as vhosts. Basically, depending on what domain you visit my web server from, you will get a different website. This is actually very simple to set up.

First, navigate to your `apache2` directory and go to the `sites-available` directory within it. On my Debian system, this is at `/etc/apache2/sites-available/`. In this directory, you'll see a bunch of files. Each one of these files is a config file that can be enabled or disabled individually; this is called a site.

To set up vhosting, you should first disable the default website. Use the command `sudo a2dissite default` to do this.

Next, add the rest of your websites. Here is the very simple config file I use:

```
<VirtualHost *:80>
    ServerName domain.you.want.to.use.com
    DocumentRoot /var/www/sitefiles/
    <Directory /var/www/sitefiles/>
        Options Indexes FollowSymLinks MultiViews
        Order allow,deny
        Allow from all
    </Directory>
</VirtualHost>
```

Save this to a file with the name of the site, no extension. I named my site `screenshots` for example.

Obviously, replace `domain.you.want.to.use.com` with the domain you want to use for the website. (For my screenshot website, this is `s.giza.us`.) The document root is the folder that contains the files at the root of your website. For me that's `/var/www/screenshots`.

Lastly, type `sudo a2ensite sitename` where `sitename` is whatever you named that file. Then, restart apache with `sudo service apache2 restart`, and all is well. For any additional domains, create more config files with that information, replacing all of the relevant stuff. Enjoy your awesome new vhosted website!
