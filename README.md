# Dot Net 7 with the Raspberry Pi

This is the source code to accompany my talk on Microsoft .NET 7 with the Raspberry Pi.

Talk details, slides and a blog are incoming!

Tested on a Raspberry Pi 3B+ / Raspberry Pi Zero 2W and a Raspberry Pi 4

Any Queries, contact me at;

https://www.petecodes.co.uk/contact/

Pete Gallagher / Pete Codes / PJG Creations 2022

# Blog Post

You can read the accompanying blog post for this repository here;

[Install and use .NET 7 with the Raspberry Pi](http://bit.ly/dotnet7pi)

# .NET 7 Installation on a Raspberry Pi

You can install Dot Net 7 on the Raspberry Pi in one command by executing;

```
wget -O - https://raw.githubusercontent.com/pjgpetecodes/dotnet7pi/master/install.sh | sudo bash
```

You can see a run through of the installation here;

![Image](/assets/install.gif "Installation")

# Local Install Script

If you've cloned this repo, you can install Dot Net 7 by running the following in the root of the repo;

```
sudo chmod +x install.sh
sudo ./install.sh 

```

# PC Setup

Download the latest version of the .NET framework for your system from here;

https://dotnet.microsoft.com/download/dotnet/7.0

# Other Devices

## ODroid HC4

This script has been tentatively tested on an ODroid HC4, which has an ARM Cortex A55 which is an ARMv8 Processor. The script installs correctly, however the GPIO functionality hasn't been tested yet.

The .NET GPIO Nuget Package supports the Odroid Devices according to the documentation, so it should be fine to use.

If you have one of these devices and get it working, do get in touch by tweeting me [@pete_codes](https://www.twitter.com/pete_codes)!

# Remote Deployment and Debugging

If you'd like to be able to write code on your PC and then Deploy and Debug that code directly on a Raspberry Pi, then I've create a one line script to set that up;

```
curl --output remotedebugsetup.bat https://raw.githubusercontent.com/pjgpetecodes/dotnet7pi/master/remotedebugsetup.bat && remotedebugsetup.bat
```

You can read more about this in a blog post here;

http://bit.ly/piremotedeployanddebug


# Setup PC for Remote Deployment and Debugging an Uno Application

If you'd like to be able to Create an Uno Platform Application on your PC and then Deploy and Debug that code directly on a Raspberry Pi, then I've create a one line script to set that up;

```
curl --output remotedebugsetup_uno.bat https://raw.githubusercontent.com/pjgpetecodes/dotnet7pi/master/remotedebugsetup_uno.bat && remotedebugsetup_uno.bat
```

You can read more about this in a blog post here;

http://bit.ly/piremotedeployanddebuguno

# IoT Hub Connection

The 3 IoT Hub Based Examples will require an IoT Hub Device Primary Connection String to work. 

# Deploying from VS Code on Windows

If you want to Deploy from VSCode on a Windows PC, then modify the RaspberryDeployWSL task's ```rsync``` command in the ```.vscode/tasks.json``` files in the various projects to point to your Pi IP Address;

```
"'sshpass -p \"raspberry\" rsync -rvuz $(wslpath '\"'${workspaceFolder}'\"')/bin/linux-arm/publish/ pi@[Enter Your IP Address]:share/${workspaceFolderBasename}/'"
```

Replace the ```[Enter Your IP Address]``` Section with the IP Address of your Pi (No Square Brackets!).

You will also need to change the username (```pi@```) and password (```-p \"raspberry"```) if you have altered those too.

# Debugging from VS Code on Windows

If you want to Debug from VSCode on a Windows PC, then modify the ```.NET Core Launch Console``` task in the ```.vscode/launch.json``` files in the various projects to point to your Pi's Hostname;

```
"pipeArgs": [
    "-pw",
    "raspberry",
    "root@[Your Pi Hostname].local"
],
```

You'll also need to install the VS Debugger;

```
curl -sSL https://aka.ms/getvsdbgsh | bash /dev/stdin -r linux-arm -v latest -l ~/vsdbg
```

You may also need to install curl and zip if they're not already installed;

```
sudo apt-get install curl
```