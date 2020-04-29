# centos7SSH
Centos 7 image with ssh

podman build --rm --pull -t localhost/centos7:0.0.1 .
podman run -d -p 2222:22 --name centos --rm localhost/centos7:0.0.1
