Simple Web Application Deployment on AWS EC2 Using Docker
Objective
Build and deploy a simple web application on AWS EC2 using Docker, configure basic security and implement monitoring with Prometheus and Grafana.

Prerequisites
Docker installed locally and on EC2.
AWS EC2 instance with SSH access.
AWS CLI installed and configured.
DockerHub and GitHub accounts.
Prometheus and Grafana Docker images for monitoring.
Steps
1. Docker Setup
Install Docker on the local machine and EC2 instance:
sudo apt update
sudo apt install -y docker-ce
sudo usermod -aG docker $USER
Create Dockerfile and index.html:
Use nginx:latest as the base image.
Copy index.html to /usr/share/nginx/html/.
Expose port 80.
2. Build and Push Docker Image
Build the Docker image:
sudo docker build -t my-web-app .
Tag and push the image to Docker Hub:
sudo docker tag my-web-app rpillaiakshay/my-web-app:latest
sudo docker login
sudo docker push rpillaiakshay/my-web-app:latest
3. Deploy on EC2
SSH into the EC2 instance and pull the Docker image:
sudo docker pull rpillaiakshay/my-web-app:latest
sudo docker run -d -p 80:80 rpillaiakshay/my-web-app:latest
Ensure port 80 is open for web traffic.
4. Monitoring with Prometheus and Grafana
Prometheus Setup:
Create /etc/prometheus/prometheus.yml with targets for Node Exporter and Grafana.
Run Prometheus:
docker run -d --name=prometheus -p 9090:9090 -v /etc/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml prom/prometheus:latest
Node Exporter:
docker run -d --name=node_exporter -p 9100:9100 prom/node-exporter:latest
Grafana:
docker run -d --name grafana -p 3000:3000 grafana/grafana
Outputs
Docker Image: docker pull rpillaiakshay/my-web-app:latest
Conclusion
This project demonstrates building and deploying a simple web application on AWS EC2 using Docker, with monitoring capabilities via Prometheus and Grafana. The setup ensures scalability and real-time system monitoring.
