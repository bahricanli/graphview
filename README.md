# GraphView

Android için çizgi, çubuk ve nokta grafik kütüphanesi. [jjoe64/GraphView](https://github.com/jjoe64/graphview) projesinin Android SDK 34 ile güncellenmiş fork'u.

## Kurulum

**settings.gradle** dosyanıza JitPack reposunu ekleyin:

```gradle
dependencyResolutionManagement {
    repositories {
        maven { url 'https://jitpack.io' }
    }
}
```

**build.gradle** (uygulama modülü) dosyanıza bağımlılığı ekleyin:

```gradle
dependencies {
    implementation 'com.github.bahricanli:graphview:1.0.1'
}
```

## Kullanım

### Layout XML

```xml
<com.jjoe64.graphview.GraphView
    android:id="@+id/graph"
    android:layout_width="match_parent"
    android:layout_height="300dp" />
```

### Çizgi Grafik (LineGraphSeries)

```java
GraphView graph = findViewById(R.id.graph);

LineGraphSeries<DataPoint> series = new LineGraphSeries<>(new DataPoint[]{
    new DataPoint(0, 1),
    new DataPoint(1, 5),
    new DataPoint(2, 3),
    new DataPoint(3, 2),
    new DataPoint(4, 6)
});

graph.addSeries(series);
```

### Çubuk Grafik (BarGraphSeries)

```java
BarGraphSeries<DataPoint> series = new BarGraphSeries<>(new DataPoint[]{
    new DataPoint(1, 4),
    new DataPoint(2, 8),
    new DataPoint(3, 2),
    new DataPoint(4, 6)
});

graph.addSeries(series);
```

### Nokta Grafik (PointsGraphSeries)

```java
PointsGraphSeries<DataPoint> series = new PointsGraphSeries<>(new DataPoint[]{
    new DataPoint(0, 1),
    new DataPoint(1, 5),
    new DataPoint(2, 3)
});

series.setShape(PointsGraphSeries.Shape.TRIANGLE);
graph.addSeries(series);
```

## Özellikler

### Viewport (Görünüm Alanı)

```java
// Manuel eksen sınırları
graph.getViewport().setXAxisBoundsManual(true);
graph.getViewport().setMinX(0);
graph.getViewport().setMaxX(10);

graph.getViewport().setYAxisBoundsManual(true);
graph.getViewport().setMinY(0);
graph.getViewport().setMaxY(100);

// Kaydırma ve zoom
graph.getViewport().setScrollable(true);
graph.getViewport().setScalable(true);
```

### Eksen Etiketleri

```java
// Statik etiketler
StaticLabelsFormatter formatter = new StaticLabelsFormatter(graph);
formatter.setHorizontalLabels(new String[]{"Pzt", "Sal", "Çar", "Per", "Cum"});
graph.getGridLabelRenderer().setLabelFormatter(formatter);

// Tarih formatı
graph.getGridLabelRenderer().setLabelFormatter(
    new DateAsXAxisLabelFormatter(this)
);
```

### Grafik Başlığı ve Etiket Özelleştirme

```java
graph.setTitle("Haftalık Veri");
graph.getGridLabelRenderer().setHorizontalAxisTitle("Gün");
graph.getGridLabelRenderer().setVerticalAxisTitle("Değer");
graph.getGridLabelRenderer().setNumHorizontalLabels(5);
```

### Çizgi Grafik Stili

```java
series.setColor(Color.RED);
series.setThickness(4);
series.setDrawBackground(true);
series.setBackgroundColor(Color.argb(50, 255, 0, 0));
series.setDrawDataPoints(true);
series.setDataPointsRadius(8f);
```

### Veri Noktasına Tıklama

```java
series.setOnDataPointTapListener((series1, dataPoint, x, y) -> {
    Toast.makeText(this, "X: " + dataPoint.getX() + ", Y: " + dataPoint.getY(), Toast.LENGTH_SHORT).show();
});
```

### Legend (Açıklama Kutusu)

```java
series.setTitle("Sıcaklık");
graph.getLegendRenderer().setVisible(true);
graph.getLegendRenderer().setAlign(LegendRenderer.LegendAlign.TOP);
```

### İkinci Y Ekseni

```java
LineGraphSeries<DataPoint> series2 = new LineGraphSeries<>(...);
graph.getSecondScale().addSeries(series2);
graph.getSecondScale().setMinY(0);
graph.getSecondScale().setMaxY(500);
```

## Modül Yapısı

| Modül | Açıklama |
|---|---|
| `graphview` | Kütüphane modülü |
| `graphviewdemo` | Örnek uygulama |

## Gereksinimler

- minSdk: 24
- targetSdk: 34
- Java 8

## Lisans

```
Copyright 2016 Jonas Gehring

Licensed under the Apache License, Version 2.0
```
