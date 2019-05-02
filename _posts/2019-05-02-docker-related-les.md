---
layout: post
title:  "question from Les"
date:   2019-05-02 21:30:00 +0800
categories: docker
---

### question from Les

* issue
```shell

不好意思，我想請問關於 docker-compose 的撰寫問題。
我現在想要將公司專案 docker 化開發。
所以寫了一個 docker-compose.yml

我希望將 flask 專案掛載進 container 利用 gunicorn 啟動 flask

我現在的 docker-compose.yml 長成這樣


    flask:
        build: ./backoffice/.
        container_name: backoffice
        volumes:
            - "./backoffice:/backoffice"
            - "/backoffice"
        expose:
            - 5000
        ports:
            - 5000:5000
        links:
            - backoffice-db
        networks:
            - backoffice-network
        command: bash -c "gunicorn -c ./backoffice/gunicorn.py run:app"

然而當我使用 docker-compose up 的時候他會跳

Error: './backoffice/gunicorn.py' doesn't exist

我確定我的 gunicorn.py 是有在 backoffice 中的

我懷疑 command 執行時，dir 位置不對導致找不到 gunicorn.py

我想請問， command 這個關鍵字的執行時機與執行時所處位置是怎麼判定的？
```

* Dockerfile
```dockerfile
# Use an official Python runtime as a parent image
FROM python:3.7.3-stretch

RUN mkdir /backoffice

# Set the working directory to /backoffice
WORKDIR /backoffice

# Copy the current directory contents into the container at /backoffice
COPY requirements.txt ./

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Copy the current directory contents into the container at /backoffice
COPY run.py ./
COPY config.py ./
COPY gunicorn.py ./
COPY .env ./

COPY app ./app
COPY log ./log

# pyc
RUN python3 -O -m compileall -b ./app
RUN find ./app -name "*.py"| xargs rm -rf

# Make port 5000 available to the world outside this container
EXPOSE 5000

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["gunicorn", "-c", "gunicorn.py", "run:app"]
```

