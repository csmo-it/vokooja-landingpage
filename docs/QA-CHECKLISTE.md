# QA-Checkliste – Vokooja Landingpage

**Projekt:** Vokooja Landingpage  
**Kunde:** Vokooja  
**Domain:** vokooja.de (bei all-inkl)  
**Erstellt:** 2026-04-17  
**COO:** Bianca  
**Deadline:** 2026-04-17, 18:00 UTC

---

## 📋 ÜBERSICHT

| Kategorie | Tests | Status | % Fertig |
|-----------|-------|--------|----------|
| **Frontend-Tests** | 6 | ⏳ Offen | 0% |
| **Responsive-Tests** | 4 | ⏳ Offen | 0% |
| **Performance-Tests** | 3 | ⏳ Offen | 0% |
| **SEO-Tests** | 4 | ⏳ Offen | 0% |
| **GESAMT** | **17** | ⏳ **OFFEN** | **0%** |

---

## ✅ FRONTEND-TESTS

### **F1: HTML-Validierung**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🔴 KRITISCH |
| **Test** | W3C Validator |
| **Erwartet** | 0 Fehler, 0 Warnungen |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. https://validator.w3.org/ öffnen
2. URL eingeben: vokooja.de
3. "Check" klicken
4. Ergebnis: 0 Fehler, 0 Warnungen
```

**Go/No-Go:** ❌ Bei Fehlern → Fixen

---

### **F2: CSS-Validierung**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟡 MITTEL |
| **Test** | W3C CSS Validator |
| **Erwartet** | 0 Fehler |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. https://jigsaw.w3.org/css-validator/ öffnen
2. URL eingeben: vokooja.de
3. "Check" klicken
4. Ergebnis: 0 Fehler
```

**Go/No-Go:** ⚠️ Bei wenigen Fehlern → Akzeptabel

---

### **F3: JavaScript-Funktionalität**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🔴 KRITISCH |
| **Test** | Browser Console |
| **Erwartet** | 0 Errors, 0 Warnings |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. vokooja.de in Chrome öffnen
2. F12 → Console Tab
3. Seite neu laden (F5)
4. Ergebnis: 0 Errors, 0 Warnings
```

**Go/No-Go:** ❌ Bei Errors → Fixen

---

### **F4: Alle Links funktionieren**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🔴 KRITISCH |
| **Test** | Link-Check |
| **Erwartet** | 0 defekte Links |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. https://www.deadlinkchecker.com/ öffnen
2. URL eingeben: vokooja.de
3. "Start Scan" klicken
4. Ergebnis: 0 defekte Links (intern + extern)
```

**Go/No-Go:** ❌ Bei defekten Links → Fixen

---

### **F5: Kontaktformular funktioniert**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🔴 KRITISCH |
| **Test** | Formular-Test |
| **Erwartet** | E-Mail wird gesendet |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. vokooja.de → Kontaktformular
2. Test-Daten eingeben
3. Absenden
4. E-Mail-Empfang prüfen (info@vokooja.de)
```

**Go/No-Go:** ❌ Wenn E-Mail nicht ankommt → Fixen

---

### **F6: Impressum & Datenschutz verlinkt**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🔴 KRITISCH |
| **Test** | Rechtstexte-Check |
| **Erwartet** | Beide Seiten erreichbar |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. vokooja.de → Footer prüfen
2. "Impressum" klicken → Seite lädt
3. "Datenschutz" klicken → Seite lädt
4. Beide Seiten: Vollständige Texte
```

**Go/No-Go:** ❌ Wenn fehlend → Sofort nachfügen

---

## 📱 RESPONSIVE-TESTS

### **R1: Mobile Ansicht (<768px)**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🔴 KRITISCH |
| **Test** | Mobile Viewport |
| **Erwartet** | Alle Inhalte lesbar |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. Chrome DevTools öffnen (F12)
2. Device Toolbar aktivieren (Strg+Shift+M)
3. "iPhone 12 Pro" auswählen (390x844)
4. Seite prüfen:
   - Texte lesbar?
   - Bilder skaliert?
   - Navigation bedienbar?
```

**Go/No-Go:** ❌ Wenn nicht lesbar → CSS fixen

---

### **R2: Tablet Ansicht (768px-1024px)**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟡 MITTEL |
| **Test** | Tablet Viewport |
| **Erwartet** | Layout angepasst |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. Chrome DevTools → Device Toolbar
2. "iPad Air" auswählen (820x1180)
3. Seite prüfen:
   - Layout korrekt?
   - Keine horizontalen Scrollbars?
```

**Go/No-Go:** ⚠️ Minor Issues akzeptabel

---

