```
# Initialize
sudo docker run -d -p 8080:8080 -p 50000:50000 -v /var/jenkins_docker_data:/var/jenkins_home --name jenkins --restart=always jenkins/jenkins:lts

# Stop
sudo docker stop jenkins

# Start
sudo docker start jenkins
```

