# Sonos Jukebox – Bubble Card Modul

Ein vollständiger Sonos-Player als Modul für die [Bubble Card](https://github.com/Clooos/Bubble-Card)
**Media Player**, optisch im Stil der übrigen Bubble Cards.

*English: A full Sonos player module for Bubble Card's media player – favorites, Spotify jukebox,
room grouping with per-speaker volume and EQ, and the play queue. UI is German.*

## Funktionen

- **Player** – großes oder kompaktes Cover, Titel/Interpret, Fortschritt zum Spulen, Zufall,
  Wiederholen, Gruppen-Lautstärke, Stummschalten und Sleep-Timer
- **Favoriten** – Sonos-Favoriten mit Cover, nach Radio und Titeln gruppiert; was läuft, ist markiert
- **Jukebox**
  - Spotify-Link einfügen (Playlist, Album, Titel, Podcast) → *Abspielen*, *Als Nächstes* oder *Anhängen*
  - eigene feste Playlists als Kacheln (Name und Cover kommen automatisch von Spotify)
  - Playlists aus der Spotify-Integration von Home Assistant, mit Suche
- **Räume** – Lautsprecher per Tippen zur Gruppe hinzufügen/entfernen, eigene Lautstärke pro Raum,
  *Alle Räume* / *Nur dieser Raum*, Klang pro Lautsprecher (Bass, Höhen, Balance, Loudness, Überblenden …)
- **Warteschlange** – aktuelle Queue, Titel antippen zum Springen, Titel entfernen

## Voraussetzungen

- Home Assistant mit der **Sonos**-Integration
- **Bubble Card** ab v3.3 und **Bubble Card Tools** (für den Modul-Editor)
- Für Spotify-Links: Spotify ist in der **Sonos-App** verknüpft
- Optional: **Spotify**-Integration in Home Assistant für die Bibliothek

## Installation

1. Bei einer beliebigen Bubble Card den Bereich **Modules** öffnen → **Import** →
   den Inhalt von [`sonos_jukebox.yaml`](sonos_jukebox.yaml) einfügen und speichern.
2. Eine Bubble Card vom Typ **Media Player** mit einem Sonos-Lautsprecher anlegen
   (am besten in einem Pop-up) und das Modul `sonos_jukebox` aktivieren:

```yaml
type: custom:bubble-card
card_type: media-player
entity: media_player.wohnzimmer
modules:
  - sonos_jukebox
sonos_jukebox:
  accent_color: "#ffc47e"
```

Weitere Beispiele: [`examples/popups.yaml`](examples/popups.yaml)

## Optionen

Alle Optionen lassen sich auch im Karten-Editor unter *Modules → Sonos Jukebox* einstellen.

| Option | Standard | Beschreibung |
|---|---|---|
| `accent_color` | Bubble-Akzent | Hex-Farbe (`#ffc47e`) oder HA-Farbname (`orange`) |
| `accent_text_color` | Textfarbe | Icon-/Textfarbe auf der Akzentfarbe |
| `player_layout` | `large` | `large` (Cover oben) oder `compact` (Cover links) |
| `cover_size` | `280` | maximale Cover-Größe in px |
| `show_cover` / `cover_glow` | `true` | Cover bzw. Farbschimmer im Hintergrund |
| `strip_sonos` | `true` | „Sonos“ aus Lautsprechernamen entfernen |
| `tabs` | alle | Auswahl aus `favorites`, `jukebox`, `rooms`, `queue` |
| `default_tab` / `remember_tab` | `favorites` / `true` | Startbereich, zuletzt genutzten merken |
| `favorite_columns` | `3` | Spalten bei den Favoriten |
| `playlists` | – | Liste aus `uri` (Spotify-Link), optional `name`, `image`, `icon` |
| `jukebox_title` / `jukebox_columns` | `Deine Jukebox` / `2` | Überschrift und Spalten der eigenen Playlists |
| `show_link_input` | `true` | Feld zum Einfügen von Spotify-Links |
| `show_spotify_library` / `autoload_library` | `true` | Spotify-Bibliothek anzeigen / automatisch laden |
| `library_columns` | `3` | Spalten der Spotify-Bibliothek |
| `shuffle_on_play` | `false` | beim Abspielen einer Playlist Zufallswiedergabe einschalten |
| `speakers` | alle Sonos | Lautsprecher im Bereich *Räume* |
| `show_eq` | `true` | Klangeinstellungen pro Lautsprecher |
| `show_base_card` | `false` | ursprüngliche Media-Player-Leiste zusätzlich zeigen |

## Hinweise

- Spotify-Links werden über die Sonos-Integration als *Share-Link* abgespielt.
- Die Restzeit des Sleep-Timers stellt die Sonos-Integration nicht bereit; das Modul merkt sich
  den Ablaufzeitpunkt deshalb lokal im Browser.
- Namen und Cover eigener Playlists holt das Modul über Spotifys öffentlichen oEmbed-Dienst.

## Aufbau

Das ganze Modul steckt in [`sonos_jukebox.yaml`](sonos_jukebox.yaml): CSS und JavaScript im Abschnitt `code`, das Formular für den Karten-Editor im Abschnitt `editor`.

## Lizenz

[MIT](LICENSE)
