# SnipsServer Docker Image


A Docker Image for voice interaction using SNIPS	(SNIPS SERVER)


Initial Project Here  :
https://www.hackster.io/remy-mesnard/doorbell-intercom-with-snips-voice-assistant-68e77a

GitHub Project :
https://github.com/users/rmesnard/projects/1

Wiki :

#build

install git : 

sudo apt-get install git

Build with docker :

sudo docker build -t lijah/snips-server github.com/rmesnard/SnipsServer


#install

create volume :

sudo docker volume create snips_config
sudo docker volume create snips_log

#run 

sudo docker run -d --name snips-server \
	-v snips_log:/var/log \
	-v snips_config:/usr/share/snips \
	--privileged \
	-p 1883:1883 \
	lijah/snips-server

#share config 

docker run -d -p <IP HERE>:445:445 \
  -v  snips_config:/share/data \
  -v  snips_log:/share/log \
  --name samba trnape/rpi-samba \
  -u "admin:<YOUR PASSWORD>" \
  -s "snips_config:/share/data:rw:admin" \
  -s "snips_log:/share/log:rw:admin" 


#console

docker exec -it snips-server bash

cd /usr/share/snips
