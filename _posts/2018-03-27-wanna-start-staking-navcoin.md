---
layout: post
title: Wanna Start Staking NAV / NAVCoin?
---

Wanna start staking [NAVCoin][navcoin] but don't know exactly how?

All you need are the following:

* A linux server with atleast `1GB RAM` and `1 CPU Core`
* A [NAVCoin Core][navcoin_github] wallet
* SOME [NAVCoin][binance] ( Buy some at binance to give me a kick back :D )
* A tutorial to teach you ( This is that tutorial, LMFAO )

NOTE: For the sake of simplicity, my example will be using an `Ubuntu 16.04 Linux Box`

## Step 1

Login to your linux box

```shell
ssh root@server
```

## Step 2

Get the latest NAVCoin Core wallet download link from [HERE][navcoin_releases]

Then download via `wget` on the server

```shell
wget https://github.com/NAVCoin/navcoin-core/releases/download/4.1.1/navcoin-4.1.1-x86_64-linux-gnu.tar.gz
```

## Step 3

Now extract the files with `tar` command

```shell
tar xvf navcoin-4.1.1-x86_64-linux-gnu.tar.gz
```

You should see output like the following

```shell
navcoin-4.1.1/
navcoin-4.1.1/bin/
navcoin-4.1.1/bin/navcoin-cli
navcoin-4.1.1/bin/navcoind
navcoin-4.1.1/bin/navcoin-qt
navcoin-4.1.1/bin/navcoin-tx
```

## Step 4

Move the binary files into the `/usr/bin` for system wide access

```shell
# ROOT
mv navcoin-4.1.1/bin/* /usr/bin

# NON-ROOT
sudo mv navcoin-4.1.1/bin/* /usr/bin
```

## Step 5

Add `navcoind` to the `crontab`

```shell
# Open crontab editor
crontab -e

# Once open add the following entry
@reboot navcoind
```

## Step 6

Reboot the server

```
# ROOT
reboot

# NON-ROOT
sudo reboot
```

## Step 7

Re loggin after reboot

```shell
ssh root@server
```

## Step 8

Get the main address for your new wallet

```shell
navcoin-cli getaddressesbyaccount ""
```

Should give output like the following

```shell
[
  "NSUvvL1siPM9LQdqYhJSwfzoKMH67eQo2W",
  "NVb3mSb7vPsNTZtCvM31cLwRErcQxzv1X8",
  "NdvjJWEFVkyBfZEFDssUhdToSYah7vq6Fg",
  "NcYzVrq3H75ooLDJm5M4CXnZxeRbxWs5fR"
]
```

## Step 9

Pick an address and send some [NAVCoin][binance] to it!

## Conclusion

Once you have followed this tutorial, your wallet should be staking

You can check the status with `navcoin-cli getstakinginfo`

Sample output

```shell
{
  "enabled": true,
  "staking": true,
  "errors": "",
  "currentblocksize": 1000,
  "currentblocktx": 0,
  "difficulty": 670086.1947336281,
  "search-interval": 16,
  "weight": 204495135273,
  "netstakeweight": 1592159691069937,
  "expectedtime": 233574
}
```

And you can check your staking report with `navcoin-cli getstakereport`

Which should look like this

```shell
{
  "2018-03-27 00:00:00": "0.00",
  "2018-03-26 00:00:00": "0.00",
  "2018-03-25 00:00:00": "0.00",
  "2018-03-24 00:00:00": "0.00",
  "2018-03-23 00:00:00": "0.00",
  "2018-03-22 00:00:00": "0.00",
  "2018-03-21 00:00:00": "0.00",
  "2018-03-20 00:00:00": "0.00",
  "2018-03-19 00:00:00": "0.00",
  "2018-03-18 00:00:00": "0.00",
  "2018-03-17 00:00:00": "0.00",
  "2018-03-16 00:00:00": "0.03136986",
  "2018-03-15 00:00:00": "0.08342465",
  "2018-03-14 00:00:00": "0.00",
  "2018-03-13 00:00:00": "0.35438356",
  "2018-03-12 00:00:00": "0.00",
  "2018-03-11 00:00:00": "0.00",
  "2018-03-10 00:00:00": "0.35547945",
  "2018-03-09 00:00:00": "0.00",
  "2018-03-08 00:00:00": "0.67471494",
  "2018-03-07 00:00:00": "0.00",
  "2018-03-06 00:00:00": "0.00",
  "2018-03-05 00:00:00": "0.00",
  "2018-03-04 00:00:00": "0.00",
  "2018-03-03 00:00:00": "0.28657534",
  "2018-03-02 00:00:00": "0.00",
  "2018-03-01 00:00:00": "0.35301369",
  "2018-02-28 00:00:00": "0.00",
  "2018-02-27 00:00:00": "0.00",
  "2018-02-26 00:00:00": "0.19369863",
  "Last 24H": "0.00",
  "Last 7 Days": "0.00",
  "Last 30 Days": "2.33266012",
  "Last 365 Days": "4.00405874",
  "Latest Stake": "0.03136986",
  "Latest Time": "2018-03-16 00:26:24",
  "Stake counted": 12,
  "time took (ms)": 1
}
```

## Things to keep in mind

* Your server should be **`SECURE AND NOT ACCESSIBLE BY ANYONE YOU DON'T TRUST`** with your coins
* Your wallet keys  **`MUST BE BACKED UP`** in case your server gets corrupted
* When you first start reboot your server after `Step 6`, it can take a while for the `navcoind` wallet to sync all the block from the network (A few hours on a Gigabit Network)
* It takes `2 hours` for any coins sent to your wallet to mature and start staking

[navcoin]: https://navcoin.org/
{:target="_blank"}

[navcoin_github]: https://github.com/NAVCoin/navcoin-core
{:target="_blank"}

[navcoin_releases]: https://github.com/NAVCoin/navcoin-core/releases
{:target="_blank"}

[binance]: https://www.binance.com/?ref=12367615
{:target="_blank"}
