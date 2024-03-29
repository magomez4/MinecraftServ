# Followed this tutorial to install/run/setup minecraft server:
https://www.tomshardware.com/how-to/raspberry-pi-minecraft-server
I modified the auto-start bash script. Instead of re-running every 10 seconds, it runs only once at startup. If it ever crashes, the raspberry pi would have to be reboot or re-run the command below manually from the minecraft screen (see reference below on how to use `screen` program). 

# To update minecraft server:
Folloed this tutorial: https://wiki.sportskeeda.com/minecraft/how-to-update-server-minecraft#:~:text=To%20update%20a%20server%20in%20Minecraft%2C%20create%20a%20new%20folder,executable%20into%20the%20old%20folder

# To run minecraft server:
java -Xmx1024M -Xms1024M -jar server.jar

# Top stop minecraft server:
Attach to the minecraft command line screen and run `\stop`

# To attach to minecraft server screen:
screen -r minecraft_screen
## To detach:
`ctrl-a d` (let go of ctrl-a before pressing d)


# General Notes
For minecraft server version 1.20.2, I had to install java 17

## To intall java 17:

Vanilla java 17 only works on 64 bit systems, so I had to install a port of java 17 that was built for 32 bit systems. 

I used the command described in this reddit post to install a 32 bit version of java 17 : 

https://www.reddit.com/r/raspberry_pi/comments/r677q9/installing_java_17_on_pi_4/

here is the command set:
```
wget https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.1%2B12/OpenJDK17U-jdk_arm_linux_hotspot_17.0.1_12.tar.gz

tar xzfv OpenJDK17U-jdk_arm_linux_hotspot_17.0.1_12.tar.gz

./jdk-17.0.1+12/bin/java -version
```

I put the downloaded file inside my ~/Downloads folder.

After that, I followed this list of commands of this link (also mentioned in reddit), to install and select java 17 as the current java being used:
https://gist.github.com/filipelenfers/ef3f593deb0751944bb54b744bcac074

Here is the command set:
```
#Login as root
sudo su

#create jdk directory
mkdir /opt/jdk

#uncompress, change to your file name
tar -zxf jdk-8u5-linux-x64.tar.gz -C /opt/jdk

#check if files are there
#ls /opt/jdk

#update alternatives so the command java point to the new jdk 
update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.8.0_05/bin/java 100


#update alternatives so the command javac point to the new jdk 
update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk1.8.0_05/bin/javac 100

#check if java command is pointing to " link currently points to /opt/jdk/jdk1.8.0_05/bin/java"
update-alternatives --display java

#check if java command is pointing to " link currently points to /opt/jdk/jdk1.8.0_05/bin/javac"
update-alternatives --display javac

#check if java is running
java -version
```

