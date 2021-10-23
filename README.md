# kubernetes-change-cgroup-to-systemd-driver
sloving driver issue for kubernetes installation 
Nowadays kubernetes just suport systemd driver for managing resources but in default docker installation default driver will set to cfgroup and it become issue that kubelet wont start 

For fixing this issue you need to just creat this file and change docker driver from cfgroup to system :

cat > /etc/docker/daemon.json <<EOF
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
EOF
