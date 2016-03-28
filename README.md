# AmazeeIO Local Drupal Docker Environment

## Prerequirements

- [AmazeeIO Cachalot](https://github.com/AmazeeIO/cachalot)
- docker compose

## Configuration

- Edit `docker-compose.yml` to your needs

## Usage

- `docker-compose up -d`

## Connect into container

- `docker exec -itu drupal asdf_com bash` (replace `asdf_com` with the docker container you want to connect to)

## SSH Agent

Per default your SSH Key at `~/.ssh/id_rsa` is added to the Docker containers.

If you have a passphrase protected SSH key or need another SSH Key, run:

`docker-compose run ssh-agent_add_key ssh-add /ssh/id_rsa` (replace `id_rsa` with the ssh private key you would like to add)