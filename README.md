# CloudOps Portfolio
A responsive Cloud and DevOps portfolio built with HTML, CSS, JavaScript, Docker and Nginx.

## Run locally
docker build -t cloudops-portfolio .
docker run --rm -d --name cloudops-portfolio -p 8081:80 cloudops-portfolio

Open http://localhost:8081

## Stop
docker stop cloudops-portfolio
