
#Static Website with Nginx (Dockerized)

This repository contains a fully dockerized static website (HTML/CSS/Images) served by Nginx.
The project demonstrates how to package a simple website into a Docker image and share it with others through Docker Hub.

⸻

📁 Project Structure

├── index.html
├── about.html
├── styles/
├── images/
└── Dockerfile

	•	HTML files – the website pages.
	•	styles/ – CSS files.
	•	images/ – images used by the site.
	•	Dockerfile – builds an Nginx container that serves the website.

⸻

##Dockerfile Explanation

The Dockerfile uses the official lightweight nginx:alpine image.

FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
COPY . /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

##What it does:
	1.	Downloads the Nginx server.
	2.	Removes default Nginx placeholder files.
	3.	Copies your website files into /usr/share/nginx/html (the Nginx web root).
	4.	Exposes port 80.
	5.	Starts Nginx in the foreground.

⸻

##How to Build the Docker Image

Run inside the project folder:

docker build -t mysite .

This creates a Docker image named mysite.

⸻

##How to Run the Website Locally (Docker Run)

Start a container:

docker run -d -p 8080:80 mysite

Now open your browser and visit:

http://localhost:8080

###Note: you you run this on a server with a public IP, 
you can use it instad of "localhost"

You should see your website running inside a Docker container.

⸻

##Publishing the Website to Docker Hub

If you want others to download and run your website easily, push it to Docker Hub.

* Log in:

docker login

* Tag your image:

Replace YOUR_USERNAME with your Docker Hub username.

docker tag mysite YOUR_USERNAME/mysite:latest

* Push it:

docker push YOUR_USERNAME/mysite:latest

Your image is now available in your Docker Hub repository.

⸻

##How Others Can Download and Run It

Anyone can pull and run your website:

docker pull YOUR_USERNAME/mysite:latest
docker run -d -p 8080:80 YOUR_USERNAME/mysite:latest

Then open in the browser:

http://localhost:8080


⸻

##Testing in the Browser

Once the container is running:
	1.	Open any browser (Chrome, Firefox, Edge).
	2.	Go to:

http://localhost:8080

	3.	You should see the static website served by Nginx.

To stop the container:

docker ps
docker stop <container_id>


⸻

##Summary:

This project demonstrates:

✔ How to serve a static HTML/CSS website using Nginx
✔ How to package it into a Docker image
✔ How to run it locally
✔ How to publish it to Docker Hub
✔ How others can pull and use your image
