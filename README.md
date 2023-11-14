# Devcontainer for Flutter

![Static Badge](https://img.shields.io/badge/Flutter?label=3.13.9&labelColor=blue&color=gray)
![Static Badge](https://img.shields.io/badge/Flutter%20channel?label=stable&labelColor=blue&color=gray)
![Static Badge](https://img.shields.io/badge/command%20tools?label=10406996&labelColor=green&color=gray) <br>

Flutter development environment for Visual Studio Code Devcontainer or GitHub Codespace. <br>
Dockerfile Base on [`mcr.microsoft.com/devcontainers/base:ubuntu-22.04`](https://hub.docker.com/_/microsoft-devcontainers-base) <br>
Docker Hub: [https://hub.docker.com/r/hsun1031/devcontainer_flutter](https://hub.docker.com/r/hsun1031/devcontainer_flutter) <br>
Flutter version: `3.13.9` <br>
Flutter channel: `stable` <br>
Android command tools version: `10406996` <br>

## devcontainer.json
Use Dockerfile to build image
```json
{
	"name": "Flutter ",
	"dockerFile": "Dockerfile",
    ...
}
```
Use build image [`hsun1031/devcontainer_flutter:latest`](https://hub.docker.com/r/hsun1031/devcontainer_flutter) from `Docker Hub`
```json
{
    "name": "Flutter ",
    "image": "hsun1031/devcontainer_flutter:latest",
    ...
}
```

## Create Flutter project
```
flutter create .
```

## Build Android APK
```
flutter build apk
```

## Test for codespace
```
flutter run -d web-server
```