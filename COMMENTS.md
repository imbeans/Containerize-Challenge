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


