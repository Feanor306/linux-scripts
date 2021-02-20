## Install NVM
```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash  
```
  
=> Appending nvm source string to /home/feanor/.bashrc  
=> Appending bash_completion source string to /home/feanor/.bashrc  
=> Close and reopen your terminal to start using nvm or run the following to use it now:  
  
export NVM_DIR="$HOME/.config/nvm"  
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm  
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion  

## Config Git
```shell
git config --global user.email "my@email.com"  
git config --global user.name "myusername"
```

## Heroku cli
```shell
sudo curl https://cli-assets.heroku.com/install.sh | sh
```

## Install Rbenv
[rbenv AUR package](https://aur.archlinux.org/packages/rbenv/)  
[ruby-build AUR package](https://aur.archlinux.org/packages/ruby-build/)  
[rbenv github](https://github.com/rbenv/rbenv) 

```shell
rbenv init   
rbenv init -
```
```shell
rbenv install x.x.x (2.7.2)
rbenv local x.x.x
rbenv global x.x.x
```
## Install python & yarn
```shell
pacman -S python2  
pacman -S yarn  
```

## Install gems
```shell
gem install bundler
gem install nokogiri
gem install rails
```

## NVM AUR
[NVM AUR page](https://aur.archlinux.org/packages/nvm/)
```shell
echo 'source /usr/share/nvm/init-nvm.sh' >> ~/.bashrc
echo 'source /usr/share/nvm/init-nvm.sh' >> ~/.zshrc
```
```shell
nvm install node
```
## PostgreSQL
```shell
pacman -S postgresql postgresql-libs postgresql-runit
```
**Add a service:**
```shell
ln -s /etc/runit/sv/postgresql/ /etc/runit/runsvdir/current/
```
**login as postgres**
```shell
sudo -iu postgres
```
**init postgres database as postgres user**
```shell
initdb -D /var/lib/postgres/data
```
**check if postgres running**
```shell
ss -l | grep postgres
```
**Postgres Data location env var(in ~/.bashrc)**  
export PGDATA="/var/lib/postgres/data"  
  
**Make run folder!**  
```shell
su root
mkdir /run/postgresql
chown postgres:postgres /run/postgresql
```

**Attempt to auto create /run/postgresql folder**  
nvim|nano /etc/runit/sv/postgresq/run  
[ ! -d /run/postgresql ] && mkdir -m0755 -p /run/postgresql && chown postgres:postgres /run/postgresql  

**start DB server as postgres user**  
pg_ctl -D /var/lib/postgres/data -l logfile start  

**Check & start process**
```shell
sudo sv status postgresql
sudo sv start postgresql
```
**create postgres user as postgres user**  
sudo -u postgres createuser -s railsdevuser  
psql  
\password railsdevuser  
\q  

**new rails app with postgres**  
rails new TestApp -T -d postgresql  

**EDIT config/database.yml**  
```
default: &default
  ...
  host: localhost
  username: railsdevuser
  password: password
```