# BafServe 2
An optimised, auto-updating modpack, for Fabric 1.19.2 servers.

I've been getting pretty tired of having to update all the mods I use on my server one by one. So I made this little pack.
As I use a Raspberry Pi 4 for my own server, this pack is intended to be highly optimised for low spec machines.
Feel free to fork or modify anything here, and I'm open to hearing out any mod suggestions anyone might have.

**None** of these mods are my own. I'm not smart enough for that. They're all just ones that I really like!
## By the grace of god, I love it, what mods are included?
### Super Speed Server Mods
* Lithium
* Starlight
* FerriteCore
* Krypton
* Server Core
* LazyDFU
* C2ME
* Fastload
* Very Many Players
* Memory Leak Fix
* Dimensional Threading
* Alternate Current
### Other Useful Things
* No Chat Reports
* Universal Graves
* EditSign
* RPG Stats
* Wandering Collector
### These Things
* Fabric API
* YetAnotherConfigLib
## That's peachy, now how do I use it?
Well, I'm not quite sure if it's the best way, but I just launch my server with this pack using this little script.

Not just will it **automatically restart** your server in the event of a crash, it also uses [these flags](https://github.com/brucethemoose/Minecraft-Performance-Flags-Benchmarks#server-g1gc) for even more speed!

You'll also have to download, and then drop [this thingamajig](https://github.com/packwiz/packwiz-installer-bootstrap) into your server's directory.
```
#!/bin/sh
while true
do
java -jar packwiz-installer-bootstrap.jar -g -s server https://raw.githubusercontent.com/Regular-Baf/BafServe/main/pack.toml
wait
java -Xms6656M -Xmx6656M -XX:+UseG1GC -XX:MaxGCPauseMillis=130 -XX:+UnlockExperimentalVMOptions -XX:+DisableExplicitGC -XX:+AlwaysPreTouch -XX:G1NewSizePercent=28 -XX:G1HeapRegionSize=16M -XX:G1ReservePercent=20 -XX:G1MixedGCCountTarget=3 -XX:InitiatingHeapOccupancyPercent=10 -XX:G1MixedGCLiveThresholdPercent=90 -XX:G1RSetUpdatingPauseTimePercent=0 -XX:SurvivorRatio=32 -XX:MaxTenuringThreshold=1 -XX:G1SATBBufferEnqueueingThresholdPercent=30 -XX:G1ConcMarkStepDurationMillis=5 -XX:G1ConcRSHotCardLimit=16 -XX:G1ConcRefinementServiceIntervalMillis=150 -jar server.jar nogui
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
