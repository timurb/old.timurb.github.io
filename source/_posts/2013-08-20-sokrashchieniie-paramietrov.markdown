---
layout: post
title: "Сокращение параметров командной строки"
date: 2013-08-20 11:46
comments: true
categories: shell
---

Бывает, при использовании какой-либо команды постоянно нужно бывает передавать ей длинные параметры.

Например:
```bash
aws din --region=eu
aws din --region=ap
aws start i-39b17e77 --region=us
```

Можно создать алиасы, но это не всегда бывает применимо -- например, в случае когда команда не принимает параметры
до операции, алиас создать не так просто.

Выход такой: свернем параметр до переменной:
```bash
export EU="--region=eu"
export AP="--region=ap"
export US="--region=us"

aws din $EU
aws din $AP
aws start i-39b17e77 $US
```
