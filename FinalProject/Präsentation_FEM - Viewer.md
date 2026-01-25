---
marp: true
paginate: true
footer: "VIS3VO · Projekt FEM-Viewer · Gregor Lindmair"
backgroundColor: #ffffff
# Hier wird die Seitenzahl für die erste Folie global ausgeblendet
_paginate: false 
---

# FEM - Viewer: Projektfortschritt
## Implementierung & Erweiterte Funktionen
###### S2410566012

Gregor Lindmair
Master Maschinenbau
FH OÖ Wels

---

## Aktueller Stand der Applikation

Die Basis der GUI wurde um interaktive Steuerelemente und komplexe Visualisierungs-Logik erweitert.

**Hauptkomponenten:**
- **PyQt6** für das Interface (Menüs, Slider, Checkboxen)
- **PyVista** & **PyVistaQt** für das 3D-Rendering
- **NumPy** für die Vektorberechnung der Deformation

![w:500 h:250](Platzhalter: Screenshot der gesamten Benutzeroberfläche)

---

## Neue Kernfunktionen: Kamera-Steuerung

Um die Orientierung im 3D-Raum zu verbessern, wurden dedizierte Kamera-Tools implementiert:

- **Undo-Funktion:** Speichert die letzten 20 Kamerapositionen in einer Historie (`camera_history`).
- **Standard-Ansichten:** Schneller Wechsel zwischen Top, Front und Isometrisch (Shortcuts 1, 2, 3).
- **Save/Restore:** Manuelles Fixieren einer Ansicht (`Shift+C`).

![w:600 h:300](Platzhalter: Bild der Kamera-Menüs oder Viewports)

---

## Neue Kernfunktionen: Deformations-Analyse

Das Highlight der aktuellen Version ist die Darstellung von Verformungen.

- **Verschiebungsvektoren:** Automatisches Auslesen von "U" oder "displacement" Feldern.
- **Skalierungs-Slider:** Dynamische Skalierung der Verformung von 0.1x bis 1000x in Echtzeit.
- **Überlagerung:** Gleichzeitige Darstellung des undeformierten (Wireframe) und deformierten Modells.

![w:600 h:300](Platzhalter: Bild des deformierten Mesh mit Slider)

---

## Code-Struktur: Erweiterte Controls

Die Methode `create_controls` wurde massiv erweitert, um Interaktivität zu ermöglichen:

```python
# Auszug der neuen Steuerelemente
self.deform_checkbox = QCheckBox("Show Deformed")
self.deform_slider = QSlider(Qt.Orientation.Horizontal)
self.deform_slider.setRange(1, 10000) 

# Verknüpfung der Logik
self.deform_slider.valueChanged.connect(self.update_deformation)