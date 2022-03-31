- linux映射windows共享文件夹
  ```shell
  yay -S coreutils
  sudo mount.cifs //10.10.1.240/algodata4/oyrq /sharefile -o user=algodata
  ```

- linux映射linux服务器文件夹
  ```shell
  yay -S nfs-utils
  sudo mount -t nfs 192.168.2.195:/data /facedata
  ```

