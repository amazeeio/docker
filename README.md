# amazee.io Local Drupal Docker Environment

This docker based Drupal Development environment consists of two parts:
1. The shared docker containers for HAProxy and the SSH Agent, these are used by all other containers in order to properly work. They are started with the `docker-compose.yml` in the root folder
2. Separate `docker-compose.yml` files for each site, these can be either copied directly into a Drupal site and started there or started directly from here

## Prerequirements

- [amazee.io Cachalot](https://github.com/AmazeeIO/cachalot)
- [docker-compose](https://docs.docker.com/compose/install/)

## Start

First start the shared containers with:

- `docker-compose up -d`

## Usage

1. Copy the `docker-compose.yml` from the example folders into your Drupal directory and run `docker-compose up -d` in this directory.
2. Edit the `docker-compose.yml` according your needs, the file is documented. Btw: It's perfectly fine to commit this file into your git repo, so others that are also using amazeeio-docker can use it as well.
3. Open your browser with the entered URL in the `docker-compose.yml`, happy Drupaling!

## Connect into container

To run commands like drush, git or other things within the container, you need to connect to the container.

Regularly you would do that via SSH, but we're using the docker internal things here:

- `docker exec -itu drupal asdf_com bash` (replace `asdf_com` with the docker container you want to connect to)

## SSH Agent

Per default your SSH Key at `~/.ssh/id_rsa` is added to the Docker containers.

If you have a passphrase protected SSH key or need another SSH Key, run this command from the this directory (not inside the Drupal directory, also you don't need to do that for each Drupal site, just once)

`docker-compose run --rm ssh-agent_add_key ssh-add /ssh/id_rsa` (replace `id_rsa` with the ssh private key you would like to add)