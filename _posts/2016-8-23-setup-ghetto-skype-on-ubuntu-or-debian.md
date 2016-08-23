---
layout: post
title: Setup Ghetto Skype on Ubuntu/Debian?
---

[Ghetto Skype][skype_ghetto] is an open source desktop application powered by [Electron][electron] which acts as the wrapper for the [Web Skype][skype_web] beta that Microsoft has been working on. A quote from the [Ghetto Skype][skype_ghetto] README.md file:

  > Are you tired of a buggy 32 bit official Skype client? Then Ghetto Skype is for you!

Setup is easy, basically we need to download it like so:

```bash
# Assuming you are using 64 bit Ubuntu/Debian
wget https://github.com/stanfieldr/ghetto-skype/releases/download/v1.4.1/ghetto-skype_1.4.1_amd64.deb
```

NOTE: you can check for the other versions of [Ghetto Skype][skype_ghetto] on it's [releases page](https://github.com/stanfieldr/ghetto-skype/releases){:target="_blank"}

After the download has completed successfully, we should do a checksum to make sure it's not corrupted or anything.

```bash
md5sum ghetto-skype_1.4.1_amd64.deb
```

And you should get this checksum:

```bash
a18ca8f2e525a01f80c6c011a3480c1b  ghetto-skype_1.4.1_amd64.deb
```

After that, it's as simple as this to install it:

```bash
# You only need sudo if you are not using ROOT
sudo dpkg -i ghetto-skype_1.4.1_amd64.deb
```

Once installation is done, you should be able to launch it from your application launcher or from a terminal like so:

```bash
ghetto-skype
```

Now you should have something like this once you have logged in

![Screenshot](/public/img/ghetto-skype.png)

## For lazy people

This is do all of the mentioned in 1 terminal command

```bash
# I'm talking to you `John Fiel` (Easier to install on Windows my ass)
wget https://github.com/stanfieldr/ghetto-skype/releases/download/v1.4.1/ghetto-skype_1.4.1_amd64.deb && sudo dpkg -i ghetto-skype_1.4.1_amd64.deb
```

## Conclusion

Sometimes (Most of the time) the open source community can do a lot with very limited resources

If you are interested in the [Electron][electron] framework for creating desktop applications with web technology, then visit their [Github page][electron_github]

[skype_ghetto]: https://github.com/stanfieldr/ghetto-skype
{:target="_blank"}

[skype_web]: https://web.skype.com/
{:target="_blank"}

[electron]: http://electron.atom.io/
{:target="_blank"}

[electron_github]: https://github.com/electron/electron
{:target="_blank"}
