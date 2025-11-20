## Worlds and plugins
The configs are made for the following mods/plugins and worlds:
https://drive.google.com/drive/folders/1czKvmVnBTjbTHoz5rtf03OnpBZqBnyVj?usp=drive_link

## Environment variables
Specify variables in `.env`.

- FORWARDING_SECRET: The secret used by Velocity proxy

## Adding a new server
Create a new service in `compose.yaml`:

```
services:
  ...
  example-server:
    image: itzg/minecraft-server:latest
    pull_policy: daily
    tty: true
    stdin_open: true
    environment:
      EULA: TRUE
      TYPE: "PAPER" # PAPER or FABRIC
      VERSION: 1.21.4 # Minecraft version
      ONLINE_MODE: false
    volumes:
      - ./servers/example-server:/data
```

Create the data folder `servers/example-server` and put `.gitignore.paper` inside of it, renaming it to `.gitignore`.

> Note: Make sure to add additional gitignore entries if needed (such as worlds or .jar files)

Inside `proxy/velocity.toml`, add the service as a server.

Run the server to generate files.

Edit the `velocity` entry inside `servers/example-server/config/paper-global.yml` to the following:

```
  velocity:
    enabled: true
    online-mode: true
    secret: ${FORWARDING_SECRET}
```

And you should be done!

## TODO
- Automatic mod and plugin downloads
- Import worlds from `worlds` directory
