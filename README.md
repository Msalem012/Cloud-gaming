# Cloud gaming

Этот проект позволяет пользователям играть в компьютерные игры в браузере, без загрузки и установки, одним нажатием кнопки.
Это означает, что пользователи могут играть в игры AAA на своих низкопробных компьютерах, смартфонах или даже "умных" телевизорах в любое время и в любом месте.
Единственное требование - быстрый и надежный интернет.

Отличие этого проекта от других облачных игровых проектов в том, что он позволяет пользователям предлагать свои компьютеры (провайдеров) другим пользователям (игрокам) и получать прибыль.
То есть игры запускаются на компьютерах провайдеров и транслируются в браузеры игроков.

## Demo

![Demo](https://user-images.githubusercontent.com/16115992/159097057-be003206-8d2c-49f4-973b-7a27fccb8559.gif)

## Usage

### Prerequisite
- Golang >= 1.16
- NodeJs and npm (for Web UI)
- Docker and docker-compose (for providers)
- Current user on your computer has permissions to run Docker
- For now, we only support Linux providers

### How to run

- To run Coordinator service:
```bash
cd coordinator/
go run main.go
```

- To be a provider:
```
cd provider/
./run.sh
```

- To run UI:
```bash
cd web/
npm install
npm start
```

## Design

Этот проект вдохновлен [cloudmorph](https://github.com/giongto35/cloud-morph) и [drova.io](https://drova.io/).
Основная идея проекта - запуск игр в Wine внутри контейнеров Docker.
Видео и звук из игр захватываются Xvfb, Pulseaudio, обрабатываются ffmpeg, а затем транслируются в браузеры пользователей с помощью WebRTC.
Кроме того, входные данные от пользователей (например, щелчки мыши, события на клавиатуре) также перехватываются и передаются в Syncinput с помощью канала WebRTC Data.
Syncinput - это процесс, который получает эти данные и моделирует соответствующие события для игр с помощью WinAPI.
