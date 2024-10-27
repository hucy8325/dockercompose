# dockercompose
version: '3'
services:
  opencv:
    build:
      context: .  # Dockerfile 所在目录
      dockerfile: Dockerfile
    image: hcy/opencv-container
    container_name: opencv-container
    environment:
      - DISPLAY=$DISPLAY
    volumes:
      - ${XAUTHORITY}:/root/.Xauthority
      - /tmp/.X11-unix:/tmp/.X11-unix 
      - .:/home/hcy/opencv  # 确保挂载的路径正确
    network_mode: host
    pid: "host"      # 添加 pid 命名空间共享
    ipc: "host"      # 添加 ipc 命名空间共享    
    privileged: true
    stdin_open: true
    tty: true
    user: "hcy"
    working_dir: "/home/hcy" # 指定默认工作目录