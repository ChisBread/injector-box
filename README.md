# Injector Box
- Happy Hacking!

## Do Not
```
git clone https://github.com/ChisBread/wechat-box target

wget -P target/root https://<Any>/WeChatSetup-v3.3.0.115.exe
wget https://<Any>/3.3.0.115-0.0.0.001.dll -o auto.dll

sudo docker build -t local/injector-box:latest .

sudo docker run -it --name injector-box \
    -e HOOK_PROC_NAME=WeChat \
    -e HOOK_DLL=auto.dll \
    -e TARGET_CMD=wechat-start \
    -v $PWD/auto.dll:/home/app/.wine/drive_c/injector/auto.dll \
    -p 8080:8080 -p 5555:5555 \
    local/injector-box:latest
```


## Related Projects
- https://github.com/chisbread/wine-box
- https://github.com/ChisBread/wechat-box
- https://github.com/cixingguangming55555/wechat-bot

## docker-compose
```yaml
version: "3.3"

services:
    injector-box:
        image: "chisbread/injector-box:latest"
        restart: unless-stopped
        container_name: "injector-box"
        environment:
            HOOK_PROC_NAME: 'WeProcName'
            HOOK_DLL: 'your.dll'
            TARGET_CMD: 'target-start'
            #optional INJMON_LOG_FILE: "/dev/null"
        ports:
            - "8080:8080" # noVNC
            - "5555:5555" # Hook API
        volumes:
            - "/path/to/your.dll:/home/app/.wine/drive_c/injector/your.dll"
            - "<path>:/home/app/.wine/drive_c/users/user/Application Data/"
            - "<path>:/home/app/Some Files/" 
        tty: true

```