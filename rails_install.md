## Install NVM
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash

=> Appending nvm source string to /home/feanor/.bashrc
=> Appending bash_completion source string to /home/feanor/.bashrc
=> Close and reopen your terminal to start using nvm or run the following to use it now:

export NVM_DIR="$HOME/.config/nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

## Config Git
git config --global user.email "feanor306@live.com"
git config --global user.name "Feanor306"

## Heroku cli
sudo curl https://cli-assets.heroku.com/install.sh | sh

## Install Rbenv
https://aur.archlinux.org/packages/rbenv/
https://aur.archlinux.org/packages/ruby-build/
https://wiki.archlinux.org/index.php/Arch_User_Repository#Installing_and_upgrading_packages
https://github.com/rbenv/rbenv

rbenv init 
rbenv init -

rbenv install x.x.x (2.7.2)
rbenv local x.x.x
rbenv global x.x.x

## Install python & yarn
pacman -S python2
pacman -S yarn

## Install gems
gem install bundler
gem install nokogiri
gem install rails

## NVM AUR
https://aur.archlinux.org/packages/nvm/
echo 'source /usr/share/nvm/init-nvm.sh' >> ~/.bashrc
echo 'source /usr/share/nvm/init-nvm.sh' >> ~/.zshrc

nvm install node

## PostgreSQL
pacman -S postgresql postgresql-libs postgresql-runit

**Add a service:**
ln -s /etc/runit/sv/postgresql/ /etc/runit/runsvdir/current/

**login as postgres**
sudo -iu postgres

**init postgres database as postgres user**
initdb -D /var/lib/postgres/data

**check if postgres running**
ss -l | grep postgres

**Postgres Data location env var(in ~/.bashrc)**
export PGDATA="/var/lib/postgres/data"

**Make run folder!**
su root
mkdir /run/postgresql
chown postgres:postgres /run/postgresql

**Attempt to auto create /run/postgresql folder**
nvim|nano /etc/runit/sv/postgresq/run
[ ! -d /run/postgresql ] && mkdir -m0755 -p /run/postgresql && chown postgres:postgres /run/postgresql

**start DB server as postgres user**
pg_ctl -D /var/lib/postgres/data -l logfile start

**Check & start process**
sudo sv status postgresql
sudo sv start postgresql

**create postgres user as postgres user**
sudo -u postgres createuser -s railsdevuser
psql
\password railsdevuser
\q

**new rails app with postgres**
rails new TestApp -T -d postgresql

**EDIT config/database.yml**
default: &default
  ...
  host: localhost
  username: railsdevuser
  password: password