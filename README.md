Database Shard GitHub.

For this project we need a vitual machine running with OS ubuntu and you need to install docker and docker-compose.

this is how to install docker community edition.

sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update
sudo apt install docker-ce

Check the Docker status with command.
sudo systemctl run docker
sudo systenctl enable docker
sudo systemctl status docker.

Installation docker compose:

sudo apt install docker-compose.

install client access to MariaDB

sudo apt install MariaDB-client.

set up and clone maxscale-docker repositoy rom Zohan GitHub.

https://github.com/Zohan/maxscale-docker.git

we will direct to maxscale directory. “ /maxscale/maxscale-docker/maxscale# “ and run the following command:

docker-compose build
docker-compose up -d

Starting maxscale_master1_1 ... done

Starting maxscale_master2_1 ... done

Starting maxscale_maxscale_1 ... done

After that we will edit the docker-compose.yml in maxscale directory

nano docker-compose.yml

Edit the example.cnf file inside the maxscale.cnf.d file

nano example.cnf

once the example.cnf file edited, create SQL shard files inside the master directory

/maxscale/maxscale-docker/maxscale/sql/master#

Use the following command to list the servers

docker-compose exec maxscale maxctrl list servers

┌─────────┬─────────┬──────┬─────────────┬─────────────────┬──────────┐
│ Server  │ Address │ Port │ Connections │ State           │ GTID     │
├─────────┼─────────┼──────┼─────────────┼─────────────────┼──────────┤
│ server1 │ master  │ 3306 │ 0           │ Master, Running │ 0-3000-5 │
├─────────┼─────────┼──────┼─────────────┼─────────────────┼──────────┤
│ server2 │ slave1  │ 3306 │ 0           │ Slave, Running  │ 0-3000-5 │
├─────────┼─────────┼──────┼─────────────┼─────────────────┼──────────┤
│ server3 │ slave2  │ 3306 │ 0           │ Running         │ 0-3000-5 │
└─────────┴─────────┴──────┴─────────────┴─────────────────┴──────────┘


we can use the following command to connect to DB:

mariadb -umaxuser -pmaxpwd -h 127.0.0.1 -P 4000

I got helped by Abdirizak kulmiye who he is the tutor for our class. 

Refrences:

Repository was fork from Dr. Zak (https://github.com/Zohan/maxscale-docker.git)
The Readme.md file was also edit from Dr. Zak gitHup (https://github.com/Zohan/maxscale-docker.git)

