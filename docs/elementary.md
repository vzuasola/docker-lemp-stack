![](https://raw.githubusercontent.com/elementary/website/master/_images/logotype.png)

# Elementary VM

This is the future. This is `innovation`

### Why work on a VM

* Fast
* No Windows
* Workspace support
* Native linux commands
* Native Docker support
* Fast
* Not Windows

## Prerequisites

* 16 GB of RAM
* SSD
* i7 processor
* At least VMware player 14 with latest VMware linux tools

> Please request for the lastest VMware Player if you don't have at least version 14. This stack is thoroughly tested using VMware Player 14

## Features

* Material Sublime with lots of useful plugins
* Linter support for PHP and JS for Sublime
* Native PHP 7.1
* Native Node
* Docker engine + CLI
* Elementary Tweaks
* DNSmasq setup

## Setup Guide

* Copy the `Elementary OS` folder from here `\\ph.esl-asia.com\shares\IT\elementary` to your local filesystem
* Open VMware and click `Open existing machine`
* Point to the `vmdk` file
* Run the machine
* Select `"I Copied It"` option when prompted
* Default password is `pass123`

## Post Setup

* Setup your SSH key for our Gitlab. It is recommended to setup a new SSH key for your local VM and put it on Gitlab
* Checkout the [Docker Lemp Stack](https://gitlab.ph.esl-asia.com/CMS/docker-lemp-stack) and start it
* You can now start migrating your repositories

## Setup Verification Guide

> Please do this step as this is important, this make sure that everything works as expected

1. Check if VM can accomodate full monitor resolution
2. Add new SSH key to Gitlab
3. Git clone that master branch of https://gitlab.ph.esl-asia.com/CMS/docker-lemp-stack, `please read extensively the docker stack setup guide`
4. Run the docker using the start command
5. Check if you can access `laravel.dev` on your VM chrome

# Miscellaneous

## Accessing your site on Windows

To access your hosted sites on Windows, you need to assign a static IP for your Virtual Machine

* On the status bar, click on the Network Icon and go to `Network Settings`
* You should see the IP Address of your Ethernet adapter
* Add a host file on Windows referencing to that IP Address

## Sublime Text 3 Plugins

* Advanced New File
* Material Theme
* PHP Companion
* PHP-Twig
* Sass
* SidebarEnhancements
* SublimeLinter-contrib-eslint
* SublimeLinter-php
* SublimeLinter-phpcs

# Troubleshooting

#### Network does not work
> Simply disconnect the network from the status bar. If problem persist, open `Edit Connection` and delete all networks under ethernet

#### Screen get stuck at certain resolution
> Simply exit fullscreen, un-maximize then go to fullscreen again

Sometimes restarting your VM (and your PC) solves most of the common (and sometimes weird) problems

# Special Thanks

Brader for beta testing the VM