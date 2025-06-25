```java
void setup() {
  size(1200, 1000);
  Table daten = loadTable("amplitudes.csv", "header");

  float[] times = toArray(daten, "Time (s)");
  float[] dezibel = toArray(daten, "Sound pressure level (dB)");

  toGraph(times, dezibel);
}

float[] toArray(Table daten, String header) {
  float[] array = new float[daten.getRowCount()];

  for (int i = 0; i < daten.getRowCount(); i++) {
    TableRow row = daten.getRow(i);
    array[i] = row.getFloat(header);
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