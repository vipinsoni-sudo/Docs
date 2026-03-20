# Docker Architecture

1. docker engine
2. docker demon
3. docker cli
4. docker client

# How to install Docker on AWS?

1. Login AWS and go to EC2 instance and click ***Launch an Install***
2. Enter instance name and select Ubuntu OS.
3. Instance type -> select ***t2.medium***
4. ***key pair (login)*** Create key pair entre name and click on ***create key pair*** button
5. configure storage select 15gb storage and click on ***Launch instance*** now instance created.

# Connect AWS instance to your pc bia ssh 

1. Open an SSH client.
2. Locate your private key file. The key used to launch this instance is docker-in-one-shot-key.pem
3. Run this command, if necessary, to ensure your key is not publicly viewable.
khmod 400 "docker-in-one-shot-key.pem"
4. Connect to your instance using its Public DNS:
ec2-35-91-25-145.us-west-2.compute.amazonaws.com

Example:
ssh -i "docker-in-one-shot-key.pem" ubuntu@ec2-35-91-25-145.us-west-2.compute.amazonaws.com

Note: In most cases, the guessed username is correct. However, read your AMI usage instructions to check
if the AMI owner has changed the default AMI username.

# After connect AWS instance
1. Run `sudo api-get update` to update system.
2. Now run `sudo apt-get install docker.io` to install docker in the system.
3. now run `sudo systemctl status docker` to check docker status.
4. Now run `docker ps` command to list running containers. if you getting error *permission denied ... massage* then run `sudo usermod -aG docker $USER` to give system permission to docker,
5. Run `newgrp docker` to refresh docker engin.


https://www.youtube.com/watch?v=9bSbNNH4Nqw  time:44:00