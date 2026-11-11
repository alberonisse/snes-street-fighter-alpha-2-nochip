# OFFENER BRIEF AN GUSTAVO FRANCO
[Português](README.md) / [English](README.en.md) / [Español](README.es.md) / [Italiano](README.it.md) / [Deutsch](README.de.md) / [简体中文](README.zh-CN.md) / [日本語](README.ja.md) / [繁體中文（香港）](README.zh-HK.md)

Bitte um Klarstellung, Berichtigung der Zuschreibung und Widerruf

11. November 2026

Gustavo,

Ich habe diesen Fork erstellt, nachdem du das Repository archiviert hast, weil dies der einzige schnelle und direkte Weg war, den ich gefunden habe, um zu versuchen, dir diesen Brief so bald wie möglich zukommen zu lassen.

Ich schreibe, um der in deinem Repository veröffentlichten Zuschreibung zu widersprechen, die die auf der Seite genannten Module als eine kommerzielle Verwertung deiner Implementierung von Street Fighter Alpha 2 ohne S-DD1 bezeichnet.

Meine Erklärung zur Herkunft der Fassung ist eindeutig: Für die USA-Fassung mit 8 MiB, Shin Akuma und beschleunigten Ladezeiten, die ich mithilfe meiner Dekomprimierung und der für den Speicher 29LV640 vorbereiteten Patches bereitgestellt habe, habe ich kein Material aus deinem Projekt verwendet. Ich erkläre, dass die Module, auf die ich mich beziehe, diese Fassung verwenden. Ich widerspreche der Zuschreibung dieser Module zu deinem Projekt, solange der tatsächlich verwendete Inhalt nicht technisch identifiziert wurde.

Mit diesem Brief möchte ich die Herkunft der betreffenden Fassung klären, den Werdegang meiner Arbeit erläutern und darum bitten, dass die öffentliche Zuschreibung durch überprüfbare Belege gestützt wird.

## 1. DER WERDEGANG MEINES PROJEKTS

Meine Arbeit begann nicht erst mit der Bereitstellung der Patches für 8 MiB. Dem ging ein Prozess voraus, der das Studium des S-DD1, die Entwicklung von Werkzeugen, die Analyse des Mappings, den Zusammenbau von Platinen, Korrekturen und Tests auf echter SNES-Hardware umfasste.

Der ursprüngliche Plan sah eine PCB mit CPLD vor, die den Datenzugriff steuern und die Einzelheiten der Implementierung schützen sollte. Ich hatte nicht vor, diese gesamte Struktur aus Dekomprimierung, Datenorganisation und Rekonstruktion offen bereitzustellen.

Als ich von der Veröffentlichung deines Projekts erfuhr, war ich zutiefst demotiviert. Ich betrachtete das Alleinstellungsmerkmal der Arbeit, in die ich Zeit und Mühe investiert hatte, nun als gefährdet. Das war meine Wahrnehmung der Zukunft meines Projekts.

In diesem Zusammenhang beschloss ich, die Richtung zu ändern und die Dekomprimierung sowie die Patches der Fassung mit 8 MiB privat bereitzustellen, um die bereits geleistete Arbeit fortzuführen. Diese Entscheidung rechtfertigt es nicht, die von mir bereitgestellte Fassung automatisch als eine Version deines Repositorys zu bezeichnen.

## 2. WIE MEIN DEKOMPRIMIERUNGSANSATZ FUNKTIONIERT

Im ursprünglichen Kern von sdd1_unpacker habe ich die in bsnes vorhandene Implementierung des S-DD1 untersucht und isoliert. Die Urheberangaben des Codes wurden beibehalten: Andreas Naive für den ursprünglichen Algorithmus beziehungsweise die ursprüngliche Implementierung und byuu für den bsnes-Port. Ich beanspruche nicht, den S-DD1-Algorithmus erfunden zu haben.

Dieser Code wurde zu einem C++-Werkzeug angepasst, das unabhängig von der grafischen Oberfläche und dem vollständigen Betrieb des Emulators arbeitet, mit validiertem Einlesen der ROM-Daten und Behandlung der Speicherbänke des S-DD1.

