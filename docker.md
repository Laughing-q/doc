- build:`docker build --tag hello-world .`
- show images: `docker images`
- 查看正在运行的image: `docker ps`, 只能看到正在运行的image
- 查看所有运行的image: `docker ps -a`, 能查看暂停的image
- 暂停image: `docker stop hello-world`
- 开启image: `docker start hello-world`
- 删除image运行进程: `docker rm name`
- run: `docker run -p 8080:80 --name hello -d hello-world` 
  * `--name`指定运行name，不指定则docker自己设定
  * `-p`指定端口
  * `-d`detached, 后台运行
- 查看后台运行image的日志: `docker logs name`
  * `-f`, `--follow`: Follow the log
- push image: `docker push `
  * tag: `docker tag hello-world laughingq/hello-world`
  * push: `docker push laughingq/hello-world`
- remove image: `docker rmi laughingq/hello-world`
- pull image: `docker pull laughingq/hello-world`

```shell
sudo docker pull ultralytics/yolov5:latest
sudo docker run --ipc=host --gpus all -it -v "$(pwd)"/coco:/usr/src/coco ultralytics/yolov5:latest
```

- `docker-compose`
  * `docker-compose up`
  * `docker-compose down`
