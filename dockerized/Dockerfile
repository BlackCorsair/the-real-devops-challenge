FROM ubuntu:18.04

ARG MONGO_URI_ENV=mongodb://localhost/test
ENV MONGO_URI=$MONGO_URI_ENV

RUN	apt-get update \
	&& apt-get install -y python3 python3-pip git gnupg2\
	&& apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4 \
	&& echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-4.0.list \
	&& apt-get update \
	&& apt-get install -y mongodb \
	&& service mongodb start \
	&& git clone https://github.com/BlackCorsair/the-real-devops-challenge /app \
	&& cd /app \
	&& mongoimport --file data/restaurant.json \
	&& pip3 install -r requirements.txt

RUN echo "service mongodb start && python3 /app/app.py" > /app/start \
	&& chmod +x /app/app.py

ENTRYPOINT ["bash", "/app/start"]