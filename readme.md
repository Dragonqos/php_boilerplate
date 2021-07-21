# Boilerplate

### Version
0.0.1


~/.bashrc Linux helpers
~/.profile MAC helpers
```bash
parse_git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}
export PS1="\u@\h \[\033[32m\]\w\[\033[33m\]\$(parse_git_branch)\[\033[00m\] $ "

alias up_dev='docker volume create --name=app-sync && docker-compose -f docker-compose.yml -f docker-compose-dev.yml up -d'
alias up='docker network create shared && docker-compose up -d'
alias start='docker-compose start'
alias stop='docker-compose stop && docker-sync stop'
alias drop='docker rmi $(docker images -q)'

function de() {
    (  docker exec -it $* bash )
}

function recreate() {
    ( docker-compose stop $* && docker-compose rm -f $* && docker-compose pull $* && docker-compose up --build -d)
}

alias gs='git status'
alias commit='git commit -m'
alias add='git add .'
```

### Installation
1. Install docker
2. Run docker setup
```sh
$ docker network create shared
$ docker-compose up -d
or 
$ up
```

### NPM
If you will run npm build on virtual machine, your server become very slow.
To make it work faster try to run "npm start" on you host machine
```sh
$ brew install nodejs
$ npm install -g npm@7.9.0
$ npm i
$ npm run build:dll
$ npm run build:app
$ npm start
```

// For mac os: execute once the command `npm i` at the virtual machine to avoid inotify installation bug


### Unit tests

```sh
$ bin/phpunit 
```