# ME/CFS Monitoring

Application Android construite avec [Capacitor](https://capacitorjs.com/) à partir d'un fichier HTML single-page.

- **App ID** : `com.ulysseimpex.mecfsmonitoring`
- **Source web** : `www/index.html`
- **Plateforme** : Android (le dossier `android/` est régénéré à chaque build CI)

## Récupérer l'APK

À chaque push sur `main`, GitHub Actions construit un APK de debug et le publie comme artefact :

1. Aller dans l'onglet **Actions** du repo.
2. Ouvrir le dernier run **Build Android APK**.
3. Télécharger l'artefact `mecfs-monitoring-debug-apk` en bas de la page.

## Remplacer le HTML

Pour utiliser votre vrai contenu :

1. Copier votre fichier `suivi-sante-10.html` à la racine du repo.
2. Le déplacer/renommer en `www/index.html` (écraser le placeholder).
3. Si le fichier référence d'autres assets (images, CSS, JS), les placer dans `www/` également.
4. Commit + push sur `main` → CI rebuild l'APK.

## Build local (optionnel)

Prérequis : Node 20+, JDK 21, Android SDK (API 35).

```bash
npm install
npx cap add android        # première fois uniquement
npx cap sync android
cd android && ./gradlew assembleDebug
```

L'APK est dans `android/app/build/outputs/apk/debug/app-debug.apk`.

## Notes

- L'APK généré est **debug** : installable via `adb install` ou en activant les sources inconnues, mais non publiable sur le Play Store.
- Pour un APK release signé, il faudra ajouter un keystore et configurer les secrets GitHub (`KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`, `KEY_PASSWORD`) puis adapter le workflow.
