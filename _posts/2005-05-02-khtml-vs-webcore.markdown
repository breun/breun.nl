---
layout: post
title: KHTML vs WebCore
date: '2005-05-02 00:48:04 +0200'
mt_id: 681
categories:
- computers
---
OS X, het besturingssysteem van Apple, is gebouwd op diverse <a href="http://www.apple.com/opensource/">open source fundamenten</a>. Een belangrijk component hier is <a href="http://developer.apple.com/darwin/projects/webcore/">WebCore</a>, dat ervoor zorgt dat webbrowser <a href="http://www.apple.com/nl/macosx/features/safari/">Safari</a> webpagina's kan laten zien. WebCore is gebaseerd op KTHML van het <a href="http://www.kde.org/">KDE project</a>, dat daar onder andere gebruikt voor de webbrowser-fucntionaliteit in <a href="http://www.konqueror.org/features/browser.php">Konqueror</a>.

Nu is het zo dat de licentie (<a href="https://nl.wikipedia.org/wiki/GNU_Lesser_General_Public_License">LGPL</a>) waaronder KHTML verspreid wordt toestaat dat anderen de code gebruiken als onderdeel binnen een programma waarvan de broncode niet openbaar is, op voorwaarde dat veranderingen die zij erin aanbrengen teruggecommuniceerd worden naar de originele auteurs, opdat zij verbeteringen en uitbreidingen kunnen doorvoeren in het originele programma.

Het feit dat Apple dus koos voor KHTML als uitgangspunt voor een eigen webbrowser stemde veel KHTML gebruikers vrolijk: alles wat Apple zou verbeteren aan de code zou ook ten goede komen van hen! Nu blijkt helaas dat er toch wat minder reden voor enthousiasme is, althans als je de volgende blog posts van KDE ontwikkelaars leest.

Zack Rusin beantwoordt de vraag <a href="http://www.kdedevelopers.org/node/view/1001">So, when will KHTML merge all the WebCore changes?</a> met: waarschijnlijk nooit. De reden die hij hiervoor geeft is dat de code in Safari erg inconsistent is en altijd weer afhangt van andere stukken code. Er zijn zelfs verbeteringen die door de manier waarop ze geschreven zijn alleen kunnen werken op OS X en dus helemaal niet door te voeren in de algemene versie van KHTML. Hij besluit te zeggen dat, hoewel hij het erg jammer vindt, er helemaal geen sprake is van een samenwerking tussen de ontwikkelaars van WebCore en KHTML, maar dat dit geheel Apple's recht is. Apple houdt zich wel aan de licentievoorwaarden. Hij hoopt alleen dat mensen stoppen te vertellen hoe geweldig het is dat Apple en KDE samenwerken op dit vlak.

In <a href="http://www.kdedevelopers.org/node/view/1002">The bitter failure named "safari and khtml"</a> reageert Inorog hierop door te zeggen dat Zack helemaal gelijk heeft, maar niet zo'n toon moet aanslaan. Apple heeft immers niets misdaan. Jammer dat het niets oplevert voor het KHTML team, maar je kunt niet iemand de regels voorleggen en vervolgens gaan zeuren dat iemand best wat aardig had mogen doen. Tot slot (?) geeft carewolf in het toepasselijk getitelde stukje <a href="http://www.kdedevelopers.org/node/view/1006">Safari and KHTML again</a> nog wat concrete voorbeelden.

Persoonlijk was ik er ook van overtuigd dat het echt geweldig nieuws was dat Apple KHTML ging gebruiken. Ik vind het echt jammer dat het in praktijk niet echt blijkt te werken, zelfs al gebruik ik Konqueror noch Safari (<a href="http://www.opera.com/">Opera</a> heerst op al mijn desktop: Mac, Linux en Windows). Niet dat dit nu het ongelijk van de open source beweging aantoont, maar hoe zeggen ze dat? Oh ja: "Het had zo mooi kunnen zijn."

<small>Voor de liefhebbers: op Slashdot wordt de kwestie uiteraard ook <a href="http://apple.slashdot.org/article.pl?sid=05/04/29/1556252">besproken</a>.</small>
