# bafserve
An optimised, auto-updating modpack, for Fabric 1.18.2 servers.

I've been getting pretty tired of having to update all the mods I use on my server one by one. So I made this little pack.
As I use a Raspberry Pi 4 for my own server, this pack is intended to be highly optimised for low spec machines.
Feel free to fork or modify anything here, and I'm open to hearing out any mod suggestions anyone might have.

**None** of these mods are my own. I'm not smart enough for that. They're all just ones that I really like!
## By the grace of god, I love it, what mods are included?
### Super Speed Server Mods
* Lithium
* Starlight
* Server Core
* FerriteCore
* Krypton
* LazyDFU
* C2ME
* Alternate Current
* Very Many Players
### Actually The Best
* Xearos Worldmap
* Universal Graves
* Gimme Bundles!
* RPG Stats
* Wandering Collector
### Useful Things
* Spark
* EditSign
### This Thing (Again)
* Fabric API
## That's peachy, now how do I use it?
Well, I'm not quite sure if it's the best way, but I just launch my server with this pack using this little script.

Not just will it **automatically restart** your server in the even of a crash, it also uses **Aikar's flags** for even more speed!

You'll also have to download, and then drop [**this thingamajig**](https://github.com/packwiz/packwiz-installer-bootstrap) into your server's directory.
```
#!/bin/sh
while true
do
java -jar packwiz-installer-bootstrap.jar -g -s server https://raw.githubusercontent.com/Regular-Baf/bafserve/main/pack.toml
wait
java -Xms6656M -Xmx6656M -XX:+UseG1GC -XX:+ParallelRefProcEnabled -XX:MaxGCPauseMillis=200 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=30 -XX:G1MaxNewSizePercent=40 -XX:G1HeapRegionSize=8M -XX:G1ReservePercent=20 -XX:G1HeapWastePercent=5 -XX:G1MixedGCCountTarget=4 -XX:InitiatingHeapOccupancyPercent=15 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=5 -XX:SurvivorRatio=32 -XX:+PerfDisableSharedMem -XX:MaxTenuringThreshold=1 -Dusing.aikars.flags=https://mcflags.emc.gs -Daikars.new.flags=true -jar server.jar nogui
echo "To stop the server from restarting, press Ctrl+C now."
echo "Restarting in:"
for i in 5 4 3 2 1
do
echo "$i..."
sleep 1
done
echo "Restarting now!"
done
```
**Don't forget** to make sure that you adjust the values for memory, as well as add the the name of your server.jar.
