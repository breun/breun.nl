---
layout: post
title: Backups voor Dummies
date: '2006-07-18 04:33:31 +0200'
mt_id: 791
categories:
- tech
---
Na een hele zooi gratis backupprogramma's geprobeerd te hebben, heb ik nu eindelijk de oplossing voor mijn setup. Ik heb een externe USB harde schijf en wil een backup van /Users hebben. Een scheduler heb ik niet echt wat aan, want ik sluit die externe schijf slechts af en toe aan. Ik vraag me af waarom ik deze oplossing niet eerder bedacht had. En voor deze oplossing hoef je helemaal niks te installeren, want je krijgt het al bij OS X meegeleverd (Linux distributies hebben 't ook allemaal wel):

<blockquote>sudo rsync -av --delete /Users/ /Volumes/MacPorsche/Backup/Users/</blockquote>

That's it. Het mooie van rsync is dat alleen veranderde files naar de backupschijf gestuurd worden, dus na de eerste backup is het vervolgens meestal heel snel geregeld. Dat --delete ziet er een beetje eng uit, maar geeft aan dat bestanden die niet meer op m'n laptop staan ook op de backupschijf verwijderd mogen worden.

Mocht je meerdere computers centraal willen backuppen, makkelijk restores kunnen uitvoeren (via een web interface) en meerdere dagen(/weken/maanden) terug kunnen gaan e.d., dan raad ik je aan om eens naar <a href="http://backuppc.sourceforge.net/">BackupPC</a> te kijken. BackupPC kan ook rsync als backupmethode gebruiken (naast tar, Samba, desgewenst over NFS/RSH/SSH). Maar gewoon voor een zekerheidskopie van je eigen bestandjes is een rsync commando eigenlijk gewoon perfect.
