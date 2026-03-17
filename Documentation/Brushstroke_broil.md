Bei so einem Sprite-Effekt passiert “Edge Breakup” nicht über echte Geometrieverzerrung, sondern fast immer über:

1. Opacity Breakup an den Rändern


2. optional leichte UV-Distortion des Smoke-Textures


3. optional weiche Erosion, die an den Kanten stärker ist als in der Mitte



Das ist genau das, was du willst.


---

Das Ziel

Dein Smoke soll nicht wie ein perfekter weicher Kreis/Sprite aussehen, sondern:

Rand leicht fransig

Brush-Textur schneidet unregelmäßig in die Kante

Mitte bleibt voller

Boil lässt die Kante lebendig wirken


Also:

> die Brush-Textur soll vor allem die Randbereiche beeinflussen



Nicht die gesamte Opacity gleich stark.


---

Die Kernidee

Du baust eine Edge Mask für den Sprite und benutzt diese, um die Brush-Textur nur an den Kanten stark wirken zu lassen.

Formel grob

FinalOpacity =
BaseSmokeOpacity
*
DepthFade
*
EdgeBrokenMask

Und:

EdgeBrokenMask =
Lerp(1.0, BrushMask, EdgeInfluence)

wobei EdgeInfluence in der Mitte klein und am Rand groß ist.


---

So baust du das konkret


---

1. Erzeuge eine Edge Mask aus den Sprite-UVs

Nimm TexCoord oder deine Particle SubUV UVs.

Nodes

TexCoord
→ Subtract(0.5, 0.5)
→ Length

Das gibt dir den Abstand zur Mitte.

Nenne das:

Radius

Dann:

Radius
→ Multiply
→ OneMinus / Subtract von 1
→ Saturate

Aber für deinen Fall noch besser:

Kantenmaske bauen

Du willst:

Mitte = 0

Rand = 1


Also:

EdgeMask = Saturate( (Radius - EdgeStart) / EdgeWidth )

Gute Startwerte

EdgeStart = 0.25
EdgeWidth = 0.2

Oder praktisch mit Nodes:

Subtract(Radius, 0.25)

Divide by 0.2

Saturate


Dann ist:

in der Mitte fast 0

am Rand Richtung 1



---

2. Benutze deine Brush-Textur als Breakup Mask

Du hast die Brush schon per MF_PainterlyBroil am Laufen.

Nimm daraus:

BrushSample = TextureSample(BrushTex, UV_OUT).R

Dann optional:

BrushSample → Power(1.3 bis 1.8)
→ Saturate

Das macht die Struktur schöner lesbar.

Nenne das:

BrushMask


---

3. Brush nur am Rand stark einwirken lassen

Jetzt kombinierst du beides.

A. Soft-Version

EdgeBreakup = Lerp(1.0, BrushMask, EdgeMask * BreakupStrength)

Gute Startwerte

BreakupStrength = 0.5 bis 0.8

Das heißt:

Mitte fast unberührt

Rand bekommt Brush-Breakup



---

B. Stärkere Version

Wenn du mehr fransige Löcher willst:

EdgeBrush = Lerp(1.0, BrushMask, EdgeMask)
FinalOpacity = BaseOpacity * DepthFade * EdgeBrush

Oder aggressiver:

EdgeBrush = 1 - (EdgeMask * (1 - BrushMask))

Aber fürs erste ist Lerp am besten.


---

4. Deine Base Smoke Opacity definieren

Gerade nutzt du ungefähr:

ParticleSubUV Alpha

mal ParticleColor Alpha

mal DepthFade


Das ist okay, aber sauberer wäre:

BaseSmokeOpacity =
ParticleSubUV.A
*
ParticleColor.A

Dann:

FinalOpacity =
BaseSmokeOpacity
*
DepthFade
*
EdgeBreakup

Und das geht in:

Opacity Override


---

Konkrete Node-Reihenfolge

Ausgehend von deinem aktuellen Material:


---

A. Base Smoke Opacity

Nimm:

Particle SubUV Alpha
*
Particle Color Alpha

Das ist deine Grund-Opacity.


---

B. Edge Mask

Baue neu:

TexCoord
→ Subtract(0.5, 0.5)
→ Length
→ Subtract(0.25)
→ Divide(0.2)
→ Saturate
= EdgeMask

Optional:

EdgeMask → Power(1.2 bis 1.8)

