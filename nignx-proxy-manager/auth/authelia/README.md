# npm rest API Authelia Workflow

the npm_authelia_proxy_host_sample is a [workflow](/nignx-proxy-manager/auth/authelia/npm_authelia_proxy_host_sample.json) that creates and updates the proxy hosts to use authelia from this particular [guide](https://dbt3ch.com/books/authelia-for-nginx-proxy-manager).

this workflow only updates the proxy-hosts advanced nginx conf, nothing else will change. I highly reccomend disabling the access list yourself which is why that flag is not updated automatically.

everything is configured in the first node "get-config-data", just update the info and use the comments as a guide.

```
[
   {
      "authelia":"http://0.0.0.0:9091", // set authelia's IP and port
      "real_ip_from":"0.0.0.0/16", // match your home network...192, 178, 10..etc
      "auth_uri":"auth.MY_DOMAIN.com", // auth uri that used for authelia
      "npm_uri":"http://0.0.0.0:81", // npm IP:PORT
      "npm_auth":{ // NPM BASIC AUTH, can be admin or specific user
         "email":"email@email.com",
         "pass":"changeme"
      },
      "proxy_host_x":"/media/auth/proxy_host_x.conf", // Set the location to point to the proxy_host_x.conf
      "discord_web_hook":null, //set it to false, "", or null if you do not wish to use the discord webhook
      "proxy_hosts":[ //create a js string array of all the domains you want to add authelia too., this is the filter list
         "adguard.mydomain.com",
         "bazarr.mydomain.com"
      ]
   }
]
```


all you need to do is download "[proxy_host_x.conf](/nignx-proxy-manager/auth/authelia/proxy_host_x.conf)" to a folder that the n8n workflow can access
and the workflow will update the proxy-host advanced conf.