Das Spiel behandelt nicht die gesamte ROM als eine einzige komprimierte Datei. Es fordert bestimmte Datenströme an, normalerweise während DMA-Übertragungen. Deshalb umfasste die Arbeit die Analyse von Deskriptoren und Tabellen der ursprünglichen ROM, die Aufzeichnung von während der Ausführung gestellten Requests und die Zusammenführung von Herkunft, Größe und Konfiguration der Speicherbänke.

Der kanonische Trace der historischen Rekonstruktion enthält 3.155 Request-Identitäten in 3.160 Zeilen. Die fünf zusätzlichen Zeilen halten Belege für weitere Aufrufstellen bereits katalogisierter Requests fest. Beobachtete Requests und statisch abgeleitete Einträge werden getrennt klassifiziert; diese Zählung bedeutet weder 3.155 unterschiedliche komprimierte Datenströme noch beweist sie für sich genommen die Abdeckung aller Spielsituationen.

Die Verarbeitungskette des ursprünglichen Kerns war wie folgt aufgebaut: ursprüngliche USA-ROM, Analyse und Traces, Request-Katalog, Dekomprimierung der Daten, Anordnung in einem neuen Layout, DMA-Patches und Überprüfungen der Rekonstruktion ohne S-DD1.

Diese Rekonstruktion erforderte es, zwischen CPU-Adresse und Offset in der Datei zu unterscheiden, die ROM-Bereiche des SNES zu beachten und die bearbeiteten Routinen auf bereits dekomprimierte Daten umzuleiten. Sie lässt sich nicht darauf reduzieren, die Datei zu vergrößern oder ihren Header zu ändern.

## 3. DIE ANPASSUNG AUF 8 MiB UND DIE EINFACHE PLATINE

Die Entwicklungslinie mit 8 MiB ist vom vorherigen Rekonstruktionskern mit 16 MiB zu unterscheiden. Sie durchlief einen anderen Organisations- und Zuordnungsprozess, bei dem ein Inventar verwendet wurde, das aus der von mir getesteten und auf YouTube gezeigten 16mb-Basis gewonnen wurde, sowie spätere Korrekturen und Überprüfungen. Ich stelle sie nicht als einen einfachen Ausschnitt aus der Datei mit 16 MiB dar.

Die Fassung wurde für eine einfache Platine mit den entsprechenden Verbindungen und einem einzigen TSOP48-Flash-Speicher mit 8 MiB vorbereitet, dem 29LV640 im x8-Modus. Diese Fassung benötigt in dieser Konfiguration weder S-DD1 noch CPLD und wurde auf echter SNES-Hardware getestet. Auch die Variante für eine modifizierte LoROM-Platine wurde vorbereitet.

Es besteht ein objektiver Unterschied zu der in deinem Projekt dokumentierten historischen Konvertierung mit 12 MiB. Dieses Image mit 12 MiB kann nicht einfach auf den 29LV640 mit 8 MiB geschrieben und in der von mir vorgeführten Konfiguration verwendet werden. Dein eigener technischer Bericht beschreibt ein spezifisches Mapping, einschließlich eines Fensters in den Bänken C0-FF:

https://github.com/snes9xgit/snes9x/issues/1081

Ich behaupte nicht, dass deine Implementierung niemals für ein physisches Modul angepasst werden könnte, und bestreite auch nicht die Hardwaretests, die du dokumentiert hast. Ich unterscheide ein Image mit 12 MiB und dessen Mapping von der Fassung mit 8 MiB, die für meine Platinenkonfiguration vorbereitet wurde.

Wenn das Ziel darin besteht, den Zugang zum Spiel zu erweitern, halte ich es für wichtig, auch diesen Weg anzuerkennen: Menschen die Nutzung einer einfachen Platine und zugänglicher Bauteile zu ermöglichen, ohne ein bestimmtes Flashcart kaufen zu müssen. Ich hatte bereits eine bei dieser Arbeit verwendete Testplatine dokumentiert; das Video ist in der Liste am Ende dieses Briefes aufgeführt.

## 4. URHEBERANGABEN UND GENAUIGKEIT

Der vorliegende Widerspruch bezieht sich ausdrücklich auf die USA-Fassung mit 8 MiB, die in den genannten Modulen verwendet wird. Die Herkunft dieser Fassung muss anhand der tatsächlich verwendeten Dateien, ihrer Patches und ihrer Provenienz untersucht werden. Sie darf weder aus Inventaren einer anderen Region oder aus separaten Forschungsrevisionen noch aus der bloßen Ähnlichkeit der beworbenen Funktionen abgeleitet werden.

