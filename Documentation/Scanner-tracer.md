Trace Sense — Systemdokumentation

Ziel

Trace Sense erlaubt dem Spieler, kürzlich entstandene akustische Spuren in der Welt sichtbar zu machen und zu untersuchen.

Das System dient dazu:

vergangene Aktivität zu lesen

Bewegungen und Kämpfe zu rekonstruieren

Bedrohung einzuschätzen

Entscheidungen zu treffen, ohne direkten Sichtkontakt gehabt zu haben


Es ist kein exakter Audio-Replay-Modus, sondern ein abstrahierter, unvollständiger, interpretierbarer Erinnerungsmodus.


---

1. Kernfantasie

Wenn Trace Sense aktiv ist:

vergangene Geräusche werden als akustische Nachbilder sichtbar

Footsteps erscheinen als Spur oder Reihe von Impulsen

Gunshots erscheinen als stärkere, isolierte Ereignisse

Stimmen / Rufe erscheinen als diffuse Gesprächsreste

die Welt zeigt was hier passiert ist, aber nicht perfekt


Der Spieler kann also:

einen Weg nachvollziehen

erkennen, wo geschossen wurde

verstehen, ob ein Raum gerade benutzt wurde

einschätzen, wie frisch eine Spur ist



---

2. Abgrenzung zu AudioSense

AudioSense

Zeigt:

aktuelle Geräusche

live

direkt reaktiv

für unmittelbare taktische Wahrnehmung


Trace Sense

Zeigt:

vergangene Geräusche

gespeichert

abstrahiert

für Rekonstruktion und Planung


Kurzform

AudioSense = Jetzt

TraceSense = Vor kurzem



---

3. Grundprinzip

Die Welt speichert nicht die gesamte Audioausgabe, sondern nur relevante akustische Ereignisse als Datenpunkte.

Also nicht:

komplettes 3-Sekunden-Audio der ganzen Welt


sondern:

ausgewählte “Trace Events”


Jedes Event speichert:

Ort

Zeit

Soundtyp

Intensität

Quelle

optional Richtung / Ziel / Kontext


Diese Events können später im Trace Sense:

visualisiert

gruppiert

optional abstrahiert abgespielt


werden.


---

4. Welche Sounds werden gespeichert?

Nicht alle Sounds.
Du brauchst ein Kurationssystem, sonst wird der Modus unlesbar.

Es werden nur Sounds gespeichert, die:

taktisch relevant sind

semantisch lesbar sind

eine Handlung oder Präsenz anzeigen

nicht zu häufig bedeutungslos rauschen



---

5. Sound-Kategorien

Ich würde die Sounds in 4 Speicherklassen teilen.

A. Hochpriorisierte Trace Events

Immer speicherwürdig, wenn im Radius / Kontext:

Gunshots

Explosionen

laute Melee Hits

Alarme

Schreie / kurze laute Rufe


Diese sind:

stark sichtbar

lange gespeichert

gut lesbar


B. Mittlere Priorität

Speicherwürdig unter Bedingungen:

Footsteps

Sprinten

Reloads

Door interactions

Funk / kurze Kommunikation


Diese werden gespeichert, aber:

komprimiert

gruppiert

zeitlich begrenzt


C. Niedrige Priorität

Nur speichern, wenn explizit wichtig oder isoliert:

Cloth

kleine Objektinteraktionen

leises Umsehen

leichtes Gehen


Diese normalerweise nicht einzeln, sondern nur verdichtet.

D. Nicht speicherwürdig

Nicht speichern:

Ambience

Regen

Wind

generelles Raumrauschen

kleine unbedeutende Foley-Geräusche



---

6. Entscheidungslogik: Was wird gespeichert?

Es braucht einen Filter pro Event.

Jedes mögliche Trace Event bekommt:

SoundType
WorldLocation
Timestamp
SourceActor
RawIntensity
ImportanceScore

Dann entscheidet eine Funktion:

ShouldStoreTraceEvent(EventData)


---

Entscheidungskriterien

1. Soundtyp

Manche Typen sind von Natur aus speicherwürdig:

Gunshot = fast immer ja

Explosion = ja

Reload = oft ja

Footstep = nur unter Bedingungen


2. Lautstärke / Wichtigkeit

Sehr leise Ereignisse werden ignoriert.

3. Frische / Dichte in Umgebung

Wenn 10 Footsteps in 1 Sekunde an fast gleichem Ort passieren, speicherst du nicht 10 Einzelereignisse.

4. Räumliche Nähe zu anderen Events

Events können zusammengefasst werden.

5. Source-Kategorie

Ein Spieler oder eine wichtige KI kann höher priorisiert werden als ein unbedeutender NPC.

6. Weltzustand

Im Sturm oder bei Massengewalt kann aggressiver gefiltert werden, damit der Modus lesbar bleibt.


---

7. Footsteps speziell

Das ist dein wichtigster Sonderfall.

