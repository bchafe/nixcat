# nixcat
Compose and Service files for the NixCat Stack

This repo contains both the Docker Compose file and Systemd service file for the stack I run on my Nixcat server. The server I run these on is a Google Cloud f1-micro instance running CentOS 7. 

## The Compose Stack

The Compose stack is made up of 2 containers, one Wordpress container and one MariaDB container. Both containers are stock, and networked together using the legacy link. I understand that this means of networking is deprecated, but I opted for it due to simplicity and time constraints in implementation. I also figured that it was more secure than simply networking both containers through the host. 

I left the database password empty, both due to time constraints, and the fact that I don't consider any information stored as sensitive. My credentials are specific to this Wordpress instance, and commentors and other users do not have any reason to provide sensitive information, such as passwords. If someone had gained the priivileges and wanted to drop all tables for example, they could just as easily delete the database because they would already have the access required to do so. 

I've opted for implementing SSL for my Wordpress instance, as this allows me to log in from anywhere securely to post. Also, it looks a little nicer with the lock beside the URL :)

## The Service File

The service file is a pretty simple Systemd service. It pretty much just starts the stack in Docker Compose upon starting, and stops the stack upon stopping. It does a full on-off cycle when restarting too, which Compose seems to prefer. Using a Systemd service makes it easier to stop/start the stack. It also makes it easy to automate starting the stack, and gracefully closing it before the system goes down for maintenance.
