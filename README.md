# ansible-pull

## Dependency

1. python3
2. docker(pip3 install docker)
3. docker/docker-compose

## How makes ansible-pull work on vps

**ALWAYS USE ABSOLUTE PATH**

local.yml

1. private_key - absolute path to private key for repo
2. repo_url - url(ssh) to repo
3. workdir - workdir on the server where docker-compose.yaml/webapp will be placed
4. logfile - where place log file
5. ansible_bin - package where stored ansible-pull

```
ansible_bin: /opt/homebrew/bin
```

how find

```
which ansible-pu
ll
```

## How run example

Now code from github doesnt pulled on changes in repo, so u must make changes in file **/webapp/index.html** when ansible-pull see changes in repo, changes in index.html will be attached to docker-container and after build image and run docker-compose, take place.

1. add changes to **webapp/index.html**

```
<h2>PLACE_ANY_TEXT</h2>
```

2. reorder variables from **How run example**.

3. push changes to repo

4. run command, but replace **PLACE_YOUR_SUDO_PASSWORD**, **PLACE_REPO_URL**

```
ansible-pull -o -U PLACE_REPO_URL -i hosts -e ansible_become_password=PLACE_YOUR_SUDO_PASSWORD
```

5. wait when container **apache_web** will running or watch logs file, because cronjob write logs.

Check

```
docker ps | grep apache_web
```

6. follow [link](http://localhost:8080/)

7. If all ok rm crontab

```
sudo crontab -u root -r
```

## Troubleshooting

1. If something goes wrong, just delete cron job and ansible-pull again

```
sudo crontab -u root -r

ansible-pull -o -U PLACE_REPO_URL -i hosts -e ansible_become_password=PLACE_YOUR_SUDO_PASSWORD

```
