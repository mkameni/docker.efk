# Docker Definition for ElasticSearch Curator
FROM centos:7
MAINTAINER Moise Kameni <moise.kameni@adaware.com>

RUN mkdir /var/lib/curator
ADD delete_action.yml /var/lib/curator
ADD config.yml /var/lib/curator

# Install python-pip
RUN curl "https://bootstrap.pypa.io/get-pip.py" -o "get-pip.py"
RUN python get-pip.py

RUN pip install --quiet elasticsearch-curator

# download go-cron
RUN curl -L -o /usr/local/bin/go-cron-linux.gz https://github.com/odise/go-cron/releases/download/v0.0.7/go-cron-linux.gz
RUN gunzip /usr/local/bin/go-cron-linux.gz
RUN chmod u+x /usr/local/bin/go-cron-linux

ENV PATH=/usr/local/bin:$PATH
ENV SCHEDULE "* * * * * *"
ENV COMMAND "echo test go-cron"
EXPOSE 8080
CMD go-cron-linux -s "$SCHEDULE" -p 8080 -- /bin/bash -c "$COMMAND"
