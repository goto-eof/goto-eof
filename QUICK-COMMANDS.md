
Here are some usefull commands 

P.S. it's for me (=

# Git
### Push on 2 diferent repos
- `git remote -v`
- `git remote add all https://github.com/goto-eof/dev_board_ts_react.git`
- `git remote set-url --add --push all https://another-ropo.com/goto-eof/dev_board_ts_react.git`
- `git remote set-url --add --push all https://another-ropo.com/goto-eof/dev_board_ts_react.git`
- `git push all`


# Docker
- `docker system prune` - clean docker

## install docker and docker-compose
- sudo yum update -y
- sudo amazon-linux-extras install docker
- sudo service docker start
- sudo usermod -a -G docker ec2-user
- sudo curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
- sudo chmod +x /usr/local/bin/docker-compose
