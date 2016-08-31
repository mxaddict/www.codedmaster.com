---
layout: post
title: Getting latest NVIDIA drivers and Vulkan support for Ubuntu 16.04
---

Sometimes the [NVIDIA][nvidia] drivers on LTS [Ubuntu][ubuntu] Releases are not the best, sometimes they are good, but old. If you want to have access to the new BETA drivers plus Vulkan support on [Ubuntu][ubuntu] 16.04 this tutorial is for you.

You will need to add the PPA Repo to get access to these packages:

```bash
sudo add-apt-repository ppa:graphics-drivers/ppa
```

Then you will need to do an update to get the latest package references in apt:

```bash
sudo apt update
```

Once done with the update, you can install the latest [NVIDIA][nvidia] driver like so:

```bash
sudo apt install nvidia-370 -y
```

NOTE: At the time of writing, `nvidia-370` package is the latest BETA driver

To check if you have [Vulkan][vulkan] working correctly you will need `vulkan-utils` package:

```bash
sudo apt install vulkan-utils -y
```

Then run the `vulkaninfo` command to check which version is installed:

```bash
vulkaninfo | grep "Version"
```

You should see something like the following:

```bash
Vulkan API Version: 1.0.21
        apiVersion     = 0x40000d  (1.0.13)
        driverVersion  = 1552269312 (0x5c85c000)
```

NOTE: If [Vulkan][vulkan] is not working after the install, you might have to do a simple system reboot, which you can do via the terminal with `sudo reboot`

## Optional

If you have [Dota 2][dota2] on your machine, you can use it to check for [Vulkan][vulkan].

You will need to open [Steam][steam] and enable [Vulkan][vulkan] for [Dota 2][dota2]

![Screenshot](/public/img/vulkan_steam_dota2_01.png)

Just set the following launch option value:

![Screenshot](/public/img/vulkan_steam_dota2_02.png)
![Screenshot](/public/img/vulkan_steam_dota2_03.png)
![Screenshot](/public/img/vulkan_steam_dota2_04.png)

Then run [Dota 2][dota2], if it works then you have [Vulkan][vulkan] setup correctly!

## Conclusion

As of the writing of this article, this method is the easiest way to get the latest [NVIDIA][nvidia] driver with [Vulkan][vulkan] support, so If you are reading this in the future, which I damn sure hope so, there may already be Vulkan support on the default [Ubuntu][ubuntu] package repos.

[ubuntu_ppa_graphics]: https://launchpad.net/~graphics-drivers/+archive/ubuntu/ppa
{:target="_blank"}

[ubuntu]: http://www.ubuntu.com/
{:target="_blank"}

[nvidia]: http://www.nvidia.com/
{:target="_blank"}

[steam]: http://store.steampowered.com/
{:target="_blank"}

[dota2]: http://blog.dota2.com/
{:target="_blank"}

[vulkan]: https://www.khronos.org/vulkan/
{:target="_blank"}
