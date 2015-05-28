---
author:
- Florian Mayer
title: ' MBR-Übung'
...

Einführung
==========

Der MBR, kurz für Master Boot Record, stellt in vielen, heute immer noch
im Einsatz befindlichen Rechnersystemen, den fundamentalen Übergang vom
BIOS hin zum Betriebssystem sicher. Er beinhaltet unter anderem den
Bootloader mit dem dieser Übergang, bzw. der eigentliche Startvorgang,
erst ermöglicht wird. Der MBR ist eine 512 Bytes große Datenstruktur,
die auf IBM-kompatiblen PC-Systemen *immer* den 0-ten Datenblock eines
Festspeichers (z.B. HDD, SDD, ...) füllt. Die wichtigsten Informationen,
die er speichert, sind:

-   Die Partitionstabelle,

-   der Bootloader und

-   die Datenträgersignatur.

Beispielhafter Aufbau eines CHS-Eintrags
----------------------------------------

#### Fragestellung

Angenommen die folgenden Bytes liegen der Reihe nach im MBR: 0xF3 0xFF
0x32. Bestimmen Sie die Nummer des Kopfs, des Sectors und des Zylinders.

#### Lösung

-   Kopf: $F3_(16) = 243_(10)$,

-   Sektor:
    FF_(16) = 1111111_(2) => 00111111_(2) = 127_(10)

-   Zylinder:
    FF_(16), 32_(16) => 1100000000_(2) + 32_(16) = 50_(10) + 512_(10) + 256_(10) = 818_(10)

Konvertierung von CHS nach LBA
------------------------------

Die Formel zur Konvertierung von CHS-Adressen nach LBA-Adressen sein im
Folgenden dargestellt.

$$LBA = (c * H + h) * S + x - 1$$

-   *LBA* Adresse des Blocks nach dem LBA-Verfahren

-   *c* Zylindernummer

-   *H* Zahl der Leseköpfe

-   *h* Lesekopfnummer

-   *S* Zahl der Sektoren. Zahl der Blöcke je Zylinder

-   *s* Sektornummer

Übung
=====

1.  Geben Sie den gesamten MBR einer Festplatte mittels $dd$ und
    $hexdump$ aus.

2.  Geben Sie den Partitionstabelleneintrag der ersten Partition aus.
    Hinweis: Verwenden Sie wieder $dd$ und $hexdump$

3.  Bestimmen Sie:

    -   den Typ der Partition,

    -   den Start-CHS-Eintrag (Welche Nummer hat der Zylinder?),

    -   die Startfähigkeit der Partition,

    -   die Anzahl der Sektoren,

    -   den End-CHS-Eintrag (Welche Nummer hat der Kopf?) und

    -   den Startsektor.

    Hinweis: Die Felder der Partitionstabelleneinträge werden immer im
    Little-Endian-Format abgespeichert

4.  Welches Problem sehen Sie im Bezug auf Partitionstabelleneinträge
    (LBA) im Zusammenhang mit Partitionsgrößen?
