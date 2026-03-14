Scanner-Audiodarstellung — Systemdokumentation

Ziel

Der Scanner-Modus übersetzt akustische Informationen in visuelle, painterly Impulse, damit der Spieler Geräusche räumlich lesen kann, ohne ein klassisches Radar oder Wallhack-System zu bekommen.

Das System soll:

die Welt visuell abstrahieren

Audio wichtiger machen

Geräusche räumlich und stilistisch lesbar machen

Unsicherheit erhalten

zwischen sichtbaren und nicht sichtbaren Quellen unterscheiden

mit Occlusion, Distanz, Wetter und später Steam Audio erweiterbar sein


Grundprinzip

Der Scanner zeigt keine Gegner, sondern akustische Ereignisse.

Er visualisiert also nicht:

“Da ist ein Feind”


sondern:

“Dort ist gerade ein lautes / relevantes Klangereignis passiert”


Damit bleibt das System:

immersiv

taktisch

nicht zu stark

mit deinem Artstyle kompatibel



---

1. Grundlegende Wahrnehmungslogik

Scanner aktiv

Wenn der Scanner aktiv ist:

Visuell

Welt wird in große Farbfelder / Brushstrokes abstrahiert

kleine Details werden reduziert

Gesichter, Waffen, kleine Props werden schwer lesbar

Bewegungen und Silhouetten bleiben erkennbar


Audio

Ambience / Rauschen wird abgesenkt

relevante Sounds werden hervorgehoben

hörbare Distanz für wichtige Sounds wird erhöht

Soundquellen erzeugen visuelle Impulse


Scanner inaktiv

normale Weltwahrnehmung

keine Audio-Visualisierung

normale Audio-Balance



---

2. Grundsystem der Darstellung

Jedes relevante Klangereignis erzeugt einen Scanner Sound Pulse.

Scanner Sound Pulse — Datenmodell

Jeder Pulse hat mindestens:

WorldLocation
SoundType
Intensity
Radius
Duration
OcclusionAmount
VisibleToPlayer
SourceActor

Optional später:

Direction
Velocity
FactionHint
SurfaceType
WindInfluence


---

3. Systemunterteilung nach Soundtypen

Die Scanner-Darstellung wird nicht für alle Sounds gleich behandelt.
Die Soundtypen werden in vier Hauptgruppen unterteilt.


---

A. Gunshots / Explosions / große Impacts

Rolle im Gameplay

Diese Sounds sind:

hochrelevant

weit hörbar

taktisch entscheidend

oft die wichtigsten Ferninformationen


Darstellung

Primär in der Welt, optional minimaler Screen-Hinweis offscreen.

Visuelles Konzept

großer roter Schockimpuls

kurze expandierende painterly Welle

starke Interaktion mit Umgebung

wirkt wie akustisches Licht / Druckwelle


Onscreen

Wenn die Quelle sichtbar ist:

Impuls direkt am Ursprungsort

umgebende Flächen werden kurz rot beleuchtet

kurze Stroke-Ausläufer entlang Boden/Wänden

klare räumliche Zuordnung


Offscreen

Wenn die Quelle nicht sichtbar ist:

Impuls bleibt primär in der Welt

zusätzlich optional:

kurzer subtiler Randglow in Soundrichtung

kein Pfeil, kein klassisches UI-Marker-Verhalten


bei starker Occlusion:

Impuls erscheint schwächer und diffuser an Öffnungen / Wänden / Kanten



Zielwirkung

Spieler kann Richtung und grobe Distanz lesen

Indoor / Outdoor / Urban soll stilistisch fühlbar sein

Sound bleibt bedrohlich und groß



---

B. Footsteps / Bewegung / Sprinten / Cloth Movement

Rolle im Gameplay

Gegnerbewegung lesen

Flanken erkennen

versteckte Annäherung oder Rush identifizieren


Darstellung

Primär in der Welt, kein klassisches UI.

Visuelles Konzept

kleine rhythmische rote Impulse

direkt an Fußkontaktpunkten oder Bodenregionen

bei Sprinten stärker und klarer

bei Schleichen schwächer und kürzer


Onscreen

Wenn die Person sichtbar ist:

Impulse direkt an der Figur / unter den Füßen

verstärkt Lesbarkeit von Bewegungsmustern

hilft, Bewegung statt Identität zu lesen


Offscreen

Wenn die Person nicht sichtbar ist:

Impuls erscheint an hörbarer Boden-/Wandregion

bei Occlusion diffuser

keine exakte Wallhack-Position, eher “aus dieser Ecke / aus diesem Raum kommt Bewegung”


Zielwirkung

Bewegung lesen, nicht Identität

hohe taktische Relevanz im Nahbereich

Scanner macht Schritte wichtig, aber nicht zu präzise



---

C. Reloads / Metall / Weapon Handling / Interaktionssounds

Rolle im Gameplay

Gegner lädt nach

jemand bereitet Schuss vor

jemand interagiert mit Objekt / Tür / Metall / Kiste


Darstellung

