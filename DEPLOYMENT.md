# Vokooja Landing Page – Deployment Guide

**Target:** all-inkl Hosting (vokooja.app)

---

## 📋 **INHALT:**

1. [Voraussetzungen](#voraussetzungen)
2. [Datei-Struktur](#datei-struktur)
3. [Deployment-Schritte](#deployment-schritte)
4. [.htaccess-Config](#htaccess-config)
5. [Domain-Setup](#domain-setup)
6. [SSL-Zertifikat](#ssl-zertifikat)
7. [Testing](#testing)

---

## ✅ **VORAUSSETZUNGEN:**

- all-inkl Hosting-Account (KAS-Zugang)
- Domain: vokooja.app (bei all-inkl verwaltet)
- FTP-Zugangsdaten
- PHP 8.0+ (optional, für statische Seite nicht erforderlich)

---

## 📁 **DATEI-STRUKTUR:**

```
vokooja-landingpage/
├── index.html          → Hauptseite
├── impressum.html      → Impressum
├── datenschutz.html    → Datenschutz
├── css/
│   └── style.css       → Stylesheet
├── js/
│   └── main.js         → JavaScript
├── assets/
│   ├── logo-agency.png → Logo (PNG)
│   └── logo-agency.svg → Logo (SVG)
└── DEPLOYMENT.md       → Diese Datei
```

---

## 🚀 **DEPLOYMENT-SCHRITTE:**

### Option A: FTP (Empfohlen)

```bash
# 1. FTP-Client öffnen (FileZilla, Cyberduck, etc.)
# 2. Verbinden mit all-inkl FTP-Server
#    - Host: wxyz.kasserver.com (ersetzte wxyz durch deine KAS-ID)
#    - User: wxyz
#    - Passwort: Dein FTP-Passwort
#    - Port: 21

# 3. Dateien hochladen nach:
#    /htdocs/vokooja.app/

# 4. Datei-Struktur auf Server:
#    /htdocs/vokooja.app/
#    ├── index.html
#    ├── impressum.html
#    ├── datenschutz.html
#    ├── css/style.css
#    ├── js/main.js
#    └── assets/
#        ├── logo-agency.png
#        └── logo-agency.svg
```

### Option B: KAS File-Manager

```
1. KAS öffnen: https://kas.all-inkl.com/
2. "Dateiverwaltung" → "Web-FTP"
3. Navigieren zu: /htdocs/vokooja.app/
4. Dateien per Drag & Drop hochladen
```

### Option C: Git (wenn verfügbar)

```bash
# Auf Server (SSH falls verfügbar):
cd /htdocs/vokooja.app/
git clone https://github.com/csmo-it/agency-bots.git temp
mv temp/vokooja-landingpage/* .
rm -rf temp
```

---

## 🔧 **.HTACCESS-CONFIG:**

**Datei:** `/htdocs/vokooja.app/.htaccess`

```apache
# HTTPS erzwingen
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

# WWW zu Non-WWW (oder umgekehrt)
RewriteCond %{HTTP_HOST} ^www\.vokooja\.app$ [NC]
RewriteRule ^(.*)$ https://vokooja.app/$1 [R=301,L]

# Custom Error Pages (optional)
ErrorDocument 404 /404.html
ErrorDocument 500 /500.html

# Browser Caching
<IfModule mod_expires.c>
  ExpiresActive On
  ExpiresByType text/html "access plus 1 hour"
  ExpiresByType text/css "access plus 1 week"
  ExpiresByType application/javascript "access plus 1 week"
  ExpiresByType image/png "access plus 1 month"
  ExpiresByType image/svg+xml "access plus 1 month"
</IfModule>

# Security Headers
<IfModule mod_headers.c>
  Header set X-Content-Type-Options "nosniff"
  Header set X-Frame-Options "SAMEORIGIN"
  Header set X-XSS-Protection "1; mode=block"
</IfModule>
```

---

## 🌐 **DOMAIN-SETUP:**

### In KAS konfigurieren:

```
1. KAS → "Domainverwaltung"
2. Domain: vokooja.app
3. "Bearbeiten" → "Verzeichnis zuweisen"
4. Verzeichnis: /htdocs/vokooja.app/
5. Speichern
```

### DNS-Einträge (falls nötig):

```
Typ: A
Name: vokooja.app
Wert: 123.45.67.89 (all-inkl Server-IP)

Typ: CNAME
Name: www
Wert: vokooja.app
```

---

## 🔒 **SSL-ZERTIFIKAT:**

### all-inkl Let's Encrypt (kostenlos):

```
1. KAS → "SSL-Zertifikate"
2. "Let's Encrypt Zertifikat erstellen"
3. Domain: vokooja.app
4. Subdomains: www (optional)
5. E-Mail für Benachrichtigungen
6. "Erstellen"
7. Warte ~5-10 Min auf Aktivierung
```

### SSL-Status prüfen:

```bash
# Browser: https://vokooja.app
# Oder: https://www.sslshopper.com/ssl-checker.html#hostname=vokooja.app
```

---

## ✅ **TESTING-CHECKLISTE:**

### Vor Deployment:

```
✅ index.html lädt lokal
✅ Alle Links funktionieren
✅ Bilder werden angezeigt
✅ CSS lädt korrekt
✅ JavaScript funktioniert
✅ Responsive Design getestet (Desktop + Mobile)
```

### Nach Deployment:

```
✅ https://vokooja.app lädt
✅ HTTPS-Umlenkung funktioniert
✅ www → Non-WWW Umlenkung
✅ Alle internen Links funktionieren
✅ Bilder werden geladen
✅ Mobile-Ansicht korrekt
✅ SSL-Zertifikat gültig
✅ PageSpeed Score > 80
```

---

## 🔍 **TROUBLESHOOTING:**

### 404 Fehler:
```
→ Prüfe Verzeichnis-Zuweisung in KAS
→ Prüfe Dateipfade (case-sensitive!)
→ .htaccess auf Syntax-Fehler prüfen
```

### SSL nicht aktiv:
```
→ Warte 10 Min nach Zertifikat-Erstellung
→ Browser-Cache leeren
→ HTTPS in .htaccess erzwingen
```

### Bilder nicht sichtbar:
```
→ Pfade prüfen: assets/logo-agency.png
→ Dateirechte: 644 für Dateien, 755 für Ordner
→ Case-Sensitivity beachten (Linux!)
```

---

## 📊 **DATEIRECHTE:**

```bash
# Empfohlene Rechte:
chmod 644 index.html impressum.html datenschutz.html
chmod 644 css/style.css
chmod 644 js/main.js
chmod 644 assets/*
chmod 755 css/ js/ assets/
```

---

## 🎯 **NEXT STEPS NACH DEPLOYMENT:**

| Task | Prio | Status |
|------|------|--------|
| Domain-Setup in KAS | 🔴 HIGH | ⏳ Felix |
| SSL-Zertifikat | 🔴 HIGH | ⏳ Felix |
| FTP-Upload | 🔴 HIGH | ⏳ Felix/COO |
| Testing | 🟡 MEDIUM | ⏳ COO/QA |
| Google Analytics (optional) | 🟢 LOW | ⏳ CMO |
| Google Search Console | 🟢 LOW | ⏳ CMO |

---

## 📞 **SUPPORT:**

Bei Deployment-Problemen:

- all-inkl Support: https://all-inkl.com/support/
- KAS-Doku: https://all-inkl.com/kas/
- CTO kontaktieren für technische Issues

---

*Stand: 2026-04-17 | Ready for Deployment*
