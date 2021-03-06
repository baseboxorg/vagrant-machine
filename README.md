## Introduction

vagrant-machine builds an environment in your machine where you can install Ruby on Rails application without making any changes to your machine.

### Host machine vs Guest machine

In this README "host machine" will be used to refer to the native
machine on which vagrant is installed. Once you ssh into the vagrant
machine then that machine will be referred to as "guest machine"

## Using vagrant-machine

* 1. [Installing Dependencies](#installing-dependencies)
* 2. [Setting up machine using vagrant](#setting-up-the-guest-machine-using-vagrant)
* 3. [Using vagrant](#using-guest-machine)

### Installing Dependencies

Please install following tools

* [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* [Vagrant](http://www.vagrantup.com/downloads.html)
* [Ansible](http://docs.ansible.com/intro_installation.html)


#### Setting up the guest machine using vagrant

Before cloning `vagrant-machine` cd into the project directory.
Let's say that project directory is `wheel`.

```
cd wheel
git clone https://github.com/bigbinary/vagrant-machine.git
cp -rv vagrant-machine/* .
rm -rf vagrant-machine
```

* Open `provisioning/group_vars/all` and change the "name" and "email" value to
have your name and your email address.

* Open `provisioning/ruby/tasks/main.yml` and change the ruby verion. If
you need more than one ruby version then add another row.

After making the changes mentioned above execute following commnad. Please note that depending on your download speed it could take upto 15 mintues for the guest machine to be built. During the installation process you will see lots of outputs because the script has been set to super verbose mode to show all the data it can.

```
vagrant up
```

#### Using guest machine

Execute following commands to get into the guest machine.

```
vagrant ssh
```

Once you are inside the guest machine you will notice that the command prompt looks like this

```
vagrant ~
```

Notice that the prompt starts with `vagrant`. It means that you are in the guest machine.

In the host machine the directory that had `Vagrantfile` is mapped to
`/vagrant` in the guest machine.

```
cd /vagrant
gem install bundler
bundle install
```

### Start server

For starting the server do not use `rails server`. Use
command given below.

```
./bin/rails server -b 0.0.0.0
```

Now open browser and visit `http://localhost:3000`.


### Installations on the guest machine

* [rvm](http://rvm.io)
* [PostgreSQL](http://www.postgresql.org)
* [ImageMagick](http://www.imagemagick.org)
* [PhantomJS](http://phantomjs.org)
* [Node.js](http://nodejs.org)
* [curl](http://curl.haxx.se)
* [git](http://git-scm.com)
* [ack](http://beyondgrep.com)
* [tree](http://linux.die.net/man/1/tree)
* [git bash completion](https://github.com/git/git/blob/master/contrib/completion/git-completion.bash)
* [custom command prompt](https://github.com/neerajdotname/dotfiles/blob/master/bash/command_prompt.bash)
* [memcached](http://memcached.org)
* [bashmarks](https://github.com/huyng/bashmarks)
* [Heroku toolbelt](https://toolbelt.heroku.com)


### Verify that PostgreSQL is working

To test if postgresql is properly working execute following commands in the guest machine.

Note that password is blank for user postgres.

```
psql -h localhost -U postgres --password
enter password:
SELECT table_name FROM information_schema.tables WHERE table_schema='public';
```

You should see result with zero row. It means postgres is wroking fine. Now to exit out of `psql` type `\q` and hit enter.

```
postgres=# \q
```

#### Brought to you by

<a href='http://BigBinary.com'><img src="https://s3.amazonaws.com/bigbinary-media/horizontal/logo_blue.png" width="200px"/></a>
