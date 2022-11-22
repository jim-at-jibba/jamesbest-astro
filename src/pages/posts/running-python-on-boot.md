---
slug: "/running-a-python-script-on-boot-on-a-rpi"
title: "Running a python script on boot on a RPi"
desscription: "I wanted to run a python script with my Raspberry Pi first booted. Here is how I did it."
pubDate: "2019-10-14"
hero: "../images/posts/python-on-boot/python-on-boot-header.jpg"
tags: ["maker", "python", "raspberry-pi"]
layout: "../../layouts/BlogPostLayout.astro"
---

Once you are able to successfully run your python script from the terminal, what are your options to run the same script on booting the Raspberry Pi? This post details the issues I had getting my scripts to run on boot and how I fixed them.

**TL;DR** Make sure you are running your scripts as the correct user. Python scripts that use Pip packages will need to be run as the user used to install said packages or else they might not be available.

Writing python scripts is a relatively new thing for me. I love playing with the Raspberry Pi and generally write Nodejs. For most of the stuff I have been doing up until this point, Nodejs has been fine. But the Raspberry Pi is blessed with a wealth of hats performing a multitude of weird and wonderful things. The problem is that most of the libraries for these hats are written in Python. So I thought it was about time I start learning some python.

My first python script was controlling the Mote LEDs through MQTT. Writing the script did not take too long as the examples in the Pimoroni repos gave me enough to get started. I was able to run the script from the terminal and had it working fine. Obviously, we don't want to have a terminal session open all the time and we want to have the script start on boot (or reboot).

I had read that there are a number of ways to run a script on boot but that the preferred way was to add an entry into the `/etc/rc.local` file. This file is loaded when the Pi is booted and so should achieve our goal.

Have you ever seen the IP of the Pi print in the terminal output when the Pi is booting? This is where that command is run from.

So I added the following line to the file:

```bash
/usr/bin/python3 /home/pi/Code/desklights/desklights.py
```

and rebooted the Pi. Nothing! No logs, no error. Nothing! Very unhelpful. I tried every possible way of calling the script. And each one proved fruitless. Nothing.

What I needed was to see so sort of log output. I hoped that this would give me an idea of what was wrong. I updated the command to the following:

```bash
/usr/bin/python3 /home/pi/Code/desklights/desklights.py > /tmp/desklights.out > /tmp/desklights.err
```

This would write anything logging from the program to `/tmp/desklights.out` and and errors to `/tmp/desklights/err`. This was a key to solving the issue. The _.out file was empty which indicated the script was failing. The `_.err` file, on the other hand, contained this:

![Alt Text](https://thepracticaldev.s3.amazonaws.com/i/3g93i5dwvjay78yito7z.png)

It was now clear what I needed to do. The python packages I had installed were install using the Pi user. This file runs as root and so does not have access to the installed packages. I need to make sure I am running my script as the Pi user and all should be fine and dandy.

```bash
sudo -H -u pi /usr/bin/python3 /home/pi/Code/desklights/desklights.py/home/pi/Code/desklights/desklights.py
```

Updating the script to include the change of user fixed my issue and allowed the script to run successfully on boot.

Thanks for reading 🙏
