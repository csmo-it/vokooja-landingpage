# Deployment-Plan – Vokooja Landingpage

**Projekt:** Vokooja Landingpage  
**Kunde:** Vokooja  
**Domain:** vokooja.de (bei all-inkl)  
**Erstellt:** 2026-04-17  
**COO:** Bianca  
**Hosting:** All-Inkl  
**Deadline:** 2026-04-17, 18:00 UTC

---

## 📋 VORAUSSETZUNGEN

### **All-Inkl Account Zugänge benötigt:**

| Zugang | Beschreibung | Status |
|--------|--------------|--------|
| **FTP/SFTP** | Upload-Zugang zum Webspace | ⏳ Bereitstellen |
| **KAS (KundenAdministrationssystem)** | All-Inkl Control Panel | ⏳ Bereitstellen |
| **E-Mail** | SMTP-Zugang für Kontaktformular | ⏳ Bereitstellen |

---

## 🗄️ SCHRITT 1: DATENBANK (OPTIONAL)

**Hinweis:** Vokooja Landingpage ist statisch (HTML/CSS/JS) – keine Datenbank erforderlich!

**Falls Kontaktformular mit PHP-Mail:**
```
Keine Datenbank nötig – Formular sendet direkt via PHP mail() oder SMTP
```

---

## 🌐 SCHRITT 2: DOMAIN & SSL KONFIGURIEREN

### **2.1 DNS-Einstellungen prüfen**

```
1. KAS Login → https://kas.all-inkl.com
2. Menü: Domainverwaltung → vokooja.de
3. DNS-Einträge prüfen:
   - A-Record: Zeigt auf All-Inkl Server-IP
   - www CNAME: Zeigt auf vokooja.de
4. SSL-Zertifikat aktivieren:
   - KAS → SSL → Let's Encrypt
   - Domain auswählen → "Jetzt bestellen" (kostenlos)
   - Aktivierung dauert ca. 5-10 Minuten
```

### **2.2 HTTPS Redirect einrichten**

```apache
# .htaccess (im Webroot-Verzeichnis: /www/htdocs/w0xxxxxx/)
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

---

## 📁 SCHRITT 3: DATEIEN HOCHLADEN

### **3.1 FTP-Upload**

```
1. FTP-Client öffnen (FileZilla, Cyberduck, etc.)
2. Verbindung herstellen:
   - Host: ftp.your-domain.de (oder Server-IP von All-Inkl)
   - Benutzer: w0xxxxxx (von All-Inkl)
   - Passwort: [dein FTP-Passwort]
   - Port: 21 (FTP) oder 22 (SFTP empfohlen)
3. Lokaler Ordner: /home/clawadmin/.openclaw/workspace-ceo-orchestrator/projekte/vokooja-landingpage/
4. Remote-Ordner: /www/htdocs/w0xxxxxx/ (Webroot bei All-Inkl)
5. Alle Dateien hochladen:
   ✅ index.html
   ✅ impressum.html
   ✅ datenschutz.html
   ✅ /css/ (gesamter Ordner)
   ✅ /js/ (gesamter Ordner)
   ✅ /assets/ (gesamter Ordner)
```

### **3.2 Datei-Struktur nach Upload:**

```
/www/htdocs/w0xxxxxx/          (Webroot)
├── index.html                 (Hauptseite)
├── impressum.html             (Rechtstexte)
├── datenschutz.html           (Datenschutz)
├── css/
│   ├── style.css
│   └── responsive.css
├── js/
│   └── main.js
└── assets/
    ├── images/
    │   ├── logo.png
    │   ├── hero-bg.jpg
    │   └── ...
    └── icons/
        └── favicon.ico
```

---

## ⚙️ SCHRITT 4: KONTAKTFORMULAR KONFIGURIEREN

### **4.1 PHP-Mailer einrichten (wenn vorhanden)**

```php
// contact.php (im Webroot erstellen)
<?php
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $name = htmlspecialchars($_POST['name']);
    $email = htmlspecialchars($_POST['email']);
    $message = htmlspecialchars($_POST['message']);
    
    $to = "info@vokooja.de";
    $subject = "Neue Kontaktanfrage von $name";
    $body = "Name: $name\nEmail: $email\n\nNachricht:\n$message";
    $headers = "From: noreply@vokooja.de\r\nReply-To: $email";
    
    if (mail($to, $subject, $body, $headers)) {
        echo "✅ Nachricht gesendet!";
    } else {
        echo "❌ Fehler beim Senden!";
    }
}
?>
```

### **4.2 Alternative: SMTP mit PHPMailer**

```php
// PHPMailer installieren (empfohlen für bessere Zustellung)
// composer require phpmailer/phpmailer

