# Grundlage
## Arrays erstellen
Arrays sind eine Datenstruktur mit der mehrere Werte zusammen gespeichert werden können. Ein Array kan nur einen Datentyp speichern, welchen man beim Erzeugen festlegt.
```java
int[] a = {4, 0, -3}; // Array kann nur Zahlen vom Typ int speichern
float[] b = {4.25, 0.125, 0.3, -2.0} // Array kann nur Zahlen vom Typ float speichern
String[] c = {"hallo", "Max","Mustermann"}; // kann nur Strings speichern
int[] d = {"hallo", 2, 3}; // error: es können nur ints gespeichert werden, "hallo" ist aber ein String
```
Ist am Anfang der Inhalt des Arrays noch nicht bekannt, kann man auch ein Array mit einer gewünschten Größe festlegen und der Inhalt wird mit Platzhaltern gefüllt (denn ein Array kann nie "leer" sein).
```java
int[] a = new int[5]; // ergibt: [0, 0, 0, 0, 0]
String[] b = new String[3]; // ergibt: ["", "", ""]
```
## Werte auslesen
In Processing kann man sich den Inhalt eines Arrays mit `println(...)` ausgeben lassen:
```java
float[] b = {4.25, 0.125, 0.3, -2.0}
println(b);
/*
ergibt:
[0] 4.25
[1] 0.125
[2] 0.3
[3] -2.0
*/
```
Int der rechten Spalte sehen wir unseren Inhalt des Arrays und links nebendran wird die Stelle angezeigt, an der die Zahl gespeichert wird. Zu beachten ist hier also, dass Arrays in Java (und vielen anderen Programmiersprachen) bei `0` anfangen zu zählen.
 Möchten wir einen einzelnen Werte aus einem Array auslesen müssen wir dies also bedenken:
```java
float[] b = {4.25, 0.125, 0.3, -2.0}
println(b[0]); // ergibt: 4.25
println(b[3]); // ergibt: -2.0
println(b[4]); // error: IndexOutOfBound -> Wir dürfen außerhalb eines Arrays nicht zugreifen

float x = b[2] // 0.3 wird ausgelesen und in der Variablen x gespeichert
```
## Arrays verändern
Wir können auch einzelne Werte verändern:
```java
float[] b = {4.25, 0.125, 0.3, -2.0};
b[1] = 0;
/*
ergibt:
[0] 4.25
[1] 0
[2] 0.3
[3] -2.0
*/
```
  Das Array selbst merkt sich zusätzlich zum Inhalt auch seine Länge, also die Anzahl der gespeicherten Elemente.
```java
float[] b = {4.25, 0.125, 0.3, -2.0};
int laenge = b.length;
print(laenge); // ergibt: 4
```

## Array horizontal ausgeben
`println(...)` druckt ein Array in Processing vertikal in der Konsole. Für längere Arrays drucke ich Arrays gerne horizontal aus. Mit einer `for`-Schleife können wir auch jedes einzelne Element mit Hilfe von `print()` ohne Zeilenumbruch ausdrucken lassen. 
Mit `+ " "` fügen wir nach jeder Zahl noch ein Leerzeichen ein.
```java
void printHorizontal(int[] liste) {
  print("[");
  for (int i = 0; i < liste.length; i++) {
    print(liste[i] + " ");
  }
  println("]");
}
```

## Array mit zufälligen Zahlen befüllen

## Minimum und Maximum finden

## Array graphisch darstellen

---
### Gesamtlösung
```java
void setup() {
  size(500, 700);
  
  int[] top10 = new int[10];
  fillRandom(top10, 10, width - 50);
  
  toGraph(top10);
}

void toGraph(int[] liste) {
  int min = minimum(liste);
  int max = maximum(liste);

  int y = 10;
  for (int i = 0; i < liste.length; i++) {
    if (liste[i] == min) {
      fill(0, 255, 0);
    } else if (liste[i] == max) {
      fill(255, 0, 0);
    } else {
      fill(255);
    }
    rect(10, y, liste[i], 30);
    y += 35;
  }
}

int minimum(int[] liste) {
  int gemerkt = liste[0];
  for (int i = 0; i < liste.length; i++) {
    if (liste[i] < gemerkt) {
      gemerkt = liste[i];
    }
  }
  return gemerkt;
}

int maximum(int[] liste) {
  int gemerkt = liste[0];
  for (int i = 0; i < liste.length; i++) {
    if (liste[i] > gemerkt) {
      gemerkt = liste[i];
    }
  }
  return gemerkt;
}

void printHorizontal(int[] liste) {
  print("[");
  for (int i = 0; i < liste.length; i++) {
    print(liste[i] + " ");
  }
  println("]");
}

void fillRandom(int[] liste, int untereGrenze, int obereGrenze) {
  for (int i = 0; i < liste.length; i++) {
    liste[i] = (int)random(untereGrenze, obereGrenze);
  }
}
```