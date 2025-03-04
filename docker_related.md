## Commands
Dont forget to add container name.
```bash
docker run --detach --interactive --network host \
  --cap-add SYS_PTRACE --cap-add SYS_ADMIN --device /dev/fuse \
  -v /run/user/1000/pulse:/run/user/1000/pulse \
  -e PULSE_SERVER=unix:/run/user/1000/pulse/native \
  -v /run/user/1000/pulse/native:/run/user/1000/pulse/native \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  -e QT_X11_NO_MITSHM=1 -e DISPLAY -e HOME -e USER \
  -t --entrypoint=/bin/bash \
  --name <container-name> --privileged \
  -v /dev:/dev \
  ros:humble-ros-base
```

```bash
id -u  # Get UID
id -g  # Get GID
```

```
docker exec -it <container-name> bash -c "groupadd -g <GID> <username> && useradd -u <UID> -g <GID> -m <username>"
```

```
docker exec -it <container-name> bash -c 'echo "<username> ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers'
```

```
docker exec --user $USER --workdir $HOME -it <container-name> bash
```