für schärfere Kontrolle.


---

C. Brush Sample

Das hast du schon fast:

MF_PainterlyBroil → UV_OUT
→ Texture Sample (BrushTex)
→ R
→ Power(1.4)
→ Saturate
= BrushMask


---

D. Edge Breakup

Neu:

Lerp
A = 1.0
B = BrushMask
Alpha = EdgeMask * BreakupStrength

Setz:

BreakupStrength = 0.7

Ergebnis:

EdgeBreakupMask


---

E. Final Opacity

Dann:

BaseSmokeOpacity
*
DepthFade
*
EdgeBreakupMask

= Opacity Override


---

5. Noch besser: Brush auch leicht in die Form reinziehen

Wenn du nicht nur Opacity, sondern auch die wahrgenommene Kante “verzerren” willst, kannst du die Brush noch leicht auf das Smoke-Texture-Sampling anwenden.

Idee

Nicht nur:

Brush maskiert die Opacity


sondern:

Brush verzerrt leicht die SubUV / Alpha



---

Variante

Nimm deine UV_OUT oder einen daraus abgeleiteten Offset und addiere ihn ganz leicht auf die Particle SubUV UV.

Aber Achtung: Particle SubUV arbeitet mit dem Flipbook/Atlas, da willst du nicht zu aggressiv verzerren.

Sicherer Weg:

Verzerr lieber nur eine zusätzliche Noise-/Mask-Textur, nicht den Flipbook selbst.

Für Smoke ist meistens:

> Opacity breakup reicht schon, um die Kante deutlich painterly zu machen.




---

6. Noch mehr Handpainted-Look

Wenn du den Rand noch unperfekter willst, mach zwei Brush Samples.

Beispiel

BrushA = Sample(BrushTex, UV_OUT).R
BrushB = Sample(BrushTex, UV_OUT * 1.13 + float2(0.07, 0.03)).R
BrushCombined = Lerp(BrushA, BrushB, 0.5)

Dann:

BrushCombined → Power → Saturate

Das gibt organischere Kanten.


---

7. Beste Variante für dich: Edge Erosion

Noch näher an “Rauch wird unregelmäßig weggeknabbert”:

Erosion Setup

Erosion = 1 - (EdgeMask * ErodeStrength)

Dann mit Brush kombinieren:

EdgeBreakup =
Lerp(1.0, BrushMask, EdgeMask)

Oder härter:

EdgeBreakup = Saturate(BrushMask + (1 - EdgeMask))

Aber das ist schon aggressiver.

Für deinen Stand würde ich erstmal bei der Lerp-Variante bleiben.


---

8. Gute Startwerte

Edge Mask

EdgeStart = 0.22 bis 0.3
EdgeWidth = 0.18 bis 0.28

Brush

Brush Power = 1.4
BreakupStrength = 0.65 bis 0.8

Boil

Für Smoke eher:

BoilStrength_Local = 0.003 bis 0.008
BoilScale = 1.0 bis 2.0


---

9. Was du wahrscheinlich direkt sehen willst

Die einfachste konkrete Änderung in deinem Material:

Neu hinzufügen

EdgeMask Block:

TexCoord
→ Subtract(0.5, 0.5)
→ Length
→ Subtract(0.25)
→ Divide(0.2)
→ Saturate

BrushSample aus deinem Boil:

MF_PainterlyBroil → TextureSample.R → Power(1.4)

Dann:

Lerp(1.0, BrushSample, EdgeMask * 0.7)

Und dieses Ergebnis multiplizierst du mit:

DepthFade * BaseOpacity

→ in Opacity Override

Das sollte sofort deutlich painterly wirken.


---

10. Wenn du willst, dass die Kante “mehr verzogen” statt nur “mehr gelöchert” wirkt

Dann brauchst du zusätzlich einen kleinen UV Vector Offset aus der Brush.

Dafür wäre die nächste bessere Version deiner Function:

MF_PainterlyBroil

nicht nur UV_OUT, sondern zusätzlich:

BrushVectorOut
BrushMaskOut

Zum Beispiel:

ein Brush-Sample in R und G

-0.5 zentrieren

daraus Vector2 machen


Dann könntest du:

deine Alpha-Mask oder Noise leicht verzerren


Aber für dein jetziges Material ist:

> Edge Breakup über Opacity
erstmal die richtige und einfachste Lösung.
