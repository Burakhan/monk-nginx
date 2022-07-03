## Serving static files with Monk
This repository contains Monk.io template to deploy Wordpress system either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

# Prerequisites
- [Install Monk](https://docs.monk.io/docs/get-monk)
- [Register and Login Monk](https://docs.monk.io/docs/acc-and-auth)
- [Add Cloud Provider](https://docs.monk.io/docs/cloud-provider)
- [Add Instance](https://docs.monk.io/docs/multi-cloud)

#### Make sure monkd is running.
```bash
foo@bar:~$ monk status
daemon: ready
auth: logged in
not connected to cluster
```

## Check cluster nodes
foo@bar:~$ monk cluster peers
✔ Got the list of peers
ID                                              Name   Tag  Provider  Containers  IP           Uptime   Active  Version  Pressure
QmXiEXRNs5tSjKcYvZcX4Z71qBEs2rZeiUEYaM8wLrKHME  local       unknown   0           127.0.0.1    28m 26s  true    v3.4.3   false
QmQN8BBx7Py3yZc9sq8Zshy9mN6YPs2YNNxsCg1oJrbrtN  wp-1   wo   aws       3           52.59.97.36  16m 2s   true    v3.4.3   false

## Clone Repository
```bash
git clone https://github.com/Burakhan/monk-nginx
cd monk-nginx
```


## Load template
foo@bar:~$ monk load MANIFEST
✔ Read files successfully
✔ Loaded nginx.yml successfully

Loaded 1 runnables, 0 process groups, 0 services, 0 entities and 0 entity instances
✨ Loaded:
 └─🔩 Runnables:
    └─🧩 monk-nginx/latest
✔ All templates loaded successfully

## Run nginx 
foo@bar:~$ monk run monk-nginx/latest
✔ Starting the job: monk-nginx/latest... DONE
✔ Preparing nodes DONE
✔ Checking/pulling images...
✔ [================================================] 100% docker.io/bitnami/nginx:latest QmXiEXRNs5tSjKcYvZcX4Z71qBEs2rZeiUEYaM8wLrKHME
✔ Checking/pulling images DONE
✔ Starting containers DONE
✔ monk-nginx/latest has been already running

🔩 templates/local/monk-nginx/latest
 └─🧊 Peer QmXiEXRNs5tSjKcYvZcX4Z71qBEs2rZeiUEYaM8wLrKHME
    └─🔩 templates/local/monk-nginx/latest
       └─📦 local-137b7dc879967d1182d2538012-monk-nginx-latest-nginx-static
          ├─🧩 docker.io/bitnami/nginx:latest
          ├─💾 /Users/burakhan/www/monkd/monk-nginx/app -> /app
          └─🔌 open tcp localhost:8080 (0.0.0.0:8080) -> 8080

💡 You can inspect and manage your above stack with these commands:
	monk logs (-f) monk-nginx/latest - Inspect logs
	monk shell     monk-nginx/latest - Connect to the container's shell
	monk do        monk-nginx/latest/action_name - Run defined action (if exists)
💡 Check monk help for more!

## Variables
The variables are in `nginx.yml` file. You can quickly setup by editing the values here.

| Variable                     	| Description                                           	|
|------------------------------	|-------------------------------------------------------	|
| listen-port                   | The port number where the server will serve the files 	|
| static-data:      	        | The path of the files to be served.                    	|
| server_name                  	| The domain name you want to run                       	|


## Stop, remove and clean up workloads and templates

```bash
monk purge -x monk-nginx/latest
```
