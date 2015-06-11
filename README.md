http-proxy server
=================

to reroute request internally/externally

## Usage

    ./proxy-server --table config.json

## Config examples

https

    {
      "http://www.mydomain.org": {
        "forward": "https://www.mydomain.org",
        "xfwd": true
      },
        "https://www.mydomain.org": {
        "target": "https://localhost:8070",
        "ws": true,
        "secure": true
      }
    }

simple

    {
      "http://www.mydomain.org": {
        "target": "https://localhost:8080"
      }
    }

externally

    {
      "http://www.mydomain.org": {
        "forward": "http://otherdomain.org",
        "xfwd": true
      }
    }
   
websocket
 
    {
      "http://www.mydomain.org": {
        "target": "https://localhost:8080",
        "ws": true
      }
    }

## Config from (ndg) app directories 

> ndg + ndg-proxy = multiple nodejscontainers in 1 nodejs container

ndg-proxy reads container-configurations from ndg

* more on ndg: https://github.com/coderofsalvation/nodejs-deploy-githook.bash
    
Suppose you have all your ndg apps living in a `/srv/app/` dir: 

    /srv/app/foo
    /srv/app/bar

The proxy will parse each`.ndg/config` file (which contains host/port configuration variables).

Then make sure to add/uncomment `CONFIGPATH+=("/srv/apps/*/.ndg")` to the `daemon` file so the proxy knows where to look for configurations.

