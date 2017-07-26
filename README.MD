# Hugo docker

This spins up;
* Up-to-date Alpine OS
* Up-to-date Hugo 64 bit
* Up-to-date Academic Theme

Your site should be live at on port 80, check the troubleshooting section if you want to bind to a certain IP address.

## Getting Started



### I don't have a site yet.

---
To create a brand-new site;

1. #### Go to a folder where you want your website files, Run the below script, this will automagically create a "site" folder in the directory where you run this command. (and it also mounts it on a re-run)

```
docker run -d --name hugo -p 80:1313 hugo server --bind "0.0.0.0" -p 1313 --themesDir /app/themes && docker cp hugo:/app/site $(pwd) && docker stop hugo && docker rm hugo && docker run -d -v $(pwd)/site:/app/site --name hugo -p 80:1313 hugo server --bind "0.0.0.0" -p 1313 --themesDir /app/themes
```
Done!

### I already have an academic site.

---
Then all you need to do is tell docker where your file structure lives (the folder which contains config.toml content and static)

1. #### ```cd``` to the directory which contains your site files, e.g ```cd /var/www/```
 (config.toml content and static should live in that folder)

2. #### Run this line
```
docker run -d -v $(pwd):/app/site --name hugo -p 80:1313 hugo server --bind "0.0.0.0" -p 1313 --themesDir /app/themes
```





Further torubleshooting
docker logs hugo

2. #### Copy existing website files over 

if you dont have a site, then you can git clone this directory to get an example site and edit it.
```
docker cp www/. hugo:/app/site
```
It's important you keep the "/." after your directory you want to copy

Inside your www folder, make sure it should be setup with the hugo directory structure https://gohugo.io/getting-started/directory-structure/
## Upgrading 
docker stop hugo
docker rm hugo
re-run the docker line for existing website
 
 ### I want to bind it to a Public IP address

