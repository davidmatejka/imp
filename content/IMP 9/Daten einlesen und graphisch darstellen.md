# Ziel
Gegeben ist eine csv-Datei mit Messwerten eines Lärmpegels gemessen in Dezibell(dB) pro Zeit in Sekunden (s). Ziel ist es diese Messwerte einzulesen und grafisch aufzubereiten. Die Lösung wird im folgenden noch erklärt.

## Code Lösung
```java
void setup() {
  size(1200, 1000);
  Table daten = loadTable("amplitudes.csv", "header");

  float[] times = toArray(daten, "Time (s)");
  float[] dezibel = toArray(daten, "Sound pressure level (dB)");

  toGraph(times, dezibel);
}

float[] toArray(Table daten, String columnName) {
  float[] array = new float[daten.getRowCount()];

  for (int i = 0; i < daten.getRowCount(); i++) {
    TableRow row = daten.getRow(i);
    array[i] = row.getFloat(columnName);
  }
  return array;
}

float maximum(float[] db) {
  float max = db[0];
  for (int i = 0; i < db.length; i++) {
    if (db[i] > max) max = db[i];
  }
  return max;
}

void toGraph(float[] xValues, float[] yValues) {
  float xFactor = maximum(xValues) / width;
  float yFactor = maximum(yValues) / height;

  for (int i = 0; i < xValues.length - 1; i++) {
    float x1 = xValues[i];
    float y1 = yValues[i];
    float x2 = xValues[i + 1];
    float y2 = yValues[i + 1];

    x1 /= xFactor;
    y1 /= yFactor;
    x2 /= xFactor;
    y2 /= yFactor;

    strokeWeight(0.2);
    line(x1, height - y1, x2, height - y2);
  }
}
```
# Einlesen
In Processing gibt es einige Methoden, die das einlesen vereinfachen. Wichtig dazu ist, dass die Datei, die eingelesen werden soll, in dem selben Ordner wie die sketch-Datei von Processing ist. Das macht das Einlesen am einfachsten.

```java
 Table daten = loadTable("amplitudes.csv","header");
```

`loadTable()`[^1] ist eine Methode in Processing. Man gibt ihr den Dateinamen und mit "header" gibt man der Methode die Information, dass die erste Zeile in der Datei eine Kopfzeile ist.
Wir speichern die eingelesenene Informationen unter der Variable `daten`, welche vom Typ `Table` ist.

## Daten in Arrays aufteilen
Damit wir die Daten korrekt auf unsere durch `size()` festgelegte Größe zeichnen können, müssen wir vorher wissen, wir groß die Werte für die Zeit und für die Dezibel jeweils werden. Deswegen wandeln wir die jeweiligen Daten in Arrays um, um dann davon das Maximum zu suchen.
```java
  float[] times = toArray(daten, "Time (s)");
  float[] dezibel = toArray(daten, "Sound pressure level (dB)");
```

Wir schreiben dazu `toArray()`:
``` java
float[] toArray(Table daten, String columnName) {
  float[] array = new float[daten.getRowCount()];

  for (int i = 0; i < daten.getRowCount(); i++) {
    TableRow row = daten.getRow(i);
    array[i] = row.getFloat(columnName);
  }
  return array;
}
```

Der Rückgabewert ist `float[]`, da die Zeiten und die Dezibel beide Kommazahlen enthalten. Wir erstellen zuerst ein Array und legen die Größe mithilfe von `daten.getRowCount()` fest, welche uns die Anzahl der Zeilen in der eingelesenen Datei gibt. (Diese und weitere Methoden, die auf `Table` verwendet werden können, kann man unter https://processing.org/reference/Table.html nachlesen.)
Danach durchlaufen wir alle Zeilen unserer Daten 

[^1]: https://processing.org/reference/loadTable_.html