
## Install SteamCMD and dependencies
sudo pacman -S steamcmd lib32-gcc-libs lib32-glibc

## Mod for tournaments
https://github.com/splewis/get5

## Mods folder
cs2-server/game/csgo/addons/sourcemod/plugins

## move player to 




## Run the steamcmd docker
```sh
mkdir -p ./cs2-server
docker run \
    -v ./cs2-server:/home/steam/cs2 \
    -p 27015:27015/udp \
    -p 27020:27020/udp \
    --rm -it --name steamcmd cm2network/steamcmd bash
```

## Install csgo server
```sh
./steamcmd.sh \
    +force_install_dir /home/steam/cs2 \
    +login anonymous \
    +app_update 740 validate \
    +quit

# a small hack; need to build into my own dockerfile
mv /home/steam/cs2/bin/libgcc_s.so.1 /home/steam/cs2/bin/libgcc_s.so.1.bak

export export LD_LIBRARY_PATH=/home/steam/cs2/bin
~/cs2/srcds_linux -game csgo -console -usercon +map de_dust2 +sv_lan 1
```

