# Docker BIND9 DNS server

more info: [YT - DNS Server at home - Christian Lempa](https://www.youtube.com/watch?v=syzwLwE3Xq4&ab_channel=ChristianLempa)

## Why? 

I want to have a DNS server in my homelab to resolve servers / machines / docker containers and would like to extend on this to have valid SSL certificates on my homelab services. 

## Why BIND9? 

It is a very versatile, enterprise level and open-source DNS server.

## Waht do we need?

To run the BIND9 docker container we need: 
1. Ubuntu Server 22.04 (on Virtualbox / Proxmox or VMware with a Bridged NIC)
2. Docker and Docker compose installed
3. To make life easier VS Code with Remote Explorer

# How? 

Setup using the following steps:
1. Connect to your Ubuntu server via VS Code - Remote Explorer
2. Create a folder for this project e.g. 'labdns' or 'localdns'
3. Cd into this folder and create the following subfolders which are needed by BIND9 (cache, config and records)
4. Copy the docker-compose.yml file into the root of your project folder
5. Cd into the config folder and copy the cd zone file and adjust to your needs.

Once you finished the setup test the BIND9 container by start it with: 
```
docker-compose up
```

If you get an error saying 'ERROR: for bind9 listen tcp4 0.0.0.0:53: bind socket already in use.'. This is easily fixed by editing the /etc/systemd/resolved.conf where you find the line with ```#DNSStubListerner=yes``` and change it to: 
```
DNSStubListerner=no
```
After that restart systemd-resolved with the following command: 
```
sudo systenctl restart systemd-resolved
```
After this fix try test BIND9 again by running ```docker-compose up``` again.
All should be fine now and you can test if the DNS server is resolving correctly by querying it from another PC in the network, with the following command: 
```
nslookup yourdomain.com x.x.x.x
```
Where x.x.x.x is the IP address of the docker container.

Done! You build a DNS server in your homelab!

