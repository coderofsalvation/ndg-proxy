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

## Config from app directories 

This proxy can automatically parse config from app-dirs.
Suppose you have all your apps living in a `/srv/app/` dir: 

    /srv/app/foo
    /srv/app/bar

Then put a 'config' file somewhere in a subdir like so: `/srv/app/foo/config` :

    HOST=http://foo.bar.com
    LISTEN=127.0.0.1
    PORT=8888

Then make sure to add/uncomment `CONFIGPATH+=("/srv/apps/*")` to the `daemon` file so the proxy knows where to look for configurations.

    
