---
layout: post
title: Setup TOR on Ubuntu 16.04?
---

[Tor][tor] is a open source, open networking tool that allows you to surf the web with better anonymity, it is basically a free and open proxy type networking tool that will allow you to surf the web from other network nodes. From there [site](https://www.torproject.org/):

  > Tor is free software and an open network that helps you defend against traffic analysis, a form of network surveillance that threatens personal freedom and privacy, confidential business activities and relationships, and state security.

It's an immensely useful tool and one we encourage you to use if you want to be safer on the web.

Basic install for [Ubuntu][ubuntu] is as follows:

```bash
sudo apt install tor torbrowser-launcher -y
```

After installing it, the tor service should be up and running, which you can check with:

```bash
sudo service tor status
```

That should give you a similar output to the following:

```bash
● tor.service - Anonymizing overlay network for TCP (multi-instance-master)
   Loaded: loaded (/lib/systemd/system/tor.service; enabled; vendor preset: enabled)
   Active: active (exited) since Mon 2016-08-22 20:58:25 PHT; 4h 25min ago
  Process: 3129 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
 Main PID: 3129 (code=exited, status=0/SUCCESS)
    Tasks: 0
   Memory: 0B
      CPU: 0
   CGroup: /system.slice/tor.service

Aug 22 20:58:25 system-hostname systemd[1]: Starting Anonymizing overlay network for TCP (multi-instance-master)...
Aug 22 20:58:25 system-hostname systemd[1]: Started Anonymizing overlay network for TCP (multi-instance-master).
```

Now if for some weird reason the service is not started, just run this:

```bash
sudo service tor start
```

Once you know you have the service running, then you should find that you can use the torbrowser-launcher to download and install the [Tor][tor] Browser, either open it from your application launcher, or run it from a terminal:

```bash
torbrowser-launcher
```

After running that command you will get output in the terminal similar to the following before the browser actually loads up:

```bash
Tor Browser Launcher
By Micah Lee, licensed under MIT
version 0.2.4
https://github.com/micahflee/torbrowser-launcher
Launching './Browser/start-tor-browser --detach'...
```

Using the tor browser is the fastest way to get HTTP/HTTPS access using the [Tor][tor] Network.

If you want, you can run most terminal commands using [Tor][tor] to anonymize it's traffic, for example, you could run something as simple as an ssh connection using [Tor][tor] with the `torsocks` command:

```bash
torsocks ssh someone@somewhere.tld -p 2222
```

## Conclusion

[Tor][tor] might sound scary, but I assure it, it's much simpler than you might think, I hope you can use this info as a starting point to your [Tor][tor] powered adventure browsing, good luck and have fun. Peace!

[tor]:    https://www.torproject.org/
[ubuntu]: http://www.ubuntu.com/
