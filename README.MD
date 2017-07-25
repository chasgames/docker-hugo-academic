# Hugo docker
Just a dockerfile and some commands
## Getting Started
#### Run the docker

```
docker run -d --name hugo -p yourPublicIP:80:1313 chasg/hugo server --bind "0.0.0.0" -p 1313
```

This spins up;
* Up-to-date Alpine OS
* Up-to-date Hugo 64 bit
* Up-to-date Academic Theme

Your site should be live at http://yourPublicIP

#### Copy existing website files over 

if you dont have a site, then you can git clone this directory to get an example site and edit it.
```
docker cp www/. hugo:/app/site
```
It's important you keep the "/." after your directory you want to copy

Inside your www folder, make sure it should be setup with the hugo directory structure https://gohugo.io/getting-started/directory-structure/
