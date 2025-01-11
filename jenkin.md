#### 1. Jenkins Installation Using Podman 

```
sudo yum -y install podman

```

#### 2. Create Volume for Jenkins Data 

```
podman volume create jenkins-data

```

#### 3. Run Jenkins BlueOcean Container:

```
podman container run \
  --name jenkins-blueocean \
  --rm \
  --detach \
  --privileged \
  --publish 8080:8080 \
  --publish 50000:50000 \
  --volume jenkins-data:/var/jenkins_home \
  --volume jenkins-docker-certs:/certs/client:ro \
  jenkinsci/blueocean

```

#### 4. Generate Systemd Unit File:

```
podman generate systemd --name jenkins-blueocean --files --new

```

#### 5. Enable and Start Jenkins Service:

```
systemctl --user daemon-reload
systemctl --user enable container-jenkins-blueocean.service
systemctl --user start container-jenkins-blueocean.service

```

#### 6. Check Status:

```
systemctl --user status container-jenkins-blueocean.service

```


#### 7. Access Dashbord:

```
url: http://localhost:8080
```


#### How to check admin password for access dashborad.

```

rahulkumar@FPB-LAP-2608:~$ podman exec -it jenkins-blueocean sh
/ $ 

/ $ cat /var/jenkins_home/secrets/initialAdminPassword 
b181cb3e1658477cbec4621470bf574b

/ $ exit

```
