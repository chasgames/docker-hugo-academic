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

1. #### Go into a folder where you want your website files. 
2. #### Run the below script, this will automagically create a "site" folder in the directory where you run this command. (it also mounts the folder to the docker)

```
docker run -d --name hugo -p 80:1313 hugo server --bind "0.0.0.0" -p 1313 --themesDir /app/themes && docker cp hugo:/app/site $(pwd) && docker stop hugo && docker rm hugo && docker run -d -v $(pwd)/site:/app/site --name hugo -p 80:1313 hugo server --bind "0.0.0.0" -p 1313 --themesDir /app/themes
```
Done!

### Already have an academic site?

---
Then all you need to do is tell docker where your file structure lives (the folder which contains config.toml content and static)

1. #### ```cd``` to the directory which contains your site files, e.g ```cd /var/www/```
 (config.toml content and static should live in that folder)

2. #### Run this line
```
docker run -d -v $(pwd):/app/site --name hugo -p 80:1313 hugo server --bind "0.0.0.0" -p 1313 --themesDir /app/themes
```




# Troubleshooting

 ### I want to bind it to a Public IP address, or change the port.

 No problem, just specify it next to the port section.
 
 In the docker run, replace:
 `-p 80:1313`
 with:
`-p 1.3.3.7:80:1313`

Which will be live at 1.3.3.7:80

### Don't want to mount web files to your host machine?
As an alternative to mounting, you could always remove the mounting line in docker run `"-v dir:dir"` and spin the docker up and copy and paste your website files.
```
docker cp www/. hugo:/app/site
```
It's important you keep the "/." after your directory you want to copy

Inside your www folder, make sure it should be setup with the hugo directory structure https://gohugo.io/getting-started/directory-structure/

## Upgrading 

```
docker stop hugo
docker rm hugo
re-run the docker line for existing website
```
You could also set up a cron for this task.


---

- [ ] Perhaps we can integrate a self-updating task inside the docker itself in the near future.