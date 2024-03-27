# Yolov4, Yolo-Fish, Docker container on a Server 
## Version 1.0, built by J. Giessmann, R. Subiza and N. Albers 
## BAZ1624@studium.uni-hamburg.de BAY0521@studium.uni-hamburg.de BAZ3955@studium.uni-hamburg.de

* https://github.com/AlexeyAB/darknet
* https://github.com/tamim662/YOLO-Fish

The goal was it to set up a version of Yolov4 with the loaded Yolo-Fish model inside a docker container on a linux server to detect zebrafish inside of aquariums. Ultimately counting them, as this data is needed for research.
To access the container more easily, a python web server was added, to upload and download data more easily.

# Steps for setup
- create directory zebrai 
- clone the following two github projects into zebrai
- https://github.com/Nikalb/darknet
- https://github.com/Nikalb/share-for-zebrAI
- configuration parts are marked by TODO as comments
- build a docker container from /darknet
- run the docker container from /darknet
- access the container via localhost:5656 (if not configured otherwise)

## How to download weights
- change into the directory /zebrai/dnshare/server/weights/ 
- download the weights from Google Drive:
- curl "https://drive.usercontent.google.com/download?id=1f9rmB3kYFGkUaCtIkYgkHD4gc2Mtt13V&confirm=xxx" -o merge_yolo-fish-1.weights
- curl "https://drive.usercontent.google.com/download?id=1EYq2nl-VlflaqIcWNI2mZH9ew_Aa4R5-&confirm=xxx" -o merge_yolo-fish-2.weights
- curl "https://drive.usercontent.google.com/download?id=10Xz3i03WXY8nxkuXxWk68VhmdlCUvQqK&confirm=xxx" -o merge_yolo-fish-3.weights
- curl "https://drive.usercontent.google.com/download?id=1QUk4AJr9-QMFrF2z3gyR2YsNYhwAkJqj&confirm=xxx" -o merge_yolo-fish-4.weights

### How to change the weights
- change the file the stated directory, for example for trained weights
- change the variable >>weights_path<< in darknet_main.py 

## Configured original files
- docker-compose.yml
- Dockerfile.cpu
- cocoo.data
- coco.names
- Makefile 

## Using GPU 
- Adapt the Dockerfile.gpu in a similar fashion to Dockerfile.cpu
- Change the values in Makefile to support GPU, make sure all drivers are and other dependencies are installied on the server
- Change the docker-compose.yml for yolo-gpu in a similar fashion to yolo-cpu, with the entrypoint, volume and ports. 

## Ideas for future features
- Delete pictures and folders
- Upload videos
- Live video streaming

- Train the model to detect specific zebrafishes 
--> https://github.com/AlexeyAB/darknet?tab=readme-ov-file#how-to-train-with-multi-gpu
