# Pi-hole

This is my personal [Pi-hole](https://pi-hole.net/) setup. It's a Raspberry Pi running Raspbian,
with Tailscale running on the host and Pi-hole running in a Docker container.

## Installing

1. Install [Tailscale](https://tailscale.com/kb/1174/install-debian-bookworm). Ensure when you
run `tailscale up` you are passing in the additional `--accept-dns=false` flag to ensure the
Pi-hole can make upstream DNS queries:
```
tailscale up --accept-dns=false
```

2. Create an `.env` file containing the admin password for the Pi-hole in the same directory as
`docker-compose.yml`:
```
echo "PIHOLE_PASSWORD=<password>" > .env
```

3. Run `docker compose` to start the Pi-hole docker container:
```
DOCKER_HOST="ssh://<user>@<ip>" docker compose up -d
```

Replace <user> and <ip> with the user and IP of your Raspberry Pi.

4. If everything works, you should be able to navigate to `http://<ip>/admin` and log into the
Pi-hole dashboard using the password you configured in (2).

## Resources

[Tailscale: Access a Pi-hole from anywhere](https://tailscale.com/kb/1114/pi-hole)
