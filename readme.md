[![Blog](https://badges.weareopensource.me/badge/Read-On%20our%20Blog-1abc9c.svg?style=flat-square)](https://weareopensource.me) [![Slack](https://badges.weareopensource.me/badge/Chat-On%20Slack-d0355b.svg?style=flat-square)](mailto:weareopensource.me@gmail.com?subject=Join%20Slack&body=Hi,%20I%20found%20your%20community%20We%20Are%20Open%20Source.%20I%20would%20be%20interested%20to%20join%20the%20Slack%20to%20share%20and%20discuss,%20Thanks) [![Mail](https://badges.weareopensource.me/badge/Contact-By%20Mail-3498db.svg?style=flat-square)](mailto:weareopensource.me@gmail.com?subject=Contact)

[![Packagist](https://badges.weareopensource.me/packagist/l/doctrine/orm.svg?style=flat-square)](/LICENSE.md)


# Slack Themes

Slack themes with fonts and colors of apple

# Preview

![Screenshot](https://github.com/PierreBrisorgueil/slack-black-theme/blob/master/screens/001.png?raw=true)

# Installing into Slack

Find your Slack's application directory.

* Windows: `%homepath%\AppData\Local\slack\`
* Mac: `/Applications/Slack.app/Contents/`
* Linux: `/usr/lib/slack/` (Debian-based)


Open up the most recent version (e.g. `app-2.5.1`) then open
`resources\app.asar.unpacked\src\static\index.js`

At the very bottom, add

```js
// First make sure the wrapper app is loaded
document.addEventListener("DOMContentLoaded", function() {

   // Then get its webviews
   let webviews = document.querySelectorAll(".TeamView webview");

   // Fetch our CSS in parallel ahead of time
   const cssPath = 'https://raw.githubusercontent.com/PierreBrisorgueil/slack-black-theme/master/custom.css';
   let cssPromise = fetch(cssPath).then(response => response.text());
   //let cssPromise = fetch(cssPath + '?zz=' + Date.now(), {cache: "no-store"}).then(response => response.text());

   let customCustomCSS = `
    :root {
       --text: #000;
       --text-special: #333;
       --background: #fafafa;
       --background-special: #fff;
    }

      // dark
       /*
       --text: #ccc;
       --text-special: #fff;
       --background: #333;
       --background-special: #3f3f3f;
       */
      // light
   `   /*
       --text: #000;
       --text-special: #333;
       --background: #fafafa;
       --background-special: #fff;
      */

   // Insert a style tag into the wrapper view
   cssPromise.then(css => {
      let s = document.createElement('style');
      s.type = 'text/css';
      s.innerHTML = css + customCustomCSS;
      document.head.appendChild(s);
   });

   // Wait for each webview to load
   webviews.forEach(webview => {
      webview.addEventListener('ipc-message', message => {
         if (message.channel == 'didFinishLoading')
            // Finally add the CSS into the webview
            cssPromise.then(css => {
               let script = `
                     let s = document.createElement('style');
                     s.type = 'text/css';
                     s.id = 'slack-custom-css';
                     s.innerHTML = \`${css + customCustomCSS}\`;
                     document.head.appendChild(s);
                     `
               webview.executeJavaScript(script);
            })
      });
   });
});
```

Notice that you can edit any of the theme colors using the custom CSS (for
the already-custom theme.) Also, you can put any CSS URL you want here,
so you don't necessarily need to create an entire fork to change some small styles.

That's it! Restart Slack and see how well it works.

NB: You'll have to do this every time Slack updates.

# Color Schemes

Here's some example color variations you might like.

Custom sidebar in preferences : #2D2D2D,#2D2D2D,#42B8A5,#FFFFFF,#555555,#FFFFFF,#42B8A5,#F27C55

## Dark
![Dark](https://github.com/PierreBrisorgueil/slack-black-theme/blob/master/screens/001.png?raw=true)
```
--text: #ccc;
--text-special: #fff;
--background: #333;
--background-special: #3f3f3f;
```

## Light
![Light](https://github.com/PierreBrisorgueil/slack-black-theme/blob/master/screens/002.png?raw=true)
```
--text: #000;
--text-special: #333;
--background: #fafafa;
--background-special: #fff;
```

# License

Apache 2.0


[![Help](https://badges.weareopensource.me/badge/Help-On%20Patreon-052d49.svg?style=flat-square)](https://www.patreon.com/pbrisorgueil) [![Cofee](https://badges.weareopensource.me/badge/Buy-Me%20a%20Coffee-FF813F.svg?style=flat-square)](https://www.buymeacoffee.com/JrSa9tZGO)


[![Youtube](https://badges.weareopensource.me/badge/Watch-me%20on%20Youtube-e74c3c.svg?style=flat-square)](https://www.youtube.com/channel/UCIIjHtrZL5-rFFupn7c3OtA) [![Twitter](https://badges.weareopensource.me/badge/Follow-me%20on%20Twitter-3498db.svg?style=flat-square)](https://www.youtube.com/channel/UCIIjHtrZL5-rFFupn7c3OtA) 
