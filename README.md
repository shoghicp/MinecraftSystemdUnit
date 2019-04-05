# MinecraftSystemdUnit
Systemd Unit file for Minecraft Bedrock Server

## Installation
1. Connect to your (v)root server or if you want to run the server on your machine, open a terminal.<br />
2. Become root using su or sudo. To check if you are root run "echo $EUID" if it returns "0" you are root.<br />
3. Next install the necessary packages "apt install openjdk-8-jre-headless curl screen nano bash grep"<br />
4. Create the /opt folder if it doesn't already exist "mkdir /opt"<br />
5. Now you need to create the user for the service: "adduser --system --shell /bin/bash --home /opt/minecraft --group minecraft"<br />
6. Create the Systemd Unit file "nano /etc/systemd/system/minecraftbr@.service" : "curl https://raw.githubusercontent.com/shoghicp/MinecraftSystemdUnit/master/minecraft%40.service > /etc/systemd/system/minecraftbr@.service"<br />

## Setup Instance


## Usage
### Enable Autostart
<pre>systemctl enable minecraftbr@server</pre>
### Disable Autostart
<pre>systemctl disable minecraftbr@server</pre>
### Start Manually
<pre>systemctl start minecraftbr@server</pre>
### Stop Manually
<pre>systemctl stop minecraftbr@server</pre>
### Enter Server Commands
Entering commands into the console is somehow complicated thorugh the nature of systemd.<br />
So to enter the console "screen" is used (that's why it is in the script).<br />
<b>Note</b>: To detach (exit) screen press [STRG] + [A] followed by [D].<br />
<pre>
chmod 666 $(tty)
su -c "/usr/bin/screen -r" minecraft
chmod 430 $(tty)
</pre>
The first command allows otter users to read and write to your terminal.<br />
The second switches the user context to the minecraft service account.<br />
The last one restores the original terminal access rights for security. It is not very recommended to set the tty access to 666, but it seam to be the only way to enter a screen session within a su session.<br />
