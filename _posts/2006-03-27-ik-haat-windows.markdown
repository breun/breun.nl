---
layout: post
title: Ik háát Windows
date: '2006-03-27 20:42:56 +0200'
mt_id: 772
categories:
- tech
---
Ik moet voor mijn afstudeerwerk werken met een C++ programma in een Microsoft Visual Studio project. Ik hÃ¡Ã¡t C++. En al helemaal als ik er alleen onder Windows (want Visual Studio) aan kan werken.

Een klein lichtpuntje leek het feit dat ik via de Universiteit middels een MSDN-AA licentie Visual Studio 2005 thuis gratis (legaal) kan gebruiken. Dat ging ik vanochtend dus maar eens even installeren, want een fijn robbertje thuiswerk, daar kan niets tegenop.

Zal je altijd zien: Windows-partitie te klein. Nouja, m'n dataschijf (gedeeld tussen Windows en Linux) had nog wel wat ruimte, dus ik Partition Magic maar weer eens uit de kast getrokken. Maar ergens op 60% van de herindeling van mijn schijf loopt de boel vast. Een reboot bevestigde wat ik al vreesde. Ik hÃ¡Ã¡t onbruikbare partities.

Nou biedt Windows je ook geen enkele mogelijkheid om iets te doen aan partities die niet willen. Je tweede schijf is gewoon nergens meer te vinden en daar moet je het maar mee doen. Aangezien ik toch enkele tientallen gigabytes op deze partitie had staan, wilde ik graag nog wat terug. Dus je googlet wat rond. En blijkbaar hebben de makers van Partition Magic (het programma dat net je partitie heeft proberen op te eten) ook het programmaatje PTEDIT, waarmee je de boel weer vlot zou moeten kunnen trekken. Nou kun je dit programma uiteraard alleen niet gebruiken terwijl Windows draait. Je zult een opstartdiskette moeten maken. En ik heb al jaren geen diskettes meer in huis.

Dus wat doet de nerd in mij? Gewoon Linux opstarten en daar even fdisk draaien. Hup, partitie-type weer naar FAT32 en terug naar Windows. Ja hoor, schijf is terug. Wel wat schrammetjes (beschadigde bestanden), maar dat mag de pret niet drukken. Fedora Core, bedankt.

Oh, en mooi niet dat ik nou nog een keer Partition Magic loslaat op mijn partities. Laat die suffe C++ compiler (bijna 2 GB!) maar zitten. Ik ga wel weer naar de Uithof als er gewerkt moet worden...
