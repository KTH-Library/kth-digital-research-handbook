# The staging version of this site

We have the following `Dockerfile` defined:
```
FROM nginx:alpine
RUN rm /etc/nginx/conf.d/default.conf
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
COPY ./.htpasswd /etc/nginx/.htpasswd
COPY ./site /usr/share/nginx/html
EXPOSE 80
```

And in the working directory we have a `.htpasswd` file and `nginx.conf`, here's the latter:
```
server {
   listen 80;
   server_name drguide.kth.chepec.se;
   location / {
      root /usr/share/nginx/html;
      index index.html;
      try_files $uri $uri/ =404;
      auth_basic "Restricted, please authenticate";
      auth_basic_user_file /etc/nginx/.htpasswd;
   }
}
```

The `.htpasswd` file contains just a single username/password, which I created interactively:
```
htpasswd -c .htpasswd kthb
```
This basic auth by a shared username/password is meant as a fallback in case the KTHCloud Private Auth proxy
cannot be tweaked to allow either any authenticated user or a preset list of KTH accounts
(I have sent in a question regarding this to the developers).


## To publish the staging site

Rebuild the site HTML/CSS in the local directory `site/`:
```
$ uv run mkdocs build -d site
```

Rebuild the Docker image and deploy it in one step (after authenticating, secrets redacted):
```
$ docker login ******* -u robot******* -p *******
$ docker buildx build --platform="linux/amd64" -t ******* --push .
```




## Background

It would be nice to have a staging area for KTH-DR User Guide.

A staging version of the site would allow a much faster workflow than copy-pasting final drafts into Confluence (along with building up the tree structure there).

The problem is where to host the generated static files...

- KTH Cloud only offers Docker deployments, which is not my forte. But I confirmed DNS redirection works! For some reason VM creation is grayed out (maybe temporary? there is no way except Discord to contact the team).
- EOSC Cloud is such a mess - I could not even figure out the public IPv4 address of the VM. The official docs talk about creating a Router, but their description does not match the web GUI. Very frustrating.
- I installed Apache on the VHS workstation (the machine is courtesy of Anders Wändahl) to test if it could act as webserver from my KTH laptop (connected to eduroam), but unfortunately it seems eduroam does not allow traffic on port 80 to the KTH wired LAN.
- I considered creating a container on my own NAS, but I abstained because there are no good answers to the question of authentication: basic Apache auth is simple to setup, but requires the team to learn another username and password; perhaps a firewall rule that only allows KTH:s subnet?
