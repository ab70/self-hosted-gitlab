## self-hosted gitlab CE via docker

## Setup

### 1. Docker command for initialization
```
sudo docker run --detach \
  --hostname gitlab.example.com \
  --publish 127.0.0.1:4443:443 --publish 127.0.0.1:4000:80 \
  --name gitlab \
  --restart always \
  --volume /srv/gitlab/config:/etc/gitlab \
  --volume /srv/gitlab/logs:/var/log/gitlab \
  --volume /srv/gitlab/data:/var/opt/gitlab \
  --env GITLAB_ROOT_PASSWORD='newpassword' \
  gitlab/gitlab-ce:latest
```

*** Now you can access it on 127.0.0.1:4000 and it will redirect to user signin page. If you are not redirected to root user password setup page then follow those steps:

## Fail root user setup
### Get into the gitlab docker terminal
```
docker exec -it gitlab bash 
```

### Get into gitlab railswhich is responsible for config
```
gitlab-rails console -e production
```
### Run this command for new username and password as root is user 1
```
user = User.where(id: 1).first
user.password = 'admin'
user.password_confirmation = 'admin'
user.save
exit
```

### Now you can login to root user and good to go.