Primär in der Welt, punktueller als Schritte.

Visuelles Konzept

kurzer, präziser roter Klick-/Spark-Impuls

klein, scharf, fokussiert

kein großer Ring

eher “akustischer Funke”


Onscreen

kleiner heller Impuls direkt an Quelle

hohe Präzision

sehr gutes Taktiksignal


Offscreen

kleiner diffuser Punkt / Funke an plausibler Wand-/Tür-/Kantenregion

Richtung lesbar, aber nicht pixelgenau


Zielwirkung

hochwertige Information für erfahrene Spieler

“da lädt jemand nach” / “da hantiert jemand”

exakter als Stimme, subtiler als Gunshot



---

D. Voices / Funk / Rufe / Schreie

Rolle im Gameplay

Aktivität in einem Bereich erkennen

menschliche Präsenz lesen

Gruppen oder Patrouillen orten


Darstellung

Primär in der Welt, diffus und volumetrisch.

Visuelles Konzept

pulsierende rote Wolke / Aura / weicher Blob

nicht punktgenau

mehr räumliches Feld als klarer Punkt


Onscreen

rote pulsierende Region in Raum / Korridor / Fenster

zeigt “hier ist Kommunikation / menschliche Präsenz”


Offscreen

etwas diffuserer Blob oder Wandschimmer an plausibler Richtung

gut geeignet für Räume hinter Türen oder Stockwerke


Zielwirkung

Präsenz statt Präzision

Spieler erkennt Aktivitätszonen

nicht als exakte Zielhilfe gedacht



---

4. Darstellungsebenen: Welt vs Screen/UI

Primärsystem: Weltbasierte Darstellung

Alle Scanner-Audiohinweise sollten primär in der 3D-Welt stattfinden.

Gründe

immersiver

stilistisch passender

räumlich ehrlicher

kompatibel mit Occlusion, Wetter, Architektur und Artstyle


Weltbasierte Darstellung umfasst

Licht-/Farbimpulse

kurze painterly Wellen

Pulsflächen auf Boden / Wänden

volumetrische Blobs für Stimmen

präzise Sparks für Metall / Reload



---

Sekundärsystem: subtile Screen-Hinweise

UI/Screen-Darstellung sollte nur ein lesbarkeitsunterstützendes Backup sein.

Einsatz nur bei:

stark offscreen liegenden großen Ereignissen

sehr wichtigen Sounds

stark occluded / schwer lesbaren Raumlagen

vertikalen Mehrstock-Situationen


Form

Nicht:

Pfeile

Radar

Marker


Sondern:

kurzer roter Randschimmer

peripherer Brushstroke am Screenrand

Richtungshinweis ohne exakte UI


Empfehlung

Nur für:

Gunshots

Explosionen

eventuell sehr laute Schreie / Alarme


Nicht für:

Schritte

Reloads

kleine Interactions



---

5. Onscreen vs Offscreen — allgemeine Regeln

Onscreen

Wenn die Quelle im Sichtfeld des Spielers liegt:

Impuls direkt am Ursprung

klare Weltreaktion

beste Lesbarkeit

stärkerer Lokalisationswert


Offscreen

Wenn die Quelle nicht im Sichtfeld liegt:

Impuls weiterhin primär in der Welt

optional subtile periphere Hilfe

keine exakte Offenlegung der Quelle

bei Occlusion: stärker an Wänden / Öffnungen / Kanten zeigen


Occluded

Wenn zwischen Quelle und Spieler Wände liegen:

Impuls schwächer

diffuser

weniger präzise

eher “durch den Raum gedrückt” als “dort steht exakt jemand”



---

6. Distanzregeln

Nah

schärfer

heller

kürzer

präziser


Mittel

etwas diffuser

gut lesbar

mittlere Dauer


Weit

größer

diffuser

weniger präzise

bei Gunshots stark, bei Schritten fast gar nicht



---

7. Wetter- und Schleierintegration

Das Scanner-System soll direkt mit dem Schleier-System arbeiten.

Regen

allgemeiner Schleier leicht erhöht

Audio-Impulse bleiben sichtbar, aber etwas weicher

kleine Sounds werden schwerer lesbar


Sturm

allgemeiner Schleier stark erhöht

große Sounds dominieren

Schritte und kleine Interactions werden schwieriger

Impulse können leicht windgerichtet verzogen werden


Suppression

Gegner werden visuell schwerer lesbar

Scanner hilft, sie über Sound weiter zu verfolgen

Scanner ist also ein partielles Anti-Veil-Werkzeug



---

8. Audio-Mix im Scanner-Modus

Scanner soll nicht einfach “alles lauter” machen.
Er soll selektiv priorisieren.

Ambience

deutlich abgesenkt

Wind / Regen / Stadtnoise reduziert

nicht komplett weg


Relevante Sounds

Steps

Reloads

Voices

Funk

Gunshots

Interactions


Diese werden:

etwas lauter

klarer im transienten Bereich

mit größerem Wahrnehmungsradius versehen


Ziel

Der Spieler soll das Gefühl haben:

“Die Welt wird still”

“Wichtige Ereignisse treten aus dem Hintergrund hervor”



---

9. UE5-Implementierung


---

A. Scanner-Komponente

Erstelle z. B.:

BP_ScannerComponent

oder im Player direkt:

Zustände

bScannerActive
ScannerRangeMultiplier
ScannerVisualIntensity

Aufgaben

Scanner ein/aus

Audio-Balance umschalten

Sound-Events empfangen

visuelle Pulse spawnen



---

B. Sound Event Interface

Alle relevanten Sounds sollten ein Scanner-Event erzeugen.

Struktur

Jeder relevante Sound-Spawn ruft zusätzlich:

EmitScannerSoundPulse(
    WorldLocation,
    SoundType,
    Loudness,
    Radius,
    Duration,
    SourceActor
)

auf.

Das kann z. B. aus:

Gunshot-System

Footstep-Notifies

Reload-Events

Voice-System

Explosion-Actors


kommen.


---

C. VFX-Actor

Erstelle einen Actor:

BP_ScannerSoundPulse

Aufgaben

Darstellung eines Pulses in der Welt

abhängig von Typ, Radius, Dauer, Sichtbarkeit, Occlusion

Niagara / Decal / Mesh / Light-Kombination


Varianten

NS_Scanner_GunshotPulse

NS_Scanner_FootstepPulse

NS_Scanner_ReloadPulse

NS_Scanner_VoicePulse



---

D. Visuelle Umsetzung in UE5

Für Gunshots

Niagara System + Point Light + optional Decal

kurzer roter Expansionsimpuls

Licht beeinflusst Umgebung kurz


Für Schritte

kleine Niagara-Flecken oder Boden-Decals

an Fußkontakt oder Schallursprung


Für Reloads

kurzer Niagara Spark / kleine emissive pulse mesh


Für Voices

volumetrisches Niagara-Feld oder diffuse Glow Sphere



---

E. Sichtbarkeit / Onscreen / Offscreen prüfen

Vor dem Spawn oder bei Update:

Project World to Screen

prüfen:

liegt Quelle im Screen?

wie weit von Mitte / Rand?


daraus ableiten:

nur Weltimpuls

Weltimpuls + subtiler Randhint




---

F. Occlusion später

Später mit Steam Audio oder eigenem System:

OcclusionAmount in SoundPulse einfließen lassen

hoher Occlusion-Wert:

schwächer

diffuser

eher an Barrieren/Öffnungen visualisieren




---

10. Konkrete Klassifikationstabelle

Gunshots / Explosions

Welt: Ja, stark

Screen/UI: Ja, subtil offscreen

Darstellung: rote Schockwelle + kurzer Lichtimpuls + Stroke-Ausläufer


Footsteps

Welt: Ja

Screen/UI: Nein

Darstellung: kleine rhythmische Bodenimpulse


Reload / Weapon Handling / Metal

Welt: Ja

Screen/UI: Nein

Darstellung: kleine punktuelle Sparks / Klick-Impulse


Voices / Funk

Welt: Ja

Screen/UI: optional sehr subtil offscreen nur bei hoher Relevanz

Darstellung: diffuse pulsierende rote Wolke / Aktivitätsfeld


kleine Ambience / unwichtige Props

Welt: Nein oder minimal

Screen/UI: Nein

Darstellung: keine Scanner-Visualisierung



---

11. Gameplay-Regeln

Scanner soll nicht zu stark sein

keine exakten Dauer-Marker

keine permanenten Silhouetten

keine minimap-artige Offenlegung

Pulse sind kurzlebig


Gute Spieler lesen Muster

Schritte = Bewegung

Reload = Verwundbarkeit

Stimme = Gruppe / Aktivität

Gunshot = Konfliktzentrum


Scanner bleibt ein Wahrnehmungstool

Nicht:

Combat Assist Sondern:

Informationsmodus mit Kosten



---

12. Erweiterbarkeit

Das System ist vorbereitet für:

Wettereinfluss

Windverzerrung

Fraktionsspezifika

Veil-Kombinationen

Steam Audio Occlusion

Falsche / gestörte Pulse

Story-Events



---

13. Empfohlene erste Implementierungsreihenfolge

Phase 1

Scanner an/aus

Welt abstrakt machen

Gunshot-Pulse

Footstep-Pulse


Phase 2

Reload / Voice hinzufügen

Ambience-Reduktion

Audio-Radius-Modifikation


Phase 3

Offscreen-Randhinweise

Occlusion-Logik

Wetter-/Schleierintegration


Phase 4

Wind / Steam Audio / Propagation

falsche Impulse / Overload / Stress



---

14. Zusammenfassung

Der Scanner zeigt keine Gegner, sondern akustische Ereignisse als rote painterly Weltreaktionen.

Die Darstellung ist:

primär in der Welt

sekundär subtil am Screenrand

je nach Soundtyp unterschiedlich

für Onscreen und Offscreen getrennt lesbar

mit Wetter, Veil und später Occlusion kombinierbar