Ich beanspruche keine ausschließliche Urheberschaft am öffentlichen Algorithmus, an Routinen Dritter oder an den Daten des ursprünglichen Spiels. Ich beanspruche die korrekte Anerkennung der Integrations-, Anpassungs-, Korrektur- und Validierungsarbeit, die an der von mir bereitgestellten Fassung geleistet wurde.

## 5. ÖFFENTLICHE AUFZEICHNUNGEN ZUR ÜBERPRÜFUNG DER CHRONOLOGIE

Ich lege die folgenden Aufzeichnungen vor, damit ihr Inhalt und ihre Veröffentlichungsdaten mit der Versionsgeschichte abgeglichen werden können. Sie dokumentieren den von mir geschilderten Werdegang; sie ersetzen nicht den Vergleich der tatsächlich im Modul verwendeten Dateien.

Einfache Testplatine:
https://www.youtube.com/shorts/EVQoQB8mD1A

Ergänzende Aufzeichnung 1:
https://www.youtube.com/shorts/uhzHfQFPbVw

Ergänzende Aufzeichnung 2:
https://www.youtube.com/shorts/23gS_IEGDqc

Sendung zum Projekt:
https://www.youtube.com/live/zakojPNeGc0

Ergänzende Aufzeichnung 3:
https://www.youtube.com/shorts/PXVAKPfAO1E

Ergänzende Aufzeichnung 4:
https://www.youtube.com/shorts/y8PAzIzPz1I

Ergänzende Aufzeichnung 5:
https://www.youtube.com/shorts/bStb8AW_QzQ

Ergänzende Aufzeichnung 6:
https://www.youtube.com/shorts/if26BECUllI

Phase mit PCB und CPLD:
https://www.youtube.com/shorts/X-Hby6Vw-m4

Video, das ich vor der Vorbereitung und der privaten Weitergabe der Patches für 8 MiB veröffentlicht habe:
https://www.youtube.com/shorts/YZbpycbEW0w

Spätere Vorführung des Spiels auf einer einfachen Platine mit dem 29LV640:
https://www.youtube.com/shorts/GKl1eOMFks0

Meine an dich gerichtete Klarstellung:
https://youtu.be/8X8jRSXFb5I

## 6. WORUM ICH BITTE

Die Veröffentlichung, auf die ich mich beziehe, befindet sich unter:
https://github.com/gufranco/snes-street-fighter-alpha-2-nochip

Ich bitte dich zu erläutern, welche Datei untersucht wurde, welchen Hash sie hat, aus welchem Modul sie gewonnen wurde und welche technischen Anhaltspunkte die Zuschreibung zu deiner Implementierung gestützt haben.

Ich bitte außerdem darum, dass der Vergleich das physische Mapping, die Routinen, die Patches und die konkrete Revision berücksichtigt, anstatt nur die kommerzielle Beschreibung oder das Vorhandensein von Funktionen wie Shin Akuma und beschleunigten Ladezeiten als Beweis zu nehmen.

Solange diese Identifizierung umstritten bleibt und kein technischer Nachweis vorgelegt wurde, bitte ich darum, dass die Veröffentlichung diesen Umstand ausdrücklich kenntlich macht und die kategorische Zuschreibung entfernt. Sollte sich der Irrtum bestätigen, bitte ich um die Berichtigung der Veröffentlichungen und einen öffentlichen Widerruf mit einer Sichtbarkeit, die der ursprünglichen Darstellung entspricht.

Ich respektiere deine Arbeit und bitte dich, auch meine zu respektieren. Ich beabsichtige weder, persönliche Angriffe zu fördern, noch deinen Einsatz herabzusetzen.

Die Frage, die ich aufwerfe, ist sachlicher Natur: Die Herkunft einer Implementierung muss nachgewiesen werden. Ein ähnliches Ergebnis, ein Name in einer Verkaufsanzeige oder eine Verpackung ersetzen nicht die Analyse des tatsächlich verwendeten Inhalts.

Mit freundlichen Grüßen

Projektverantwortlicher von ALBER MULTI HOUSE
