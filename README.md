# amazee.io local Drupal Docker dev environment

This docker based Drupal Development environment consists of two parts:

### Part I: Shared Docker Containers

The shared docker containers for HAProxy and the SSH Agent, these are used by all other containers in order to properly work. They are started with the `docker-compose.yml` in the repo folder.

### Part II: Example Containers
Example files for Drupal development containers, these are made to be copied into a Drupal root directory and to be started from there.

## Prerequirements

- [docker-compose](https://docs.docker.com/compose/install/)
- OS X: [amazee.io cachalot](https://github.com/amazeeio/cachalot)

## Installation

- Clone this repo somehwere on your local computer
- Start the shared containers inside the cloned repo (they are defined that they automatically start themselves in the future)

	```
	docker-compose up -d
	```

## Usage of development containers

1. Choose the example yaml file you need, see the table at the bottom to choose
2. Copy the example file into your Drupal directory
3. Rename the file to `docker-compose.yml`
4. Edit the file according your needs, change at least the hostname. _Btw: It's perfectly fine to commit this file into your git repo, so others that are also using amazeeio-docker can use it as well._
5. Run `docker-compose up -d` in the same directory
6. Open your browser with the entered URL in the `docker-compose.yml`, happy Drupaling!

## Connect into container

To run commands like drush, git or other things within the container, you need to connect to the container.

	docker exec -itu drupal changeme.com bash

replace `changeme.com` with the docker container you want to connect to

## SSH Agent

Per default your SSH Key at `~/.ssh/id_rsa` is added to the Docker containers.

If you have a passphrase protected SSH key or need another SSH Key, run this command from the this directory (not inside the Drupal directory, also you don't need to do that for each Drupal site, just once)

	docker-compose run --rm ssh-agent_add_key ssh-add /ssh/id_rsa

replace `id_rsa` with the ssh private key from your `~/ssh/` folder you would like to add, `/ssh/` is mounted from `~/ssh/`

## Existing Docker Images

| Example File  | PHP  | Services | Description |
| ------------- | ------------- | ------------- | ------------- |
| `php70-basic` | 7.0 | nginx, varnish, mariadb | prefered for Drupal 8 |
| `php56-basic` | 5.6 | nginx, varnish, mariadb | prefered for Drupal 7 |
| `php70-composer` | 7.0 | nginx, varnish, mariadb | For [Drupal Composer Project](https://github.com/drupal-composer/drupal-project), the Drupal root expected in the folder `/web` |
| `php56-composer` | 5.6 | nginx, varnish, mariadb | For [Drupal Composer Project](https://github.com/drupal-composer/drupal-project), the Drupal root expected in the folder `/web` |

## Update Images

If you need to update the Docker Images to the newest version from the Docker Hub run:

	docker-compose pull
	docker-compose up -d