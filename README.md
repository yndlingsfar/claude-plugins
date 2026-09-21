# yndlingsfar — Claude-Code-Plugins

Index-Repository für meine Claude-Code-Plugins. Hier liegt **nur** die
`marketplace.json`; jedes Plugin wohnt in seinem eigenen Repository und wird
dort versioniert.

## Benutzen

```bash
/plugin marketplace add yndlingsfar/claude-plugins
/plugin install family-based-treatment@yndlingsfar
```

Nach Änderungen an einem Plugin:

```bash
/plugin marketplace update
```

## Enthaltene Plugins

| Plugin | Repository | Zweck |
|---|---|---|
| `productivity-todoist` | `yndlingsfar/productivity-buddy` | Todoist als Single Source of Truth für Tasks, plus Memory für Workplace-Shorthand |
| `family-based-treatment` | `yndlingsfar/family-based-treatment` | Mahlzeitenplanung, Kalorienbilanz und Rezeptanreicherung für familienbasiertes Refeeding |

## Ein Plugin hinzufügen

Einen Eintrag in `plugins[]` ergänzen. Das `source`-Objekt bestimmt, woher es
kommt — jeder Eintrag ist unabhängig:

```json
{
  "name": "neues-plugin",
  "source": { "source": "github", "repo": "yndlingsfar/neues-plugin" },
  "version": "0.1.0",
  "description": "Wozu es gut ist."
}
```

Neben `github` gehen auch `url` (beliebiger Git-Host), `git-subdir` (Plugin in
einem Unterverzeichnis eines Monorepos), `npm`, `archive` und ein relativer
Pfad `./…`, wenn das Plugin ausnahmsweise doch hier liegen soll. Eine Version
lässt sich mit `ref` (Branch oder Tag) oder `sha` festnageln, wenn ein Plugin
nicht ungefragt mitwandern soll.

## Warum ein eigenes Index-Repository

Die Alternative wäre, den Marketplace in eines der Plugin-Repositories zu
legen. Dann wäre dieses Repository gleichzeitig Plugin und Verzeichnis, und
sein Name stünde über Plugins, mit denen es nichts zu tun hat. Getrennt bleibt
jedes Plugin für sich versionierbar, und ein neues aufzunehmen ist eine Zeile.

## Sichtbarkeit

Dieses Repository und alle verzeichneten Plugin-Repositories sind **privat**.
Marketplaces funktionieren mit privaten Repositories; der Zugriff läuft über
die eigenen Git-Credentials.
