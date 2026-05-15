# AiGrafCad
# 🤖 AI-CAD Tool

> **3D-Objekte aus Text-Prompts und Fotos generieren — powered by Claude AI**

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey)]()
[![API](https://img.shields.io/badge/API-Anthropic%20Claude-orange)](https://console.anthropic.com/)

---

## 📖 Was ist das?

AI-CAD Tool ist eine Desktop-Anwendung, die natürliche Sprache in druckfertige 3D-Modelle umwandelt. Beschreibe einfach was du bauen möchtest — das Tool generiert automatisch den passenden CAD-Code, rendert ihn und zeigt das Ergebnis in einem interaktiven 3D-Viewer an.

**Kein CAD-Wissen notwendig. Kein komplexes Modellieren. Einfach beschreiben.**

---

## ✨ Features

| Feature | Beschreibung |
|---|---|
| 🗣️ **Text zu 3D** | Natürliche Sprache direkt in 3D-Modell |
| 📷 **Foto zu 3D** | Referenzbild hochladen, AI analysiert und modelliert |
| 🌐 **Browser-Viewer** | Interaktiver 3D-Viewer (drehen, zoomen, verschieben) |
| 💾 **STL-Export** | Direkt in Slicer (Cura, PrusaSlicer) laden |
| 🔒 **Lokaler API-Key** | Key wird nur lokal gespeichert, nie übertragen |
| 🖥️ **Dark UI** | Modernes dunkles Interface |
| 📦 **Leichtgewichtig** | Nur ~50 MB (ohne schwere CAD-Bibliotheken) |

---

## 🖼️ Screenshots

> *3D-Viewer öffnet sich automatisch im Browser nach der Generierung*

---

## 🚀 Schnellstart

### Voraussetzungen

- Python 3.9 oder neuer → [python.org/downloads](https://www.python.org/downloads/)
- OpenSCAD → [openscad.org/downloads](https://openscad.org/downloads.html)
- Anthropic API Key (kostenlos) → [console.anthropic.com](https://console.anthropic.com/settings/keys)

### Installation

```bash
# Repository klonen
git clone https://github.com/Graf-d/ai-cad-tool.git
cd ai-cad-tool

# Abhängigkeiten installieren
pip install anthropic Pillow

# Tool starten
python ai_cad_tool.py
```

### Beim ersten Start

1. **API Key** eingeben und auf 💾 klicken (wird lokal gespeichert)
2. **Prompt** eingeben, z.B.:
   - *"Raspberry Pi 5 Gehäuse 100x75x40mm, 2mm Wandstärke, abgerundete Kanten"*
   - *"Lüftungsgitter für 200mm PC-Lüfter mit Logo VASTL in der Mitte"*
   - *"L-Halterung für 20mm Rohr, 3mm Stärke, 4 Schraubenlöcher"*
3. **⚡ Generieren** klicken
4. 3D-Viewer öffnet sich automatisch im Browser

---

## 💡 Prompt-Beispiele

```
Raspberry Pi 5 Gehäuse: 100mm breit, 75mm tief, 40mm hoch,
2mm Wandstärke, abgerundete Kanten 3mm, Deckel abnehmbar

Lüftungsgitter 200mm PC-Lüfter: korrekte Schraubenabstände M4,
konzentrisches Gittermuster, Schriftzug "VASTL" in der Mitte

Zahnrad: 12 Zähne, Außendurchmesser 50mm, Breite 8mm, Bohrung 8mm

Kamerahalterung: GoPro-kompatibel, 20mm Schiene, 2 Sicherungsschrauben
```

---

## 🏗️ Architektur

```
Nutzer-Prompt
      │
      ▼
Claude AI (Anthropic API)
      │ generiert OpenSCAD-Code
      ▼
OpenSCAD (lokal, eingebettet)
      │ rendert STL-Datei
      ▼
Browser-Viewer (Three.js)
      │ zeigt 3D-Modell
      ▼
STL-Export → Slicer → 3D-Drucker
```

**Warum OpenSCAD statt CadQuery/FreeCAD?**
OpenSCAD ist eine schlanke, scriptbasierte CAD-Engine (~50 MB) die sich perfekt für KI-generierte parametrische Modelle eignet. Schwere Alternativen (CadQuery + OpenCASCADE) wären >1.5 GB und schwer zu verteilen.

---

## 📁 Projektstruktur

```
ai-cad-tool/
├── ai_cad_tool.py          # Haupt-Anwendung
├── build_installer.bat     # Windows EXE Builder
├── ai_cad_setup.iss        # Inno Setup Installer-Skript
├── requirements.txt        # Python-Abhängigkeiten
├── README.md               # Diese Datei
├── LICENSE                 # MIT Lizenz
└── .gitignore
```

---

## 🔧 Für Entwickler

### Windows EXE erstellen

1. [OpenSCAD portable ZIP](https://openscad.org/downloads.html) in den Projektordner legen
2. [Inno Setup](https://jrsoftware.org/isdl.php) installieren
3. Build starten:
   ```
   .\build_installer.bat
   ```
4. Installer liegt unter `Output\AI-CAD-Tool-Setup.exe`

### Abhängigkeiten

```
anthropic    # Claude API Client
Pillow       # Logo-Rendering in der GUI
```

OpenSCAD wird als externe Binary eingebunden (nicht über pip).

---

## 🔐 Datenschutz & API-Key

- Der API-Key wird **ausschließlich lokal** gespeichert: `%USERPROFILE%\.ai_cad_config.json`
- Es werden **keine Daten** außer dem Prompt an die Anthropic API gesendet
- Generierte Modelle bleiben **lokal auf deinem PC**
- Der Key ist **nicht** im Programmcode oder in der EXE enthalten

---

## 🤝 Beitragen

Pull Requests sind willkommen! Für größere Änderungen bitte zuerst ein Issue öffnen.

1. Fork erstellen
2. Feature Branch: `git checkout -b feature/MeinFeature`
3. Committen: `git commit -m 'Add MeinFeature'`
4. Push: `git push origin feature/MeinFeature`
5. Pull Request öffnen

---

## 📋 Roadmap

- [ ] Mehrsprachige Prompts verbessern
- [ ] Modell-Bibliothek (gespeicherte Generierungen)
- [ ] Batch-Generierung mehrerer Varianten
- [ ] STEP-Export für professionelle CAD-Software
- [ ] macOS / Linux Installer

---

## 📄 Lizenz

MIT License — siehe [LICENSE](LICENSE)

---

## 👤 Autor

**Graf_d**
- Email: grafde90@gmail.com
- GitHub: [@Graf-d](https://github.com/Graf-d)

---

## 🙏 Danksagung

- [Anthropic Claude](https://anthropic.com) — KI-Engine
- [OpenSCAD](https://openscad.org) — CAD-Rendering
- [Three.js](https://threejs.org) — 3D-Browser-Viewer
