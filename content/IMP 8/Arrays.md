```java
void setup() {
  int[] top10 = new int[10];
  myPrint(top10);
  fillRandom(top10);
  myPrint(top10);
  printMin(top10);
  printMax(top10);
}

void printMin(int[] liste) {
  int gemerkt = liste[0];
  for(int i = 0; i < liste.length; i++) {
    if (liste[i] < gemerkt) {
      gemerkt = liste[i];
    }
  }
  println(gemerkt);
}

void printMax(int[] liste) {
    int gemerkt = liste[0];
  for(int i = 0; i < liste.length; i++) {
    if (liste[i] > gemerkt) {
      gemerkt = liste[i];
    }
  }
  println(gemerkt);
}

void myPrint(int[] liste) {
  print("[");
  for (int i = 0; i < liste.length; i++) {
    print(liste[i] + " ");
  }
  println("]");
}

void fillRandom(int[] liste) {
  for (int i = 0; i < liste.length; i++) {
    liste[i] = (int)random(0, 71);
  }
}
```