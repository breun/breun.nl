---
layout: post
title: Growlified Tweet Deluxe
date: '2007-04-10 17:53:29 +0200'
mt_id: 852
categories:
- tech
---
<small>English summary: I modified Ted Leung's <a href="http://www.sauria.com/blog/2007/01/18/growlified-tweet/">Growlified Tweet</a> to do some error checking. Message length is checked before sending and send errors are reported. Feel free to <a href="/files/Tweet.scpt">download my version</a>!</small>

Coda Hale maakte <a href="http://blog.codahale.com/2007/01/15/tweet-twitter-quicksilver/">een AppleScript om direct vanuit Quicksilver naar Twitter te kunnen posten</a>. Ted Leung breidde dit script uit naar <a href="http://www.sauria.com/blog/2007/01/18/growlified-tweet/">een versie die gebruik maakt van Growl notificaties</a>.

Ik heb zelf nog even wat error-checking toegevoegd: je krijgt een Growl melding als je bericht te lang is. Als je bericht niet succesvol is afgeleverd krijg je daar ook een melding over (dat checkt Ted Leung's versie niet).

<a href="/files/Tweet.scpt">Downloaden dus</a>, in ~/Library/Application Support/Quicksilver/Actions/ plaatsen en Quicksilver herstarten als je eerder nog geen Tweet.scpt had.
