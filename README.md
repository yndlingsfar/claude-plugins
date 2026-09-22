# yndlingsfar — Claude-Code-Plugins

Index-Repository für meine **öffentlichen** Claude-Code-Plugins. Hier liegt
**nur** die `marketplace.json`; jedes Plugin wohnt in seinem eigenen Repository
und wird dort versioniert.

Private Plugins gehören bewusst nicht in diesen Index — warum, steht unter
[Sichtbarkeit](#sichtbarkeit).

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

**Voraussetzung:** Das Ziel-Repository muss öffentlich sein. Sonst kippt der
Sync in Cowork — siehe unten.

## Warum ein eigenes Index-Repository

Die Alternative wäre, den Marketplace in eines der Plugin-Repositories zu
legen. Dann wäre dieses Repository gleichzeitig Plugin und Verzeichnis, und
sein Name stünde über Plugins, mit denen es nichts zu tun hat. Getrennt bleibt
jedes Plugin für sich versionierbar, und ein neues aufzunehmen ist eine Zeile.

## Sichtbarkeit

Dieses Repository ist **öffentlich**, und jedes hier verzeichnete Plugin-
Repository muss es ebenfalls sein. Das ist keine Stilfrage, sondern eine
harte Voraussetzung von Cowork.

**Der Fallstrick:** Cowork löst die Einträge aus `plugins[]` bereits beim
*Marketplace-Sync* auf, nicht erst beim Install — und dabei offenbar ohne die
Credentials des GitHub-Connectors. Ein einziges privates Ziel-Repository lässt
deshalb den **kompletten** Sync scheitern, mit der wenig hilfreichen Meldung
„Marketplace-Synchronisierung fehlgeschlagen. Überprüfe die Repository-URL."
Das passiert auch dann, wenn der Connector auf „All repositories" steht und
das Repo in der Auswahlliste auftaucht: Die Liste wird über die OAuth-Identität
befüllt und sieht alles, der Sync läuft über einen anderen Weg.

Im Terminal fällt das nicht auf. Die CLI holt die Sources erst beim Install und
nutzt dafür die lokalen Git-Credential-Helper — private Repos funktionieren
dort also problemlos.

**Konsequenz für private Plugins:** Sie kommen nicht in diesen Index. Ein
privates Plugin-Repository bekommt stattdessen seine eigene `marketplace.json`
mit `"source": "./"` und wird direkt als Marketplace eingebunden. Weil es dann
nichts Externes auflöst, synchronisiert es auch in Cowork sauber. So läuft
`yndlingsfar/productivity-buddy` (Plugin `productivity-todoist`), das deshalb
hier nicht gelistet ist.

Eine `marketplace.json` kann nicht beides zugleich sein: CLI-vollständig und
Cowork-tauglich. Dieser Index entscheidet sich für Cowork-tauglich.