Problem

Wenn eine KI eine Straße entlang rennt, entstehen viele Schritte.
Alle einzeln zu speichern wäre Spam.

Lösung

Footsteps werden nicht als isolierte Audioevents, sondern als Spursegmente gespeichert.

Also:

Nicht:

Schritt 1

Schritt 2

Schritt 3

Schritt 4


Sondern:

ein kurzer Bewegungsabschnitt / Trail


Beispiel

Eine KI rennt 5 Sekunden:

das System sammelt Footstep-Punkte

gruppiert sie zu einer Spur

in Trace Sense sieht man:

eine verblassende rote Bewegungssequenz

evtl. 3–6 repräsentative Knoten

nicht 20 identische Einzelimpulse



Vorteil

viel lesbarer

performanter

taktisch nützlicher



---

8. Gunshots speziell

Gunshots sollten als isolierte Event Marks gespeichert werden.

Warum?

Sie sind:

selten

bedeutend

gut verständlich

sehr relevant


Darstellung

klarer einzelner Event-Puls

mit stärkerer visueller Signatur

optional mit kleiner Richtungsinformation


Wenn die KI 2x schießt:

beide können gespeichert werden

aber bei sehr kurzem Abstand evtl. als Burst-Gruppe visualisiert



---

9. Voices / Gespräche speziell

Gespräche sind schwieriger.

Empfehlung

Nicht jede Zeile speichern.
Stattdessen:

Gesprächsfenster / Voice Cluster speichern


Also:

“hier wurde gesprochen”

statt “hier waren exakt diese 3 Sätze”


Darstellung

diffuse rote Gesprächswolke

pulsierende Restpräsenz

keine präzise semantische Offenlegung


Optional später

Wenn Spieler nahe rangeht:

fragmentierte, unklare Audio-Samples abspielbar

nur Bruchstücke

teilweise entschlüsselbar


Das ist narrativ und mechanisch viel spannender.


---

10. Was passiert in deinem Beispiel?

Szenario

Eine KI rennt eine Straße entlang, schießt 2x und schreit etwas.

Gespeichert wird:

Footsteps

als eine Bewegungsspur

nicht jeder einzelne Schritt


2 Gunshots

als 2 einzelne Event Marks

oder ein kleiner Burst-Cluster, wenn dicht genug


Schrei / Voice

als eine diffuse Gesprächs-/Voice-Anomalie am Ort des Rufes


In Trace Sense sichtbar:

rote Spur entlang der Laufroute

2 stärkere Event-Marken für die Schüsse

1 diffuse Voice-Wolke


Das ergibt eine extrem lesbare Rekonstruktion.


---

11. Soll die ganze Welt-Audio von 3 Sekunden abgespielt werden?

Meine klare Empfehlung: Nein

Nicht als vollständiges Replay.

Das wäre:

zu laut

zu unklar

zu gamey

zu technisch

zu overpowered


Besser

Nur kontextuelle, abstrahierte Audio-Fragmente.


---

12. Audio-Wiedergabe in Trace Sense

Trace Sense soll nicht einfach alte Sounds normal abspielen, sondern:

> akustische Erinnerungsreste



Möglichkeiten

A. Abstrahierte Wiedergabe

dumpfer

fragmentiert

gedehnt

mit Noise

wie Erinnerung / Echo


B. Näheabhängig

Nur wenn Spieler sich einem Trace nähert:

wird Audio hörbar

sonst nur visuell


C. Nicht perfekt verständlich

Ein Schrei oder Funksatz ist:

nur teilweise verständlich

mit Lücken / Störungen / Zensur

evtl. rekonstruierbar durch Nähe oder Upgrade


Das ist viel interessanter als ein perfektes Replay.


---

13. “Entschlüsseln” als Mechanik

Das ist eine sehr gute Idee.

Grundregel

Trace Audio ist zunächst:

unklar

fragmentiert

verrauscht

nur teilweise lesbar


Wenn Spieler näher kommt:

Qualität verbessert sich

Fragmente werden klarer

mehr Worte / Details hörbar


Optional Upgrades

bessere Entschlüsselung

längere Speicherzeit

mehr Kategorien sichtbar

höhere semantische Auflösung


Damit wird Trace Sense:

nicht nur Rekonstruktion

sondern Interpretations-Gameplay



---

14. Visuelle Darstellung

Trace Sense sollte anders aussehen als AudioSense.

AudioSense

live

sofortige Impulse

energetisch

Richtung/Präsenz


Trace Sense

archiviert

ruhiger

nachhallend

lesbar als Vergangenheit


Darstellungsprinzipien

rote Nachbilder

schwache pulsierende Restformen

Trails für Bewegung

Event Marks für Schüsse

diffuse Blobs für Sprache

Intensität nimmt mit Alter ab



---

15. Alterung / Zeitverfall

Jedes Trace Event hat:

