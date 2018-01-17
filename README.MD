# Hugo-Academic Docker

This docker container spins up;
* Latest [Alpine OS](https://www.alpinelinux.org/about/)
* Latest [Hugo 64 bit](https://gohugo.io/) (listening on port 80)
* Latest [Academic Theme](https://github.com/gcushen/hugo-academic)

and ... it's a nice small image size.

## Getting Started



### Don't have a site yet?

---
To create a brand-new site;

1. #### ```cd``` to the directory where you want your website files. 
2. #### Run the below script, this will automagically create a "site" folder in the directory where you run this command. (it also mounts the folder to the docker)

```
docker run -d --name hugo -p 80:1313 chasg/hugo server --bind "0.0.0.0" -p 1313 --themesDir /app/themes && docker cp hugo:/app/site $(pwd) && docker stop hugo && docker rm hugo && docker run -d -v $(pwd)/site:/app/site --name hugo -p 80:1313 chasg/hugo server --bind "0.0.0.0" -p 1313 --themesDir /app/themes
```
Done! - you can start modifying the website in the "site" folder it created.

### Already have an academic site?

---
Then all you need to do is tell docker where your file structure lives (the folder which contains config.toml content and static)

1. #### ```cd``` to the directory which contains your site files, e.g ```cd /var/www/```
 (config.toml content and static should live in that folder)

2. #### Run this line
```
docker run -d -v $(pwd):/app/site --name hugo -p 80:1313 chasg/hugo server --bind "0.0.0.0" -p 1313 --themesDir /app/themes
```

# Troubleshooting

 ### Something went wrong during "docker run"
You should get a hint of the problem with
```
docker logs hugo
```
then you will need to stop/remove and re-run the docker
```
docker stop hugo
docker rm hugo
re-run the docker line
```

 ### I want to bind it to a Public IP address, or change the port.

 No problem, just specify it next to the port section.
 
 In the docker run, replace:
 `-p 80:1313`
 with:
`-p 1.3.3.7:80:1313`

Which will be live at 1.3.3.7:80

### Theme modifications don't work
This Docker fully manages your themes directory and is kept seperately from your mounted site data. Therefore any existing theme directory is not applicable.

All you need to do is manage your config.toml content and static folders.

If you insist on testing some modifications to the theme, then you could do something like:
```
docker cp www/themes/. hugo:/app/themes
```
It's important you keep the "/." after your directory you want to copy

Though remember your theme modifications will be lost if you re-build the image.

### I want another theme!
Doh!, Maybe this Docker isn't for you, though it is possible with a few modifications :P

## Upgrading 

Image re-builds are made every day, therefore you could use watchtower to automaically update the container,

Or, to manually update on your side, you will need to:

```
docker stop hugo
docker rm hugo
re-run the docker line for existing website
```
You could also set up a cron for this task.

<dl>
 <style>.bmc-button img{box-shadow: none !important;border: none !important;vertical-align: middle !important;}.bmc-button{text-decoration: none !important;display:inline-block !important;padding:5px 10px !important;color:#FFFFFF !important;background-color:#FFFFFF !important;border-radius: 3px !important;border: 1px solid transparent !important;font-size: 26px !important;box-shadow: 0px 1px 2px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 1px 2px 2px rgba(190, 190, 190, 0.5) !important;-webkit-transition: 0.3s all linear !important;transition: 0.3s all linear !important;margin: 0 auto !important;font-family:"Cookie", cursive !important;}.bmc-button:hover, .bmc-button:active, .bmc-button:focus {-webkit-box-shadow: 0 4px 16px 0 rgba(190, 190, 190,.45) !important;text-decoration: none !important;box-shadow: 0 4px 16px 0 rgba(190, 190, 190,.45) !important;opacity: 0.85 !important;color:#FFFFFF !important;}</style><link href="https://fonts.googleapis.com/css?family=Cookie" rel="stylesheet"><a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/charles"><img src="https://www.buymeacoffee.com/assets/img/BMC-btn-logo.svg" alt=""><span style="margin-left:5px">Buy me a coffee</span></a>
 </dl>
---

- [ ] Perhaps we can integrate a self-updating task inside the docker itself in the near future.
