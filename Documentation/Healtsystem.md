🩸 Health & Injury System — Dokumentation

Ziel des Systems

Das Health System soll:

Kämpfe gefährlich machen

Schusswaffen ernst wirken lassen

Treffer spürbar machen

aber Micromanagement vermeiden


Der Spieler soll seinen Zustand fühlen, nicht UI lesen.

Das System ist:

> ⭐ zonenbasiert
⭐ zustandsbasiert
⭐ feedback-driven
⭐ minimalistisch




---

🧠 Grundprinzip

Health ist kein einzelner Wert, sondern besteht aus:

Körperzonen

Head

Torso

Arms

Legs


Globale Zustände

Pain

BloodLoss

CriticalState



---

📦 Datenstruktur

Zone Health

HeadCurrent / HeadMax
TorsoCurrent / TorsoMax
ArmsCurrent / ArmsMax
LegsCurrent / LegsMax

Global

Pain (0-100)
BleedRate
bIsBleeding
bIsCritical
bIsDead


---

🎯 Vitalzonen

Head

Wenn Head <= 0
→ sofort Tod

Torso

Wenn Torso <= 0
→ Tod / Kampfunfähig

Arms / Legs

Nie sofort tödlich
→ erzeugen Debuffs


---

🔫 Schadensberechnung

Jede Waffe hat:

BaseDamage
PainDamage
BleedChance

Jede Zone hat:

DamageMultiplier
PainMultiplier
BleedMultiplier


---

Finaler Schaden

ZoneDamage = BaseDamage * ZoneMultiplier
Pain += PainDamage * PainMultiplier
BleedChance *= BleedMultiplier


---

⭐ Empfohlene Multipliers

Head  = 1.3
Torso = 1.0
Arms  = 0.7
Legs  = 0.75


---

❤️ Beispielwerte

Player

Head 35
Torso 85
Arms 90
Legs 100

Pistole

BaseDamage = 30
PainDamage = 18
BleedChance = 0.18


---

Ergebnis

Headshot → meist oneshot
Torso → ~3 Treffer
Arme/Beine → mehrere Treffer + Debuffs


---

🩸 Blutungssystem

BleedLevels (vereinfacht)

None

Light

Heavy


Oder minimal:

BleedRate > 0 = bleeding

Wirkung

Periodischer Schaden

steigende Pain

erhöht CriticalChance



---

😖 Pain System

Pain ist ein globaler Stresswert.

Er steigt durch:

Treffer

Explosionen

Suppression

Blutverlust



---

Pain beeinflusst

Gameplay

Aim Stability ↓

Recoil Control ↓

Scanner clarity ↓

Movement smoothness ↓


Audiovisuell

Veil intensiver

Audio dump / ringing

Atemgeräusche

Tunnelblick



---

⚠️ Critical State

Wird ausgelöst wenn:

Torso sehr niedrig

BleedRate hoch

mehrere Zonen stark verletzt


bIsCritical = true


---

Critical Effekte

stärkerer Veil

schwächeres Movement

langsamere Aktionen

stärkerer Audio Stress

evtl. Collapse



---

🧍‍♂️ Zonen-Debuffs

Arms low

mehr weapon sway

langsamer reload

schlechter recoil control


Legs low

weniger Sprint

geringere Geschwindigkeit

humpeln möglich


Torso low

Atmung hörbar

Suppression stärker

Scanner unstabiler



---

🧠 Unterschied Player vs AI

System ist identisch aufgebaut.

Aber:

Player

volle Feedbackschicht

Heilung möglich

Scanner beeinflusst


AI

vereinfachte Konsequenzen


Beispiele

Arme verletzt:

schlechter Aim


Beine verletzt:

langsamer chase


Torso verletzt:

Aggression sinkt


Head:

sofort Tod



---

💊 Healing

Minimalistisches System.

Items

Bandage

stoppt bleeding


Medkit

reduziert Pain

heilt etwas ZoneHealth


Optional später:

Splint → reduziert MovementPenalty



---

🎨 Visual Feedback (sehr wichtig)

Keine UI-Bars.

Zustand wird vermittelt durch:


---

Veil System Integration

Zustand	Veil Effekt

Light injury	leichte brush distortions
Heavy injury	stärkerer smear
Critical	Tunnel + fragmentierte blobs



---

Kamera Feedback

leichte Roll bei Pain

micro jitter

movement roughness



---

Weapon Feedback

mehr sway

unsauberer ADS

delayed firing readiness



---

Audio Feedback

gedämpfte ambience

ringing transient

Atem + Herzschlag

suppression intensiver



---

🌧 Umweltintegration

Health interagiert mit Welt:

Regen verstärkt blur

Sturm verstärkt Veil

Explosion erhöht Pain massiv

Wind trägt Sound → erhöht Stress



---

🤖 AI Wahrnehmung Health

AI kann Zustand erkennen:

verwundeter Player → aggressiver push

kritischer AI → retreat / panic


Das erzeugt emergentes Gameplay.


---

🎮 Gameplay Ziel

System soll erzeugen:

kurze gefährliche Kämpfe

taktische Bewegung wichtig

Treffer sind emotional spürbar

Heilung ist Entscheidung

Scanner wird Überlebenswerkzeug



---

⭐ Wichtigste Designregel

Health ist kein Zahlen-Puzzle, sondern:

> ein sensorisches Erlebnis



Spieler denkt:

„Ich bin verletzt“
nicht

„Ich habe noch 42 HP“



---

📈 Erweiterungen später

Armor zones

limb fracture states

bleeding types

stamina interaction

downed state

NPC surrender



---

🧱 Implementierungsarchitektur

Empfohlen:

BPC_Health

Funktionen:

ApplyHit()
ApplyZoneDamage()
StartBleeding()
StopBleeding()
AddPain()
EvaluateCritical()
HandleDeath()


---

⭐ Fazit

Dieses System ist:

realistischer als HP bar

viel weniger nervig als Tarkov

perfekt für immersive stylized shooter

eng verbunden mit deinem Veil / Scanner Konzept
