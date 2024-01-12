# Notes on progress

1/11/23 5pm
    Setup Gitea for local git version control on Truenas Scale
 - Deployed Gitea app via Truenas scale
    - http://10.1.1.50:10037/

1/11/23 5:45pm  
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
1/11/223 7pm
 - Setup Gitea Runner
    - Installed ACT_Runner docker image
    - See GiteaRunner folder in Containerize Challege
    - Docker Compose file creates container and registers with Gitea instance on local network