Timestamp
MaxLifetime
Age

Regeln

neu = klar, hell, präzise

älter = diffuser, schwächer, fragmentierter

kurz vor Ende = fast nur noch Hauch / Echo


Empfehlung

Gunshots

20–40 Sekunden


Footstep Trails

10–20 Sekunden


Voice Clusters

15–30 Sekunden


Je nach Balancing.


---

16. Datenstruktur

ST_TraceEvent

TraceID
SoundType
WorldLocation
Timestamp
Intensity
SourceActor
Category
Lifetime
bCanPlayback
PlaybackClarity

ST_TraceTrailPoint

Für Footsteps / Bewegung:

WorldLocation
Timestamp
Intensity

ST_TraceTrail

SourceActor
TrailPoints : Array
StartTime
LastUpdateTime
Lifetime


---

17. Systemarchitektur

BP_TraceSenseManager

Zentrale Instanz im Player oder als World Manager.

Aufgaben

relevante Events empfangen

filtern

speichern

gruppieren

alte löschen

bei aktiviertem Trace Sense visualisieren


Event-Quellen

Gunshots

Explosionen

Footstep Notifies

Voice Events

Reload Events


Jede Quelle ruft:

RegisterTraceEvent(...)


---

18. Filterlogik

Funktion

RegisterTraceEvent(EventData)

Ablauf

1. Soundtyp prüfen


2. Mindestintensität prüfen


3. bei footsteps:

bestehende Spur dieses Actors suchen

TrailPoint hinzufügen statt neues Event



4. bei Voices:

nahen Voice-Cluster erweitern statt neues Event



5. bei Gunshots:

neues Event oder Burst-Cluster anlegen



6. Lifetime setzen


7. speichern




---

19. Wiedergabe-Logik

Wenn Trace Sense aktiv

Der Manager geht durch alle gültigen Traces und:

Footstep Trails

spawnt Trail-VFX / Marker


Gunshots

spawnt einzelne Event-Marken


Voice Clusters

spawnt diffuse Gesprächswolken


Wenn Spieler nahe genug

Zusätzlich:

abstrahierte Audiofragmente abspielen



---

20. Audiowiedergabe konkret

Footsteps

kein voller Schritt-Sound-Loop

eher kurzes dumpfes Echo am Knotenpunkt


Gunshots

leiser, verzerrter Restknall

zeitlich leicht gedehnt

kein volles Bedrohungsniveau wie live


Voices

fragmentiert

einzelne Wörter / Bruchstücke

unvollständig



---

21. Wie zwischen AudioSense und TraceSense gewechselt wird

Scanner Master

Scanner bleibt an/aus als Oberzustand.

Submodes

AudioSense
TraceSense
ThreatSense
SignalSense

Wechsel

Empfehlung:

Q = Scanner an/aus

MouseWheel oder Hold Q + Scroll = Modus wechseln


Zusammenspiel

AudioSense

zeigt Live-Events


TraceSense

zeigt gespeicherte Nachbilder


Damit ist die Logik klar und konsistent.


---

22. Balancing-Regeln

Trace Sense darf:

vergangene Aktivität zeigen

Orientierung geben

Planung erleichtern


Trace Sense darf nicht:

perfekte Replay-Kamera sein

jeden NPC path perfekt verraten

exakte Identität und Worte ohne Aufwand offenlegen


Gute Einschränkungen

nur relevante Sounds

Trail-Kompression

fragmentierte Audio-Wiedergabe

Alterungszerfall

begrenzte Reichweite / Anzahl



---

23. Optimierung

Wichtig

Nicht jede Kleinigkeit speichern.

Begrenzungen

max aktive Trace Events global

max aktive Trails pro Source

min Abstand zwischen TrailPoints

min Zeitabstand zwischen Events gleicher Kategorie


Beispiel

Footsteps

Nur neuen Punkt speichern, wenn:

mindestens 80–120 Units vom letzten entfernt

oder mindestens 0.25s vergangen


Das hält es sehr sauber.


---

24. Konkreter Implementierungsplan in UE5

Phase 1

BP_TraceSenseManager

ST_TraceEvent

ST_TraceTrail

Gunshot Events speichern

Footstep Trails speichern

einfache Visualisierung nur visuell


Phase 2

Voice Cluster

Reload Events

Lifetime / Fading

Distanzabhängige Playback-Fragmente


Phase 3

fragmentierte Audio-Wiedergabe

Entschlüsselungsmechanik

Upgrades

Wetter-/Schleierintegration



---

25. Zusammenfassung

Trace Sense ist ein forensischer Scanner-Modus, der:

vergangene relevante Geräusche speichert

sie visuell rekonstruiert

sie nicht perfekt, sondern abstrahiert wiedergibt

Footsteps als Trails

Gunshots als einzelne Ereignisse

Stimmen als Cluster

Audiofragmente nur kontextuell und unvollständig abspielt
 
