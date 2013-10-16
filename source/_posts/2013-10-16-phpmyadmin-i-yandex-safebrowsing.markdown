---
layout: post
title: "PHPMyAdmin и Yandex SafeBrowsing"
date: 2013-10-16 14:05
comments: true
categories: security
---

Иногда случается ситуация, когда [Yandex SafeBrowsing](http://api.yandex.ru/safebrowsing/) [помечает сайт](http://www.yandex.com/infected?url=yandex.ru)  как содержащий `Troj/JSRedir-MH`, причем, [VirusTotal](https://www.virustotal.com/)  говорит, что сайт чистый по всем базам, кроме Yandex SafeBrowsing.
В интернетах эту тему обсуждают много где, часто у людей эта проблема регулярно появляется и исчезает сама, в итоге приходят к выводу, что у яндекса что-то глючит.

Как выяснилось, Yandex скорее всего таким образом реагирует на PHPMyAdmin. Проверьте, не установлен ли он у вас.

Причем, для того, чтобы яндекс среагировал на него, у человека, открывшего PHPMyAdmin в броузере должно быть установлено приложение, использующее [Yandex SafeBrowsing](http://api.yandex.ru/safebrowsing/) -- например, Яндекс.Бар, или Яндекс.Браузер.

Вывод: если вы пользуетесь PHPMyAdmin, или вообще занимаетесь поддержкой сайтов, продукты Яндекса лучше не использовать.
