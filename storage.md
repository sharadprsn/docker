Linux unifies all storate under a single tree. Storage devices such as disk or usb are attached to specific locations of 
the tree. These locations are called mount points. A mount point defines the location in the tree, the access properties
and the source of the data mounted at the point. Mount point allows software and users to use file tree in a linux environment
without actually knowing how the tree is mapped to specific storage location. This is particularly useful in storage devices.

Every container has something called a MNT namespace and a unique file tree root.
Three most important types of storage mounted in a container are:
-> Bind mounts
-> In memory storage
-> Docker Volumes


1. Bind mounts::
Consider while running a container some of its files need to be changed, example log location or html file. So instead of 
creating anew image we can mount the specified location of the smae image with custom files and html, just for that particular
container.

sudo docker run -d --rm --name ngweb \
--mount type=bind,source=/home/sharad/docker/files/nginx/example.conf,target=/etc/nginx/conf.d/default.conf \
--mount type=bind,source=/home/sharad/docker/files/nginx/example.log,target=/var/log/nginx/custom.host.access.log  \
--mount type=bind,source=/home/sharad/docker/files/nginx/index.html,target=/usr/share/nginx/html/index.html \
-p 80:80 \
nginx:latest

In the above command we have taken nginx image and updated the nginx conf file, location of log file generation and the 
html file. 
