# Notes on progress

## 1/11/23

### 5pm
    Setup Gitea for local git version control on Truenas Scale
 - Deployed Gitea app via Truenas scale
    - http://10.1.1.50:10037/

### 5:45pm  
   - Built Ubuntu 22.04 VM for build environment
     -  ip: 10.1.1.144
   - Installed and updated the following apt packages
       - Docker

            ```Text
            sudo apt update
            sudo apt install apt-transport-https ca-certificates curl software-properties-common
            curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
            echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
            sudo apt update
            apt-cache policy docker-ce
            sudo apt install docker-ce
            ```

        - Docker Compose - inlcuded in Docker            
        - python3.12
            ```Text
            sudo add-apt-repository ppa:deadsnakes/ppa
            sudo apt update
            sudo apt install python3.12
            # Check success
            python3.12 --version
            ```
### 7pm
 - Setup Gitea Runner
    - Installed ACT_Runner docker image
    - See GiteaRunner folder in Containerize Challege
    - Docker Compose file creates container and registers with Gitea instance on local network

### 7:40pm
- Took a break
- Created notes.md to track milestones in progress

### 9pm
- Found https://github.com/nginx-proxy/nginx-proxy/tree/main
- use this to automate reverse proxy creation and update of containers
- Should only be used for containers running on a signle host
- Use this archetecture if this is scalled to cloud http://jasonwilder.com/blog/2014/07/15/docker-service-discovery/


## 1/12

### 1pm
- created Dockerfile for nginx
- swithced back to standard image of nginx to support a default config file configuration proceedure
- created nginx.conf 
    - config matches requirements found in readme.md udner section part one 

### 5pm
- Finalized server.py
- setup dockerfile for app
- finalized docker-compose.yml for build

## 1/14

### 5pm
- Fixed issue with hot loadding not working
- This happened because the code was copying over a static version of the source code in the app and no changes would be reflected in that
- added notes and built the docker images to complete the Validate script process.

## Final Output of ./validate.sh
```
imbeans@Ubuntu-Labv1:~/Docker/dev/Containerize-Challenge$ sudo bash ./validate.sh
Stopping containerize_nginx_1 ... done
Stopping containerize_app_1   ... done
Going to remove containerize_nginx_1, containerize_app_1
Removing containerize_nginx_1 ... done
Removing containerize_app_1   ... done
Building app
[+] Building 0.2s (6/6) FINISHED                                                                                                                                            docker:default
 => [internal] load build definition from Dockerfile                                                                                                                                  0.0s
 => => transferring dockerfile: 676B                                                                                                                                                  0.0s
 => [internal] load .dockerignore                                                                                                                                                     0.0s
 => => transferring context: 66B                                                                                                                                                      0.0s
 => [internal] load metadata for docker.io/library/python:3.12-slim                                                                                                                   0.0s
 => [1/2] FROM docker.io/library/python:3.12-slim                                                                                                                                     0.0s
 => CACHED [2/2] WORKDIR /app                                                                                                                                                         0.0s
 => exporting to image                                                                                                                                                                0.0s
 => => exporting layers                                                                                                                                                               0.0s
 => => writing image sha256:9bc3ffcff7aad05b5d4c74b4ee364ee31af8ed1215023a5f98aabadefbe91d49                                                                                          0.0s
 => => naming to docker.io/library/containerize-challenge_app                                                                                                                         0.0s
Creating containerize_app_1 ... done
Creating containerize_nginx_1 ... done
------------------------------------------------------------------------
| Testing SSL/TLS settings...                                          |
------------------------------------------------------------------------

 Start 2024-01-15 01:02:05                -->> 127.0.0.1:443 (localhost) <<--

 A record via:           /etc/hosts
 rDNS (127.0.0.1):       localhost.
 Service detected:       HTTP


 Testing protocols via sockets except NPN+ALPN

 SSLv2      not offered (OK)
 SSLv3      not offered (OK)
 TLS 1      not offered
 TLS 1.1    not offered
 TLS 1.2    offered (OK)
 TLS 1.3    offered (OK): final
 NPN/SPDY   not offered
 ALPN/HTTP2 http/1.1 (offered)

 Testing cipher categories

 NULL ciphers (no encryption)                      not offered (OK)
 Anonymous NULL Ciphers (no authentication)        not offered (OK)
 Export ciphers (w/o ADH+NULL)                     not offered (OK)
 LOW: 64 Bit + DES, RC[2,4], MD5 (w/o export)      not offered (OK)
 Triple DES Ciphers / IDEA                         not offered
 Obsoleted CBC ciphers (AES, ARIA etc.)            offered
 Strong encryption (AEAD ciphers) with no FS       offered (OK)
 Forward Secrecy strong encryption (AEAD ciphers)  offered (OK)


 Testing HTTP header response @ "/"

 HTTP Status Code             200 OK
 HTTP clock skew              0 sec from localtime
 Strict Transport Security    365 days=31536000 s, includeSubDomains, preload
 Public Key Pinning           --
 Server banner                nginx/1.25.3
 Application banner           --
 Cookie(s)                    (none issued at "/")
 Security headers             Content-Security-Policy: default-src 'self' http: https: data: blob: 'unsafe-inline'
                              X-XSS-Protection: 1; mode=block
                              Referrer-Policy: strict-origin
 Reverse Proxy banner         --



 Done 2024-01-15 01:02:14 [  13s] -->> 127.0.0.1:443 (localhost) <<--


------------------------------------------------------------------------
| Testing HTTP header and body content...                              |
------------------------------------------------------------------------
Pass: status code is 200
Pass: X-Forwarded-For is present and not 'None'
Pass: X-Real-IP is present and not 'None'
Pass: X-Forwarded-Proto is present and not 'None'
Pass: found "It's easier to ask forgiveness than it is to get permission." in response
------------------------------------------------------------------------
| Testing hot reload for local development...                          |
------------------------------------------------------------------------
Pass: found "It's harder to ask forgiveness than it is to get permission." in response
------------------------------------------------------------------------
| Docker image sizes:                                                  |
------------------------------------------------------------------------
Going to remove containerize_nginx_1, containerize_app_1
imbeans@Ubuntu-Labv1:~/Docker/dev/Containerize-Challenge$ 
```

