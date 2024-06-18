
# Raspberry Pi Computer Summative

## Raspberry Pi into minecraft java server

Links  
- [text](https://www.hanselman.com/blog/how-to-use-a-raspberry-pi-4-as-a-minecraft-java-server)
- [Turn your Raspberry Pi into a Minecraft java server](https://www.youtube.com/watch?v=u2DnafpNQW8)
- [chatGPT](https://chatgpt.com/share/0ec36c9d-0db2-4c6b-9972-68e99b3723a7)

## Setup

First things first you need to update/upgrade you `Raspberry Pi`
run the following command

```
sudo apt update
sudo apt upgrade
sudo apt install default-jdk
```

Next you need to download the [Minecraft_server.1.21.jar](https://www.minecraft.net/en-us/download/server) file from minecrafts website (note: the version number of minecraft will change with updates) 

after installing the minecraftserver.jar file you need to run the following command



```
cd ~
mkdir MinecraftServer
cd MinecraftServer
wget https://launcher.mojang.com/v1/objects/c5f6fb23c3876461d46ec380421e42b289789530/server.jar
java -Xmx1000M -Xms1000M -jar server.jar nogui
```

After this step you will need to accept the EULA agreenment, so you need to open the "nano eula.txt" file and set `eula=true` then press ctrl-x and save the file, Then run the above command again with the up arrow.  

if you want to use a differnt version of minecraft you will need to dowwlaod the jar file for the verison you want.

if you have a differnt version you need to do the following command (Note you will need to add your file path to the jar file.
)
```
cd ~
mkdir MinecraftServer
cd MinecraftServer
cp C:\your\file\path\server-1-8-9.jar ./server.jar
java -Xmx1000M -Xms1000M -jar server.jar nogui
```

## connecting to Minecraft Server 

Run `ifconfig` to get your Raspberry Pi's **IVP4 Pi address**. After you can open minecraft and then you can open minecraft java edition press **multiplayer button** then press **add server** after type in the name for the server and then the **IVP4 IP address** for the RaspBerry Pi.

## Editing Server Properties

If you want to change the default settings of the minecrafter server you need to `nano server.properties` you can edit settings like: 

- server port (what port the server runs on)
- max players (how many players are allowed on the server at one time)
- game mode (what gamemode you start in)

### port Forwarding 
If you want other people to connect to the server outside of your network you need to setup port forwarding on your router. You need to forward Minecraft port (defuault port is 25565) to your Raspberry Pi.

## Auto Server startup Script 

First you need to create a script to start the server. Type `nano start.sh` where you want to file to be made (I.E. cd Desktop).

add the follow lines to the script file you just made 
```
#!/bin/bash
cd ~/minecraft
java -Xmx1000M -Xms1000M -jar server.jar nogui
```

save the following lines the make the script a exeutable with the following line

```
chmod +x start.sh
```

you can setup a cron job to start the server on boot with the following line.
```
crontab -e
```

after the panel is open add the following lines. 
```
@reboot /home/pi/minecraft/start.sh
```
