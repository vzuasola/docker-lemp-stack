# Docker Lemp Stack

Is Windows slowing you down? Well this Docker stack won't.
`This does not work on Windows`

[How to run your own Elementary Workstation](docs/elementary.md)

# Features

* `Nginx` with exposed awesome vhost support
* `MariaDB` with data mounted on the folder (`say goodbye to missing DBs`)
* `Need to destroy your Docker stack, you keep all data, even your Databases`
* `Redis` with data mounted on the folder
* `PHP 7` with FPM
* Create instance from scratch for about 10 - 15 mins
* Up or halt the instance almost instantly (well 5 secs to be exact)

This stack was based from the [Laradock project](https://github.com/laradock/laradock).

# Getting Started

Pretty straightforward

* Clone this repository
* Copy `.env.example` to just `.env`
* See usage notes for command list

*Extra steps for Ubuntu users*

Ubuntu users are experiencing permission issues when mounting volumes, in order to fix that:
1. Open ~/.bashrc on terminal
2. sudo gedit ~/.bashrc
3. If a `umask` value is present, change it to `umask = 022`. Otherwise, add it to the end of the file.
4. Save and exit. Close your terminal.
5. Open terminal again and run `umask` command. You should get `022`.

> Note that this will only affect created files/folders moving forward, any existing files on the mounted directory should have read permission for owner.

# Usage

This Docker stack includes easy commands, so you do not need to remember the
commands to run or reload things.

If you edit vhosts, for example, you need to reload nginx. If you edit mariadb
settings, then you need to reload it.

* `./bin/start` Starts the stack
* `./bin/stop` Stops the stack
* `./bin/reload` Reloads everything, but does not recreate it
* `./bin/reload nginx` Recreates nginx instance
* `./bin/reload <service_name>` Recreates any service instance

# Notes for Webcomposer

Please check `docker-compose.yml` on the php-fpm extra host section. You might
need to adjust your extra hosts to match your custom host file for Drupal and
API layer.

Also give write permissions to cache, assets and logs folders as needed.

# FAQ

#### How does Docker mounting work ?

> On the `.env` file there is an `APPLICATION` variable which you can set manually to your desired projects folder (e.g /home/{username}/Projects).
> This gets mounted on the Docker workspace inside `/var/www` directory.

#### How to add new Nginx vhost ?

> Simply go to `./services/nginx/sites` as this folder gets mounted on the conf.d of nginx directly. After adding new sites, simply run `./bin/reload`

#### What folder path should I put on the vhost ?

> Suppose your project resides in `~/Projects/CMS/my-site` then your vhost entry should be `/var/www/CMS/my-site`

#### Configured vhost already but still the site cannot be reached ?

> Make sure to add your server name(s) on `etc/hosts` file (may require sudo privilege)

#### How to access DBs on my Drupal (or any PHP application)

> On your config, you can simply put `mariadb` as the hostname of your Database. Default username is `root` and password is `secret`

#### How to access DB using Workbench or SQLyog

> If you are on Windows, use the static IP and use port 3306. If within the VM, use the static IP defined on the `docker-compose` file

# Troubleshooting

* Destroy then initialize the machine
* If it does not solve your problem, Restart your PC 3 times
* If problems persist, fix it, or consult me (Alex)
# docker-lemp-stack
