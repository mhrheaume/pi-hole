# Pi-hole

This is my personal [Pi-hole](https://pi-hole.net/) setup. It's a Raspberry Pi running Raspbian,
with Tailscale running on the host and Pi-hole running in a Docker container.

## Installing

Start by SSHing into the Raspberry Pi and installing dependencies:

1. Install [Tailscale](https://tailscale.com/kb/1174/install-debian-bookworm). Ensure when you
run `tailscale up` you are passing in the additional `--accept-dns=false` flag to ensure the
Pi-hole can make upstream DNS queries:
```
tailscale up --accept-dns=false
```

2. Install [Docker](https://docs.docker.com/engine/install/debian/) using the apt repository. Also
make sure to grant your user permission to
[Manage Docker](https://docs.docker.com/engine/install/linux-postinstall/#manage-docker-as-a-non-root-user).

Now, back on the host where this repository has been checked out, you can orchestrate the Pi-hole
installation:

3. Create an `.env` file containing the admin password for the Pi-hole in the same directory as
`docker-compose.yml`:
```
echo "PIHOLE_PASSWORD=<password>" > .env
```

4. Run `docker compose` to start the Pi-hole Docker container:
```
DOCKER_HOST="ssh://<user>@<ip>" docker compose up -d
```

Replace `<user>` and `<ip>` with the user and IP of your Raspberry Pi.

5. If everything works, you should be able to navigate to `http://<ip>/admin` and log into the
Pi-hole dashboard using the password you configured in (3).

## Resources

[Tailscale: Access a Pi-hole from anywhere](https://tailscale.com/kb/1114/pi-hole)
