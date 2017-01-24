---
layout: post
title: Getting Electron Copy/Paste shortcuts working on MAC builds
---

If you are new to [Electron][electron] and have noticed that when running the Mac/OSX builds you there is no copy/paste shortcut support, don't be alarmed.

The reason for this is that MAC/OSX requires you to have those shortcuts declared/setup in the application menu, or one of it's sub menus.

You can do a simple fix by loading the [Electron Menu][electron_menu] module in your application's code and setting these shortcuts

Sample Code:

```javascript
const {app,Menu} = require('electron');

// Callback for the ready event
app.on('ready', () => {
    /*
     This is where your other code would go
    */

	// Check if we are on a MAC
	if (process.platform === 'darwin') {
		// Create our menu entries so that we can use MAC shortcuts
		Menu.setApplicationMenu(Menu.buildFromTemplate([
			{
				label: 'Edit',
				submenu: [
					{ role: 'undo' },
					{ role: 'redo' },
					{ type: 'separator' },
					{ role: 'cut' },
					{ role: 'copy' },
					{ role: 'paste' },
					{ role: 'pasteandmatchstyle' },
					{ role: 'delete' },
					{ role: 'selectall' }
				]
			}
		]));
	}
});
```

Once you have added this code to your application code, you should see a new menu that looks like the following image

![Screenshot](/public/img/electron-shortcuts.png)

[electron]: http://electron.atom.io/
{:target="_blank"}

[electron_menu]: https://github.com/electron/electron/blob/master/docs/api/menu.md
{:target="_blank"}
