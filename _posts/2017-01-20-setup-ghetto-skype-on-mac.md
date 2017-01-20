---
layout: post
title: Setup Ghetto Skype on Mac?
---

[Ghetto Skype][skype_ghetto] is an open source desktop application powered by [Electron][electron] which acts as the wrapper for the [Web Skype][skype_web] beta that Microsoft has been working on. A quote from the [Ghetto Skype][skype_ghetto] README.md file:

  > Are you tired of a buggy 32 bit official Skype client? Then Ghetto Skype is for you!

Install [Homebrew][brew_sh] if you don't have it already

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Once [Homebrew][brew_sh] is done installing, you will need wget (Will need this CLI tool later)

```bash
brew install wget
```

Now install [NVM][nvm] so that we can install [Node.js][node_js]

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash
```

You will need to install the stable version of [Node.js][node_js] via [NVM][nvm]

```bash
nvm install stable
```

We need to download the latest version source code from the [Github Repo][skype_ghetto] of [Ghetto Skype][skype_ghetto]

```bash
wget https://github.com/stanfieldr/ghetto-skype/archive/v1.5.0.zip
```

NOTE: You can check what the latest versions of [Ghetto Skype][skype_ghetto] are on it's [releases page](https://github.com/stanfieldr/ghetto-skype/releases){:target="_blank"}

Unzip the new archive, delete the zip, and move into the unziped folder

```bash
unzip v1.5.0.zip && rm v1.5.0.zip && cd ghetto-skype-1.5.0
```

Install all required [Node.js][node_js] modules

```bash
npm install
```

Build the package

```bash
npm run dist
```

Open up the `dist/mac` dir in finder

```bash
open dist/mac
```

Now, you should see a `.app` and a `.dmg` for [Ghetto Skype][skype_ghetto]

![Screenshot](/public/img/ghetto-skype-finder.png)

You can either drag the `.app` file to your `Applications` folder, or open the `.dmg` file and do as you would with any other `.dmg` installer

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

[node_js]: https://nodejs.org/
{:target="_blank"}

[nvm]: https://github.com/creationix/nvm
{:target="_blank"}

[brew_sh]: http://brew.sh/
{:target="_blank"}
