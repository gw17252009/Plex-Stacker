Welcome to my Plex stack. This will install Plex, Tautulli, GAPS, Posterr and Plex Meta Manager. If you followed my ARR Stack 
you will only have to change whats in this file and add some DNS entries. If you don't you will need the reverse proxy and 
watchtower apps these will be provided for you to download. Dont forget the .env file.

I use network_mode: host for plex, if you don't want too then you can change.
There will be two lines in plex.yaml to change/remove: <br>
1. caddy.reverse_proxy: host.docker.internal:32400 change to caddy.reverse_proxy: "{{upstreams 32400}}"
2. network_mode: host change to <br>
      networks: <br>
        - caddy <br>

I use a nvidia GPU for hardware acceleration, if you do, you will also need to install https://github.com/NVIDIA/nvidia-container-toolkit
if you do not there are three lines to remove noted in plex.yaml.
If you use a Intel QuickSync device you need to add: <br>
      devices: <br>
        - /dev/dri:/dev/dri <br>

Plex Meta Manager uses 2 config files. I have provided mine as examples. I have provided links to PMM's website where you can
learn to modify to your use case and liking. Please read up on this. The 2 files go in <path/for/config>/pmm/config

If you are already using the ports for other apps change ONLY the left side of XXXX:XXXX.

The actual configuring each application to your liking is up to you. I have provided links for each service:

Self Hosted Streaming service: <br>
  Plex: <br>
    https://www.plex.tv/ <br>
    https://hub.docker.com/r/linuxserver/plex <br>
<br>
PLex Analytics: <br>
  Tautulli: <br>
    https://tautulli.com/ <br>
    https://hub.docker.com/r/linuxserver/tautulli <br>
<br>
Movie Collections: <br>
  GAPS:
    Note: GAPS is no longer maintained but still works <br>
    https://github.com/JasonHHouse/gaps <br>
    https://hub.docker.com/r/housewrecker/gaps <br>

Plex Metadata Manager: <br>
  I recommend using the official docker image and so does PMM <br>
    PMM: <br>
      https://metamanager.wiki/en/latest/ <br>
      https://hub.docker.com/r/meisnate12/plex-meta-manager <br>
<br>
Media Signage Poster: <br>
  Posterr: <br>
    https://hub.docker.com/r/petersem/posterr <br>
    https://github.com/petersem/posterr <br>

You must have Docker and Docker Compose installed. For info check https://docs.docker.com/

You can follow this to install docker:
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-compose-on-ubuntu-20-04

You must have your own domain name get one from
https://www.cloudflare.com or
https://www.namecheap.com

Have DNS entries in your DNS provider. I use cloudflare.com. You want an "A" record for each service EXCEPT: caddy and watchtower 
these do NOT need DNS records (you wont be accessing them at all. they work in the background) A "CNAME" for your domain

You must have ports 80 & 443 open on server and router.

You must create docker network caddy: command line: docker network create caddy
