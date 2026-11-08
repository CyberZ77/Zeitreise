# ZEITREISE – Android-Test-APK 0.5.14

Ein kleines Android-Projekt mit einem WebView-Container und derselben ZEITREISE-Oberfläche wie die HTML-Version.

## Architektur
- Die Hauptdatei **index.html** aus dem Repository wird beim APK-Bau nach `android/app/src/main/assets/index.html` kopiert. Im Git-Repository bleibt sie weiterhin die einzige App-HTML-Quelldatei.
- Die HTML-Datei liegt anschließend **in der APK**. Sie wird über `WebViewAssetLoader` von einer sicheren lokalen HTTPS-URL geladen.
- Die bestehenden Karten- und Ortsdaten-Anfragen benötigen Internet.
- Piper/Thorsten **ist absichtlich nicht in der APK enthalten**. Das Stimmmodell wird beim ersten Betätigen von „Hörprobe starten“ nachgeladen, sofern das Gerät und der Android-System-WebView die Browser-basierte Sprachausgabe unterstützen. OPFS kann die Modell-Datei im App-Datenbereich behalten.
- Die Android-App fordert GPS-Berechtigungen bei Bedarf an.
- Gesonderte Download-/Installationsverwaltung (inklusive weiblicher Stimme, Paketprüfung, Deinstallieren und unabhängig von Browser-Cache zuverlässiger Persistenz) ist **noch nicht implementiert**; dies ist eine Testversion.

## APK bauen
GitHub Actions → ZEITREISE Android APK → Run workflow, oder automatisch bei Änderungen an der HTML-Datei oder am Android-Projekt. Die Test-APK wird als GitHub-Actions-Artefakt bereitgestellt und zusätzlich als GitHub-Release unter dem Tag `android-preview-0.5.14`.

Lokal (Android-SDK 35 + Java 17 + Gradle 8.10.2):
```bash
mkdir -p android/app/src/main/assets
cp index.html icon.svg manifest.webmanifest android/app/src/main/assets/
cd android
gradle assembleDebug
```

Die erzeugte APK ist eine **Debug-Testversion**, nicht die signierte Store-Version. Die Browseransicht enthält die Stand-Version beim Bau; künftige Änderungen an index.html benötigen einen erneuten APK-Bau.
