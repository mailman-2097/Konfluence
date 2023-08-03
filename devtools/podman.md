# Podman in WSL

## Tool install
```
sudo apt -y install podman-docker # tool that  
sudo apt-get -y install buildah
```

## Tutorial
```
docker login quay.io -u nishad_ks # its podman in the background
docker run -it busybox /bin/sh
docker commit c2aaa9cc4105 quay.io/nishad_ks/container_images_public
docker push quay.io/nishad_ks/container_images_public
docker commit c2aaa9cc4105 quay.io/mailman_2097/container_images_public
docker push quay.io/mailman_2097/container_images_public
```

# Podman in Windows

