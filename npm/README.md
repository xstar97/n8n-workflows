# Nginx Proxy Manager n8n workflows

NPM has a rest API and I thought it would be extremely easy to use the API to create various workflows for it.
So....I did!


### backup Workflow

This [workflow](/npm/workflows/npm_backup_sample.json) makes api calls to npm to get the data and save it as a backup into a single json file every 6hrs.

all you have to do is edit the get-config-data node with your info and youre good to go!

```
{
   "npm_uri":"http://IP:PORT",
   "npm_auth":{
      "email":"email@gemail.com",
      "pass":"changeme"
   },
   "npm_backup_dir": "/media/npm/backups",
   "discord_web_hook": ""
}
```

------

### NPM upload Workflow
TBD

-----

### NPM Authelia advanced conf

This [workflow](/npm/workflows/npm_nginx_authelia_config_sample.json) automates the process of creating authelia's advanced nginx confs for each proxy host and then uploading it directly to NPM through the rest API.

note:
I reccomend looking into this [guide](https://dbt3ch.com/books/authelia-for-nginx-proxy-manager) for authelia.

```
{
      "authelia":"http://IP:PORT",
      "real_ip_from":"00.0.0.0/16",
      "auth_uri":"auth.mydomain.com",
      "npm_uri":"http://IP:PORT",
      "npm_auth":{
         "email":"email@example.com",
         "pass":"changme"
      },
      "proxy_host_x":"/data/proxy_host_x.conf",
      "discord_web_hook":"",
      "root_domain": "mydomain.com",
      "proxy_hosts":[
         "mydomain.com",
         "plex.mydomain.com",
         "adguard.mydomain.com"
      ]
      }
```

### Authelia access_control rules

This [workflow](/npm/workflows/npm_authelia_access_control_sample.json) creates the access_control rules and saves into a file called access_control.yml, at this time you have to extract the content from it and paste it into the configuration.yml overwriting the access_control rules yourself.
It makes a rest API call and gets all the proxy hosts for the account user.

note:
I reccomend looking into this [guide](https://dbt3ch.com/books/authelia-for-nginx-proxy-manager) for authelia.

```
{
      "npm_uri":"http://IP:PORT",
      "npm_auth":{
         "email":"email@example.com",
         "pass":"changeme"
      },
      "access_control_dir":"/configs",//save the file to a dir
      "access_control":{
         "default_policy": "deny",
         "auth_domain": "auth.mydomain.com",
         "rule_policy": "one_factor"
      }
```