// smtp-config.php
<?php
use PHPMailer\PHPMailer\PHPMailer;

$mail = new PHPMailer(true);
$mail->isSMTP();
$mail->Host = 'smtp.all-inkl.com';
$mail->SMTPAuth = true;
$mail->Username = 'info@vokooja.de';
$mail->Password = '[dein E-Mail-Passwort]';
$mail->SMTPSecure = 'tls';
$mail->Port = 587;
?>
```

### **4.3 Formular in HTML anpassen:**

```html
<!-- index.html → Kontaktformular -->
<form action="contact.php" method="POST">
    <input type="text" name="name" required>
    <input type="email" name="email" required>
    <textarea name="message" required></textarea>
    <button type="submit">Senden</button>
</form>
```

---

## 🔒 SCHRITT 5: SICHERHEITSEINSTELLUNGEN

### **5.1 .htaccess Security**

```apache
# /www/htdocs/w0xxxxxx/.htaccess

# Schutz vor Directory Listing
Options -Indexes

# XSS-Schutz
<IfModule mod_headers.c>
    Header set X-XSS-Protection "1; mode=block"
    Header set X-Content-Type-Options "nosniff"
    Header set X-Frame-Options "SAMEORIGIN"
</IfModule>

# Cache-Control für statische Dateien
<IfModule mod_expires.c>
    ExpiresActive On
    ExpiresByType text/css "access plus 1 month"
    ExpiresByType application/javascript "access plus 1 month"
    ExpiresByType image/jpeg "access plus 1 year"
    ExpiresByType image/png "access plus 1 year"
</IfModule>
```

### **5.2 robots.txt erstellen**

```
# /www/htdocs/w0xxxxxx/robots.txt
User-agent: *
Allow: /

Sitemap: https://vokooja.de/sitemap.xml
```

### **5.3 sitemap.xml erstellen (optional)**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
    <url>
        <loc>https://vokooja.de/</loc>
        <lastmod>2026-04-17</lastmod>
        <priority>1.0</priority>
    </url>
    <url>
        <loc>https://vokooja.de/impressum.html</loc>
        <lastmod>2026-04-17</lastmod>
        <priority>0.5</priority>
    </url>
    <url>
        <loc>https://vokooja.de/datenschutz.html</loc>
        <lastmod>2026-04-17</lastmod>
        <priority>0.5</priority>
    </url>
</urlset>
```

---

## ✅ SCHRITT 6: GO-LIVE CHECKLISTE

### **6.1 Vor Go-Live:**

```
□ Alle Dateien hochgeladen (FTP-Check)
□ index.html lädt korrekt
□ impressum.html erreichbar
□ datenschutz.html erreichbar
□ CSS/JS geladen (keine 404-Fehler)
□ Bilder werden angezeigt
□ Kontaktformular testweise senden
□ HTTPS Redirect funktioniert
□ Mobile Ansicht prüfen (Responsive)
```

### **6.2 Nach Go-Live:**

```
□ Google Search Console: Seite einreichen
□ Google Analytics: Tracking-Code prüfen (falls vorhanden)
□ Social Media: OG-Tags testen (https://developers.facebook.com/tools/debug/)
□ Backup erstellt (lokale Kopie + All-Inkl Backup-Funktion)
```

---

## 🚨 ROLLBACK-PLAN

### **Falls Probleme auftreten:**

```
1. FTP-Zugang herstellen
2. Alte Dateien wiederherstellen (lokales Backup)
3. Oder: All-Inkl Backup-Funktion nutzen
   - KAS → Backup → Website-Backup
   - Letzten funktionierenden Stand wiederherstellen
4. DNS-Check: Zeigt Domain auf richtigen Server?
```

---

## 📞 SUPPORT-KONTAKTE

| Service | Kontakt |
|---------|---------|
| **All-Inkl Support** | https://all-inkl.com/support/ |
| **All-Inkl Hotline** | +49 3574 3699-0 |
| **KAS-Hilfe** | https://kas.all-inkl.com/hilfe/ |

---

## 📝 DEPLOYMENT-STATUS

| Schritt | Status | Datum |
|---------|--------|-------|
| 1. Datenbank (optional) | ⏳ Ausstehend | - |
| 2. Domain & SSL | ⏳ Ausstehend | - |
| 3. Dateien hochladen | ⏳ Ausstehend | - |
| 4. Kontaktformular | ⏳ Ausstehend | - |
| 5. Sicherheit | ⏳ Ausstehend | - |
| 6. Go-Live Check | ⏳ Ausstehend | - |

---

**GitHub:** https://github.com/csmo-it/agency-bots/tree/master/vokooja-landingpage/docs/