### **R3: Desktop Ansicht (>1024px)**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟢 NIEDRIG |
| **Test** | Desktop Viewport |
| **Erwartet** | Original-Design |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. Browser auf Fullscreen (1920x1080)
2. vokooja.de laden
3. Design mit Mockup vergleichen
```

**Go/No-Go:** ⚠️ Minor Abweichungen akzeptabel

---

### **R4: Orientation Switch (Portrait/Landscape)**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟡 MITTEL |
| **Test** | Rotation |
| **Erwartet** | Kein Layout-Bruch |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. Mobile View (Device Toolbar)
2. Rotation umschalten (90° / 0°)
3. Layout-Brüche prüfen
```

**Go/No-Go:** ⚠️ Minor Issues akzeptabel

---

## ⚡ PERFORMANCE-TESTS

### **P1: PageSpeed Score**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟢 NIEDRIG |
| **Test** | Google PageSpeed |
| **Erwartet** | >80 (Mobile), >90 (Desktop) |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. https://pagespeed.web.dev/ öffnen
2. URL: vokooja.de
3. "Analyze" klicken
4. Ergebnis notieren:
   - Mobile: ___ / 100
   - Desktop: ___ / 100
```

**Go/No-Go:** ⚠️ >70 akzeptabel für statische Seite

---

### **P2: Ladezeit**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟢 NIEDRIG |
| **Test** | GTmetrix |
| **Erwartet** | <3s Fully Loaded |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. https://gtmetrix.com/ öffnen
2. URL: vokooja.de
3. "Test your site" klicken
4. Ergebnis: Fully Loaded Time <3s
```

**Go/No-Go:** ⚠️ <5s akzeptabel

---

### **P3: Bild-Optimierung**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟡 MITTEL |
| **Test** | Bildgrößen-Check |
| **Erwartet** | Alle Bilder <500KB |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. Chrome DevTools → Network Tab
2. Seite neu laden
3. Alle Bilder filtern (Img)
4. Größe prüfen: Alle <500KB?
```

**Go/No-Go:** ⚠️ Einzelne große Bilder akzeptabel

---

## 🔍 SEO-TESTS

### **S1: Meta-Tags vorhanden**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🔴 KRITISCH |
| **Test** | Meta-Tag-Check |
| **Erwartet** | title, description, viewport |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. vokooja.de → Rechtsklick → "Seitenquelltext anzeigen"
2. <head>-Bereich prüfen:
   - <title>Vokooja ...</title>
   - <meta name="description" content="...">
   - <meta name="viewport" content="width=device-width, ...">
```

**Go/No-Go:** ❌ Wenn fehlend → Sofort nachfügen

---

### **S2: Open Graph Tags**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟡 MITTEL |
| **Test** | OG-Tag-Check |
| **Erwartet** | og:title, og:description, og:image |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. Seitenquelltext öffnen
2. Nach og:-Tags suchen:
   - <meta property="og:title" content="...">
   - <meta property="og:description" content="...">
   - <meta property="og:image" content="...">
```

**Go/No-Go:** ⚠️ Optional für statische Seite

---

### **S3: Semantisches HTML**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟢 NIEDRIG |
| **Test** | HTML-Struktur |
| **Erwartet** | header, nav, main, footer |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. Seitenquelltext öffnen
2. Struktur prüfen:
   - <header> vorhanden?
   - <nav> für Navigation?
   - <main> für Hauptinhalt?
   - <footer> für Footer?
```

**Go/No-Go:** ⚠️ Nicht kritisch für statische Seite

---

### **S4: Robots.txt & Sitemap**

| Kriterium | Wert |
|-----------|------|
| **Priorität** | 🟢 NIEDRIG |
| **Test** | SEO-Files |
| **Erwartet** | robots.txt vorhanden |
| **Status** | ⏳ Offen |

**Test-Schritte:**
```
1. vokooja.de/robots.txt aufrufen
2. Inhalt prüfen:
   - User-agent: *
   - Allow: /
3. Optional: sitemap.xml
```

**Go/No-Go:** ⚠️ Optional für kleine Seite

---

## 🚀 GO/NO-GO ENTSCHEIDUNG

### **KRITISCHE TESTS (Alle müssen bestehen):**

| Test | Status |
|------|--------|
| F1: HTML-Validierung | ⏳ Offen |
| F3: JavaScript-Funktionalität | ⏳ Offen |
| F4: Alle Links funktionieren | ⏳ Offen |
| F5: Kontaktformular | ⏳ Offen |
| F6: Impressum & Datenschutz | ⏳ Offen |
| R1: Mobile Ansicht | ⏳ Offen |
| S1: Meta-Tags | ⏳ Offen |

### **GESAMT-URTEIL:**

```
Bestanden: ___ / 17 Tests
Kritisch offen: ___
Empfehlung: ⏳ AUSSTEHEND
```

---

## 📝 NOTIZEN

| Datum | Notiz | Status |
|-------|-------|--------|
| 2026-04-17 | QA-Checkliste erstellt | ✅ Fertig |

---

**GitHub:** https://github.com/csmo-it/agency-bots/tree/master/vokooja-landingpage/docs/
