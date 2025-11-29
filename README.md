# Static Website with Nginx (Dockerized)

This repository contains a dockerized static website (HTML, CSS, images)
served by **Nginx**.\
It demonstrates how to package a website into a Docker image and share
it on **Docker Hub**.

## 📁 Project Structure

    ├── index.html
    ├── about.html
    ├── error(404).html
    ├── styles/
    ├── images/
    └── Dockerfile

## Dockerfile Explanation

The project uses the official lightweight **nginx:alpine** image.

``` dockerfile
FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY . /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

### What this Dockerfile does:

1.  Pulls the official lightweight Nginx server.
2.  Removes the default Nginx HTML files.
3.  Copies your website files into Nginx's web directory.
4.  Exposes port **80**.
5.  Starts Nginx in the foreground.

## How to Build the Docker Image

Run this inside the project folder:

``` bash
docker build -t mysite .
```

## How to Run the Website Locally

Start the container:

``` bash
docker run -d -p 8080:80 mysite
```

Then open in your browser:

    http://localhost:8080

## Publishing the Image to Docker Hub

### 1. Log in:

``` bash
docker login
```

### 2. Tag the image:

Replace **YOUR_USERNAME** with your Docker Hub username.

``` bash
docker tag mysite YOUR_USERNAME/mysite:latest
```

### 3. Push to Docker Hub:

``` bash
docker push YOUR_USERNAME/mysite:latest
```

## How Others Can Download and Run It

``` bash
docker pull YOUR_USERNAME/mysite:latest
docker run -d -p 8080:80 YOUR_USERNAME/mysite:latest
```

Open:

``` bash
http://localhost:8080
```

## Testing in the Browser

1.  Start the container.
2.  Open a browser.
3.  Go to:

``` bash 
<http://localhost:8080>
```

To stop:

``` bash
docker ps
docker stop <container_id>
```

## ✔ Summary

This project demonstrates:

-   Serving a static HTML/CSS website using Nginx\
-   Packaging the site into a Docker image\
-   Running it locally\
-   Publishing it to Docker Hub\
-   Letting others download and run it easily
