# Novex Releases

Canal public centralisé des applications Novex.

Ce dépôt ne contient aucun code source applicatif. Les installateurs vérifiés sont publiés comme assets dans GitHub Releases. Le dossier `apps/` expose un manifeste `latest.json` par application afin que Showcase et les applications installées puissent résoudre leur propre canal sans dépendre de la release globale la plus récente du dépôt.

## Contrat de manifeste

Chaque `apps/<app-id>/latest.json` utilise `novex-release-channel/v1`.

État sans artefact publié :

```json
{
  "schema": "novex-release-channel/v1",
  "appId": "example-app",
  "status": "unavailable",
  "release": null
}
```

État disponible :

```json
{
  "schema": "novex-release-channel/v1",
  "appId": "example-app",
  "status": "available",
  "release": {
    "version": "1.0.0",
    "tag": "example-app-v1.0.0",
    "publishedAt": "2026-09-01T00:00:00.000Z",
    "asset": {
      "name": "Example-App-Setup-1.0.0.exe",
      "url": "https://github.com/dbkloh/Novex-Releases/releases/download/example-app-v1.0.0/Example-App-Setup-1.0.0.exe",
      "sha256": "64-caracteres-hexadecimaux-minuscules",
      "size": 1
    }
  }
}
```

Un manifeste `available` n'est valide que si l'asset existe réellement, si son URL appartient aux Releases de ce dépôt, et si sa taille et son SHA-256 correspondent à l'artefact publié.

## Règles de publication

- Aucun binaire n'est commité dans Git.
- Aucun token, secret, code source privé ou état interne Novex n'est publié.
- Une release applicative part de `prod`; `main` est admise uniquement lorsqu'un projet ne possède pas de branche `prod`.
- Le manifeste reste `unavailable` tant qu'aucun installateur réel et vérifié n'a été publié.
