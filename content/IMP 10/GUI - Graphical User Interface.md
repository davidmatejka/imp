# Übersicht
1. [[GUI - Graphical User Interface#Bild laden]]
2. [[GUI - Graphical User Interface#Button erstellen]]
3. Funktionen für die Button schreiben
	1. [[GUI - Graphical User Interface#Schwarz-Weiß]]
	2. [[GUI - Graphical User Interface#Spieglen]]
	3. [[GUI - Graphical User Interface#Gauß-Filter]]
# Ziel dieser Einheit
Wir werden eine einfach Benutzeroberfläche (GUI - Graphical User Interface) schreiben, mit der wir eine Bildverarbeitung steuern können. Ein mögliches Layout, das für unsere Zwecke vollkommen ausreicht könnte so aussehen:
![[Layout-Light.png]]
In der oberen Hälfte befinden sich die Buttons, um zwischen den verschiedenen Bildverarbeitungen umzuschalten und die untere Hälfte zeigt als Referenz immer das Originalbild und das veränderte Bild.

# Bild laden
Mit Hilfe der Processing-Methode `loadImage(...)`[^1] lässt sich recht einfach ein Bild laden:
```java
PImage img;

void setup() {
  size(400,400);
  img = loadImage("flower.jpg");
  img.resize(400,400);
}

void draw() {
  image(img, 0, 0);
}
```

**Wichtig**: `loadImage(...)` nimmt den Dateipfad als Argument. Wenn man die Bilddatei in das Processing-Projekt platziert, reicht der Dateiname aus. Ansonsten muss der gesamt Dateipfad angegeben werden.
# Button erstellen
Für den Button erstellen wir in Processing einen neuen Tab, benennen ihn `Button` und schreiben folgenden Code rein.

```java
class Button {
  int x;
  int y;
  int breite;
  int hoehe;
  String beschriftung;

  public Button(int ix, int iy, int b, int h, String text) {
    x = ix;
    y = iy;
    breite = b;
    hoehe = h;
    beschriftung = text;
  }

  void zeichnen() {
    rect(x, y, breite, hoehe);
    fill(0);
    textSize(20);
    text(beschriftung, x+20, y+30);
    fill(255);
  }

  void clicked() {
    if (mouseX > x && mouseX < x + breite
      && mouseY > y && mouseY < y + hoehe
      ) {
      beschriftung = "clicked";
    }
  }
}
```

## Erklärung der Button-Klasse 
Ein Button können wir als Rechteck mit Text zeichnen. Genau das machen wir in `zeichnen()`. Wenn ein Button erstellt wird müssen wir die Informationen mitgeben, wo genau der Button und wie groß er gezeichnet werden soll und welcher Text darin stehen soll. Für die Erstellung eines Buttons wird `Button(...)` verwendet. 
Zum Beispiel:
```java
Button sw = new Button(20, 40, 100, 50, "sw");
```
Wir erzeugen einen neuen Button und geben die Werte `(20, 40, 100, 50, "sw")` weiter, welche wir in der Button-Klasse dann als `(x, y, breite, hoehe, text)` verwenden. Damit diese Informationen nicht verloren gehen, sobald `}` erreicht wird, speichern wir diese in den vordefinierten Variablen ab. Dann können diese Informationen in der `zeichnen()`-Methode verwendet werden.

Zur Überprüfung, ob der Button angeklickt wurde, vergleichen wir die Position des Mousezeigers zum Button. 
![[Button_Kollision.png]]
`mouseX` und `mouseY` gibt in Processing immer die aktuelle Position des Mauszeigers zurück. Der Mauszeiger befindet sich innerhalb des Rechtecks, wenn der Mauszeiger rechts `x` ist, aber kleiner als `x+breite`. Und die selbe Überlegung gilt für die y-Richtung:
```java
if (mouseX > x && mouseX < x + breite 
	&& mouseY > y && mouseY < y + hoehe
) {...}
```

### Den Button ausprobieren
Mit der fertigen Button-Klasse können wir nun die Hauptdatei entsprechend anpassen und den Button ausprobieren:
```java
PImage img;
Button sw;
Button spiegeln;

void setup() {
  size(400,400);
  img = loadImage("flower.jpg");
  img.resize(400,400);
  sw = new Button(20, 40, 100, 50, "sw");
  spiegeln = new Button(20, 100, 100, 50, "spiegeln");
}

void draw() {
  image(img, 0, 0);
  sw.zeichnen();
  spiegeln.zeichnen();
}

void mouseClicked() {
  sw.clicked();
  spiegeln.clicked();
}
```

Wir definieren die beiden Variablen `sw` und `spiegeln` zu Beginn als globale Variablen, damit alle Methoden darauf zugreifen können. In `setup()` initialisieren wir die beiden Buttons und können sie dann in `draw()` und `mouseClicked()` verwenden. 

Dies ist notwendig, weil die GUI auf Änderungen des Nutzers reagieren können muss. Da `setup()` aber nur einmal ausgeführt wird, benötigen wir `draw()`, welche **nach** `setup()` solange wiederholt ausgeführt wird, bis das Programm geschlossen wird. Wenn wir durch unsere Eingabe (z.B. durch Mausklick) etwas ändern, wird diese Änderung direkt gezeichnet.
# Funktionen für die Button schreiben
## Schwarz-Weiß
## Spieglen
## Gauß-Filter

[^1]: https://processing.org/reference/loadImage_.html