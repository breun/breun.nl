---
layout: post
title: SSD in je Mac
---
Ik heb het zelf al meerdere keren gedaan en al diverse vrienden en familieleden geadviseerd: als je nog een harde schijf in Mac hebt zitten, vervang deze dan zo snel mogelijk door een SSD. Je drie jaar oude machine voelt naderhand weer als nieuw!

1. Koop een 2,5" SSD. Momenteel lijken de Samsung 840 EVO SSD's de beste prijs/grootte-verhouding te hebben, maar je kan altijd de [Tweakers Pricewatch](http://www.tweakers.net/pricewatch) er even bij pakken.
2. Koop ook meteen een USB-behuizing voor een 2,5" schijf. Die komt van pas bij het overzetten van je systeem en kan je naderhand gebruiken voor je oude harde schijf.
3. Zet de SSD in de USB-behuizing.
4. Installeer [SuperDuper!](http://www.shirt-pocket.com/SuperDuper/superduperdescription.html) op je Mac. Dit programma kan allerlei handige dingen als je er een licentie voor koopt, maar voor het één-op-één klonen van een schijf voldoet een ongeregistreerde versie ook en laat dat nou net zijn wat we gaan doen. (Je kunt er ook voor kiezen om je systeem van een back-up zoals Time Machine terug te zetten, maar ik vind de route via SuperDuper! zelf het makkelijkst.)
5. Start SuperDuper! en kies ervoor alles van de harde schijf naar de SSD te kopiëren. SuperDuper! zal ervoor zorgen dat de SSD ook opstartbaar gemaakt wordt.
6. Wacht tot de kopie klaar is. Dat kan wel even duren.
7. Haal de harde schijf uit je Mac en de SSD uit de USB-behuizing. Op [iFixit](http://www.ifixit.com/Device/Mac) kun je handige geïllustreerde handleidingen vinden voor jouw model Mac. Een MacBook is trouwens wel wat makkelijker dan een iMac, maar ook dat is met het juiste gereedschap op zich goed te doen.
8. Zet de SSD in je Mac en de harde schijf in de USB-behuizing.
9. Als de ventilator in je Mac continu op volle snelheid begint te blazen, ook wanneer de processor verder helemaal niet druk bezig is, installeer je [SSD Fan Control](http://exirion.net/ssdfanctrl/). Start het programma eenmalig op en zet Fan Control op SMART.
10. Deze stap is optioneel, maar om de levensduur van je SSD te verlengen kun je [Trim Enabler](http://www.cindori.org/software/trimenabler/) installeren en ondersteuning voor TRIM inschakelen voor je SSD. In dit geval voldoet een gratis, ongeregistreerde versie van Trim Enabler. Start Trim Enabler en schakel op het eerste tabblad ondersteuning voor TRIM in. Het is slim om op het laatste tabblad met instellingen ook het controleren van de TRIM-ondersteuning bij het opstarten van je Mac in te schakelen, want updates van OS X kunnen de TRIM-patch ongedaan maken. Als dat gebeurt krijg je een melding en de mogelijkheid om de TRIM-ondersteuning opnieuw in te schakelen.

Woehoe! Alles is nu snel!

P.S. Als alles goed gegaan is kun je de harde schijf in de USB-behuizing nu wissen en voor andere dingen gebruiken. Time Machine back-ups bijvoorbeeld, als daar nog niet aan deed.
