FROM python:3.9-buster

ENV ACCEPT_EULA=Y

RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
RUN curl https://packages.microsoft.com/config/debian/10/prod.list > /etc/apt/sources.list.d/mssql-release.list

RUN apt-get update \
    && apt-get install -y g++ \
    apt-utils \
    apt-transport-https \
    gcc \
    build-essential \
    unixodbc \
    unixodbc-dev \
    msodbcsql17 \
    mssql-tools \
    && apt-get upgrade -y \
    && apt-get clean \
    && sed -i -E 's/(CipherString\s*=\s*DEFAULT@SECLEVEL=)2/\11/' /etc/ssl/openssl.cnf \
    && pip install --upgrade pip \
    && pip install --no-cache-dir \
    autopep8 \
    flake8 \
    && rm -rf /var/lib/apt/lists/*

RUN echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
RUN /bin/bash -c "source ~/.bashrc"

WORKDIR /tmp/work

COPY requirements.txt ${PWD}

RUN pip install -r requirements.txt

EXPOSE 8888
