# DevForge Store

Catalogue d’applications one-click pour [DevForge](https://github.com/bobdivx/devforge).

Les listings publiés depuis une application **en cours d’exécution** sont stockés dans DevForge. Ce dépôt décrit le format JSON du catalogue (export / listings officiels).

## Publier depuis DevForge

1. Déployez une application jusqu’à ce qu’elle soit fonctionnelle (`running`).
2. Ouvrez l’application → **Publier sur le Store**.
3. Choisissez les variables d’environnement à **inclure** ou à **oublier**.
4. Définissez les valeurs par défaut (jamais les secrets).
5. Ajustez les paramètres runtime (build pack, ports, commandes, healthcheck).

## Installer

Sur DevForge, ouvrez **Store**, choisissez une app, renseignez les secrets demandés et cliquez sur **Installer**. DevForge crée l’application, applique les défauts, puis déploie.

## Format d’un listing (`apps/<slug>.json`)

Voir [`schema/listing.v1.json`](schema/listing.v1.json). Exemple :

```json
{
  "schema_version": 1,
  "slug": "hello-static",
  "name": "Hello Static",
  "description": "Site statique de démonstration.",
  "category": "web",
  "git_repository": "owner/hello-static",
  "git_branch": "main",
  "runtime_defaults": {
    "build_pack": "static",
    "is_static": true,
    "ports_exposes": "80",
    "base_directory": "/",
    "publish_directory": "/dist"
  },
  "env_schema": [
    {
      "key": "PUBLIC_SITE_NAME",
      "is_secret": false,
      "required": false,
      "default": "Hello",
      "description": "Nom affiché",
      "is_runtime": true,
      "is_buildtime": true
    },
    {
      "key": "API_TOKEN",
      "is_secret": true,
      "required": true,
      "default": null,
      "description": "Jeton API (saisi à l’installation)",
      "is_runtime": true,
      "is_buildtime": false
    }
  ]
}
```

Les valeurs secrètes ne sont **jamais** stockées dans le catalogue.
