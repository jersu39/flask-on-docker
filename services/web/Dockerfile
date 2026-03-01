# pull official base image
FROM python:3.11.3-slim-buster

USER root

# set work directory
WORKDIR /usr/src/app

# set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# install system dependencies
#RUN apt-get update && apt-get install -y netcat
#RUN apk add --no-cache netcat
#RUN apt-get update --allow-insecure-repositories --yes && apt-get install -y --no-install-recommends netcat
#RUN apt-get update --yes --allow-releaseinfo-change && apt-get install -y --no-install-recommends netcat
#RUN apt-get update -y && apt-get install -y --no-install-recommends netcat
RUN sed -i 's/http:\/\/deb.debian.org\/debian/http:\/\/archive.debian.org\/debian/' /etc/apt/sources.list
RUN apt-get update -y --no-install-recommends && apt-get install -y netcat

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt /usr/src/app/requirements.txt
RUN pip install -r requirements.txt

# copy project
COPY . /usr/src/app/

# run entrypoint.sh
ENTRYPOINT ["/usr/src/app/entrypoint.sh"]




# llm <<EOF
# $(files-to-prompt .)
# question
# EOF

# files-to-prompt . | xsel
# ^ clipboard when -X when log in, links to xserver on laptop
# to xserver on lambda

