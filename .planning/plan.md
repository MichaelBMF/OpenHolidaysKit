# OpenHolidaysKit

## Zweck

`OpenHolidaysKit` ist als neues öffentliches Monorepo geplant. Ziel ist eine portable
Feiertags-Engine mit gemeinsamer Datenbasis und zwei
nativen Implementierungen:

- Swift Package: `OpenHolidaysKit`
- Kotlin Multiplatform Library: `OpenHolidaysKotlin`
- Gemeinsame Spezifikation, Daten und Golden Tests im Repo `OpenHolidaysKit`

Dieser Plan beschreibt das eigenständige Projekt. Konsumierende Apps und deren Adapter sind bewusst
nicht Teil dieses Plans.

## Ausgangspunkt

- Es gibt bereits eine kleine, separat entstandene Bayern-V1-Referenzlogik, die als fachlicher
  Startpunkt für erste Golden Fixtures dienen kann.
- `date-holidays` ist fachlich die wichtigste Referenz, weil es umfangreiche YAML-Daten unter
  `data/countries` und eine etablierte JS-Regel-Engine hat.

## Namensentscheidung

- Repository/Familie: `OpenHolidaysKit`
- Swift Package/Product: `OpenHolidaysKit`
- Kotlin Module/Artifact: `open-holidays-kotlin`
- Kotlin API Name: `OpenHolidaysKotlin`
- Gemeinsame Daten/Spec: `OpenHolidays Data`

Begründung:

- `OpenHolidays` ist bereits stark mit dem bestehenden OpenHolidays-API-Ökosystem assoziiert.
- `OpenHolidaysKit` ist auf GitHub nach aktueller Prüfung nicht als exaktes Repo prominent belegt.
- `Kit` passt gut zur Swift-Seite; durch das Monorepo bleibt der Projektname trotzdem
  sprachübergreifend nutzbar.

## Geplante Repository-Struktur

```text
OpenHolidaysKit/
├─ README.md
├─ LICENSE
├─ NOTICE.md
├─ CONTRIBUTING.md
├─ .github/
│  └─ workflows/
│     ├─ ci.yml
│     └─ sync-date-holidays.yml
├─ data/
│  ├─ LICENSE.md
│  ├─ sources/
│  │  └─ date-holidays/
│  │     ├─ UPSTREAM.md
│  │     ├─ LICENSE
│  │     └─ countries/
│  ├─ generated/
│  └─ attributions/
├─ specs/
│  ├─ license-and-data.md
│  ├─ date-holidays-sync.md
│  ├─ rule-language.md
│  ├─ data-schema.md
│  ├─ api-contract.md
│  ├─ test-and-parity.md
│  ├─ release-and-packaging.md
│  └─ compatibility.md
├─ swift/
│  ├─ Package.swift
│  ├─ Sources/OpenHolidaysKit/
│  └─ Tests/OpenHolidaysKitTests/
├─ kotlin/
│  ├─ build.gradle.kts
│  ├─ settings.gradle.kts
│  └─ src/
│     ├─ commonMain/kotlin/
│     ├─ commonTest/kotlin/
│     ├─ jvmMain/kotlin/
│     └─ androidMain/kotlin/
├─ tests/
│  ├─ fixtures/
│  ├─ golden/
│  └─ parity/
└─ tools/
   ├─ sync-date-holidays/
   ├─ import-date-holidays/
   ├─ generate-fixtures/
   └─ validate-data/
```

## Initialer Projekt-Bootstrap

Der Zielordner soll als eigenständiges Projekt funktionieren und nicht nur als Planablage.

Direkt anzulegen:

- `README.md` mit Status, Ziel, Nicht-Zielen und Lizenzhinweis.
- `LICENSE` für eigenen Code unter MIT.
- `NOTICE.md` für Attributionen und Datenquellen.
- `CONTRIBUTING.md` mit minimalem Entwicklungs- und PR-Prozess.
- `.gitignore` für Swift, Kotlin/Gradle, IDE- und OS-Artefakte.
- `.planning/plan.md` als kopierter aktueller Projektplan.
- Leere Scaffold-Ordner für `data/`, `specs/`, `swift/`, `kotlin/`, `tests/` und `tools/`.

Git/GitHub:

- Lokales Git-Repo initialisieren.
- GitHub-Repo `MichaelBMF/OpenHolidaysKit` öffentlich anlegen, falls es noch nicht existiert.
- Remote `origin` auf das GitHub-Repo setzen.
- Ersten Commit mit Scaffold, Plan und Lizenzdateien erstellen.

Verify:

- `git status` ist nach dem Initial-Commit sauber.
- Der Plan im Zielordner entspricht dem aktuellen Side-Topic-Plan.
- README und Lizenzdateien erklären klar, dass Code und Daten getrennt lizenziert werden.

## Sub-Spezifikationen

Ja, das Projekt sollte früh Sub-Spezifikationen bekommen. Sie sollen am Anfang bewusst kurz sein
und die Architekturgrenzen festlegen; Details wachsen dann während der Implementierung.

Geplante Subspecs:

- `specs/license-and-data.md`
  - Code-Lizenz MIT.
  - Daten-Lizenzen getrennt dokumentieren.
  - Umgang mit CC BY-SA Daten aus `date-holidays`.
  - Attribution-/NOTICE-Regeln.
- `specs/date-holidays-sync.md`
  - GitHub-Actions-Workflow.
  - Upstream-Ref/Commit-Tracking.
  - unveränderter YAML-Snapshot.
  - generierte Daten.
  - Pull-Request-Review statt direktem Commit auf `main`.
- `specs/rule-language.md`
  - V1-Regeltypen und Semantik.
  - Was bewusst noch nicht unterstützt wird.
- `specs/data-schema.md`
  - YAML-/IR-/Generated-Data-Strukturen.
  - Validierungsregeln.
- `specs/api-contract.md`
  - Swift- und Kotlin-API müssen semantisch gleich bleiben.
  - Fehler-/Unknown-Data-Verhalten.
- `specs/test-and-parity.md`
  - Golden Fixtures.
  - Swift/Kotlin-Parität.
  - optionaler Vergleich gegen `date-holidays` JS.
- `specs/release-and-packaging.md`
  - Swift Package Index.
  - Maven/Gradle-Veröffentlichung.
  - Versionierung von Code und Daten.
- `specs/compatibility.md`
  - unterstützte Swift-, Apple-, Kotlin-, JVM- und Android-Zielplattformen.
  - Mindestversionen und Support-Matrix.

Für den ersten Commit reichen die Dateien als kurze Skeletons mit Ziel, Entscheidungen und offenen
Fragen. Voll ausformuliert werden zuerst `license-and-data.md`, `date-holidays-sync.md`,
`rule-language.md`, `api-contract.md`, `compatibility.md` und `test-and-parity.md`.

## Lizenz- und Datenstrategie

Aktuelle Prüfung von `commenthol/date-holidays`:

- Code: ISC-Lizenz.
- Daten in `holidays.yaml`: CC BY-SA 3.0 mit Attribution.

Konsequenzen:

- Code kann als Referenz gelesen und neu implementiert werden, aber nicht blind kopiert werden.
- YAML-Daten sind wegen CC BY-SA share-alike sensibler als der Code.
- Falls Daten übernommen oder abgeleitet werden, braucht `OpenHolidaysKit`:
  - klare Attribution in `NOTICE.md` und `data/attributions/`
  - Dokumentation, welche Daten aus welchen Quellen stammen
  - Entscheidung, ob das gesamte Datenpaket ebenfalls CC BY-SA 3.0 oder kompatibel lizenziert wird
  - Trennung zwischen Engine-Code-Lizenz und Daten-Lizenz

Entscheidung für den Start:

- Engine-Code unter MIT.
- Datenpaket separat lizenzieren und versionieren.
- Eigene minimale Fixtures können MIT oder CC0 sein.
- Von `date-holidays` übernommene YAML-Snapshots bleiben unter deren Datenlizenz.
- Aus diesen YAMLs generierte Daten werden ebenfalls als abgeleitete Daten behandelt.
- Für V1 zunächst mit kleinen, selbst gepflegten Daten-Fixes und Golden Fixtures starten.
- Voller `date-holidays`-Datenimport erst nach expliziter Lizenzentscheidung.

Offene Lizenzentscheidung:

- Soll das Datenpaket bewusst CC BY-SA-kompatibel sein?
- Soll es zwei Datenkanäle geben: `core-fixtures` permissiv und `date-holidays-derived` share-alike?
- Soll das Projekt langfristig eigene Quellen pflegen, statt `date-holidays`-Daten abzuleiten?

## date-holidays YAML Sync

Die YAML-Dateien sollen nicht per GitHub-Fork und anschließendem Code-Löschen übernommen werden.
Stattdessen bekommt `OpenHolidaysKit` ein eigenes sauberes Repo und einen reproduzierbaren
Sync-Prozess.

Prinzip:

- `date-holidays` bleibt externe Datenquelle.
- Die YAML-Dateien werden als unveränderter Snapshot übernommen.
- Der Snapshot liegt unter `data/sources/date-holidays/countries/`.
- `data/sources/date-holidays/UPSTREAM.md` dokumentiert:
  - Upstream-Repo
  - Upstream-Commit
  - Sync-Datum
  - verwendeter Import-Tool-Stand
  - Lizenzhinweise
- `data/sources/date-holidays/LICENSE` enthält die Original-Lizenz.
- Normalisierte/generierte Daten liegen getrennt unter `data/generated/`.

GitHub Actions:

- `workflow_dispatch`
  - manueller Sync mit Eingabe `upstream_ref`, z. B. Branch, Tag oder Commit.
- `schedule`
  - optional wöchentlich prüfen, ob upstream neue Daten hat.
- Workflow erstellt immer einen Pull Request, nie direkt `main`.
- PR enthält:
  - aktualisierten YAML-Snapshot
  - aktualisierte `UPSTREAM.md`
  - aktualisierte generierte Daten
  - aktualisierte Golden Fixtures, falls nötig
  - Validierungs-/Parity-Ergebnis

Minimaler Workflow:

```yaml
name: Sync date-holidays data

on:
  workflow_dispatch:
    inputs:
      upstream_ref:
        description: "date-holidays ref, tag, or commit"
        required: false
        default: "master"
  schedule:
    - cron: "0 6 * * 1"

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Checkout date-holidays
        uses: actions/checkout@v4
        with:
          repository: commenthol/date-holidays
          ref: ${{ inputs.upstream_ref || 'master' }}
          path: .tmp/date-holidays

      - name: Copy YAML snapshot
        run: ./tools/sync-date-holidays/sync.sh .tmp/date-holidays

      - name: Generate normalized data
        run: ./tools/sync-date-holidays/generate.sh

      - name: Validate data and fixtures
        run: ./tools/sync-date-holidays/validate.sh

      - name: Create pull request
        uses: peter-evans/create-pull-request@v6
        with:
          branch: chore/sync-date-holidays
          title: "Sync date-holidays data"
          commit-message: "Sync date-holidays data"
```

Wichtig:

- `sync.sh` darf keine manuellen lokalen Änderungen an generierten Daten voraussetzen.
- Generierte Dateien müssen reproduzierbar sein.
- Wenn upstream-Regeln nicht unterstützt werden, muss der Import sichtbar abbrechen oder die
  betroffenen Regeln als unsupported reporten.
- Lizenz-/Attributionsänderungen müssen den PR blockieren, bis sie geprüft sind.

## Ziel-API

Die API soll klein bleiben und in Swift/Kotlin semantisch gleich sein.

Kernmodelle:

- `Holiday`
- `HolidayDate`
- `HolidayName`
- `HolidayType`
- `HolidayCalendar`
- `HolidayProfile`
- `HolidayRegion`
- `HolidayRule`
- `HolidayDataSource`
- `HolidayEngine`

Mindestabfragen:

- Feiertage für Jahr + Profil:
  `holidays(year, profile)`
- Feiertag an Datum:
  `holiday(on, profile)`
- Alle unterstützten Länder/Regionen:
  `countries()`, `regions(country)`
- Datenstatus:
  `available`, `unsupportedRegion`, `unsupportedYear`, `unknownData`

Wichtige Semantik:

- Keine Netzwerkpflicht.
- Keine personenbezogenen Daten.
- Feiertage sind `LocalDate`-Daten ohne Uhrzeit und ohne Zeitzone.
- API-Methoden dürfen keine `DateTime`-Zeitzoneninterpretation benötigen.
- Unbekannte Daten sind ein eigener Status, kein stiller Fehler.
- Typen müssen filterbar sein: `public`, `bank`, `school`, `observance`, `optional`,
  `authorities` oder provider-spezifische Erweiterungen.
- Lokalisierte Namen müssen möglich sein, mindestens `en` und Ursprungssprache.
- Namen brauchen eine definierte Fallback-Strategie:
  - angefragte Locale
  - Ursprungssprache des Landes
  - Englisch
  - stabiler technischer Name, falls keine Übersetzung verfügbar ist
- Swift und Kotlin müssen für dieselbe Eingabe dieselbe Sortierung zurückgeben.

## Rule Language

Die Regel-Engine orientiert sich fachlich an `date-holidays`, wird aber als eigene Spezifikation
formuliert.

V1-Regeltypen:

- fixes gregorianisches Datum
- relatives Datum zu Ostersonntag
- Wochentagsregel, z. B. erster Montag im Monat
- bedingte Region/Subdivision-Regeln
- optionale Typen/Flags
- einfache Observed-/Substitute-Day-Regeln

Spätere Regeltypen:

- nicht-gregorianische Kalender
- astronomische oder staatlich angekündigte Feiertage
- komplexe Regeln mit historischen Gültigkeitsintervallen
- lokale/religiöse Sonderfälle

Wichtig:

- Die Spezifikation muss zuerst in `specs/rule-language.md` stehen.
- Swift und Kotlin implementieren gegen die Spezifikation, nicht gegeneinander.
- Golden Tests sind die eigentliche Kompatibilitätsbremse gegen Drift.
- Unsupported-Regeln werden nicht still ignoriert.
- Import-Tools erzeugen einen maschinenlesbaren Unsupported-Report mit Land, Region, Regel und
  Ursache.

## Datenformat

V1 soll YAML als Input unterstützen, aber intern normalisierte Daten verwenden.

Pipeline:

1. YAML lesen.
2. Schema validieren.
3. In ein neutrales Intermediate Representation Modell transformieren.
4. Swift/Kotlin Engine berechnen daraus Feiertage.
5. Golden Tests vergleichen Output.

Optionen:

- Runtime-YAML-Parsing in beiden Sprachen.
- Build-Time-Import in JSON/Swift/Kotlin Ressourcen.
- Hybrid: YAML als Source of Truth, generierte kompakte Daten für Apps.

Empfehlung für V1:

- YAML bleibt Source of Truth im Repo.
- Import-/Validate-Tool erzeugt JSON-Golden-Fixtures.
- Swift und Kotlin starten mit einfachem Runtime-Parser für ein kleines Länder-Subset.
- Später Generator für optimierte App-Ressourcen.
- Generierte Dateien müssen deterministisch sein und dürfen keine manuellen Änderungen benötigen.

Versionierung:

- Engine-Code und Daten können unabhängig versioniert werden.
- Für V1 wird ein gemeinsames Release bevorzugt, aber mit sichtbarer Datenversion im Runtime-API.
- Langfristig soll ein Datenpaket austauschbar sein, ohne die Engine-API zu brechen.

## Teststrategie

Tests müssen wichtiger sein als API-Breite.

Testebenen:

- Unit Tests für Datum/Rechenregeln.
- Parser Tests für YAML/IR.
- Golden Tests je Land/Jahr/Region.
- Parity Tests Swift vs. Kotlin.
- Reference Tests gegen `date-holidays` JS für definierte Fixture-Sets.

Golden Fixture Format:

```json
{
  "profile": "DE-BY-KATH",
  "year": 2026,
  "holidays": [
    {
      "date": "2026-01-01",
      "name": { "de": "Neujahr", "en": "New Year's Day" },
      "type": "public"
    }
  ]
}
```

Erste Fixture-Sets:

- Deutschland/Bayern katholisch 2026
- Deutschland/Bayern protestantisch 2026
- Deutschland/Bayern Augsburg 2026
- Deutschland/Bayern katholisch 2030
- Ein Land mit observed days, z. B. USA oder UK
- Ein Land mit kantonalen/lokalen Regeln, z. B. Schweiz

## MVP-Scope

Das MVP soll bewusst klein sein:

- Monorepo-Struktur.
- Lizenz-/NOTICE-Grundlage.
- Subspec-Skeletons für Lizenz, Sync, Regeln, Schema, API und Tests.
- Regel-Spezifikation V1.
- YAML-Schema V1.
- Manueller `date-holidays` YAML-Sync per GitHub Actions, der einen PR erstellt.
- Swift Package mit Bayern/Deutschland-Subset.
- Kotlin Multiplatform Modul mit demselben Subset.
- Gemeinsame Golden Fixtures.
- CI, die Swift- und Kotlin-Tests ausführt.
- Kompatibilitäts-Spezifikation mit konkreten Mindestversionen.
- Maschinenlesbarer Unsupported-Report für nicht importierbare Regeln.

Nicht im MVP:

- Vollständiger Import aller `date-holidays`-Länder.
- Nicht-gregorianische Kalender.
- Öffentliche Web-API.
- UI.
- Schulferien.
- Automatische Veröffentlichung auf Maven Central/Swift Package Index.
- Vollständige Governance-Struktur über minimale Contribution-Regeln hinaus.

## Umsetzungsschritte

### OHK.1 Repository-Scaffold

- Neues GitHub-Repo `OpenHolidaysKit` anlegen.
- Basisstruktur mit `swift/`, `kotlin/`, `data/`, `specs/`, `tests/`, `tools/`.
- README mit Ziel, Status und Nicht-Zielen.
- LICENSE/NOTICE initial anlegen.
- `.gitignore` und `CONTRIBUTING.md` anlegen.
- Lokales Git-Repo initialisieren und ersten Commit erstellen.

Verify:

- Repo baut noch nichts, aber Struktur ist klar und dokumentiert.
- Initialer Commit ist sauber und enthält keine App-spezifischen Dateien.

### OHK.2 License Decision

- Upstream-Lizenzen dokumentieren.
- Engine-Code-Lizenz auf MIT festlegen.
- Datenlizenz getrennt festlegen:
  - eigene Fixtures: MIT oder CC0
  - `date-holidays` Snapshot: upstream Datenlizenz
  - generierte Daten aus diesem Snapshot: abgeleitete Daten, nicht MIT re-lizenzieren
- Umgang mit CC BY-SA Daten dokumentieren.
- `NOTICE.md` und `data/attributions/README.md` anlegen.
- `data/LICENSE.md` anlegen.

Verify:

- README nennt klar, welche Teile wie lizenziert sind.
- `LICENSE` deckt nur den eigenen Code ab.
- `data/LICENSE.md` macht die Datenlizenz-Trennung explizit.

### OHK.3 Subspec Skeletons

- Leere, aber strukturierte Subspec-Dateien anlegen:
  - `specs/license-and-data.md`
  - `specs/date-holidays-sync.md`
  - `specs/rule-language.md`
  - `specs/data-schema.md`
  - `specs/api-contract.md`
  - `specs/test-and-parity.md`
  - `specs/release-and-packaging.md`
  - `specs/compatibility.md`
- Jede Datei enthält:
  - Ziel
  - Entscheidungen
  - Nicht-Ziele
  - offene Fragen
  - Verify-Kriterien

Verify:

- Der Hauptplan kann auf die Subspecs verweisen, ohne Implementierungsdetails zu duplizieren.

### OHK.4 Rule Spec V1

- `specs/rule-language.md` schreiben.
- Minimale Regeltypen definieren:
  - fixed date
  - Easter relative
  - weekday-in-month
  - region condition
  - validity interval
  - type/name metadata

Verify:

- Bayern 2026 und 2030 sind vollständig ausdrückbar.
- Unsupported-Regeln haben ein definiertes Fehler-/Reportformat.

### OHK.5 Shared Fixtures

- Golden Fixture Format festlegen.
- Erste DE/BY Fixtures erzeugen.
- Reference-Script vorbereiten, das optional `date-holidays` JS gegen Fixtures laufen lässt.

Verify:

- Fixture-Dateien sind unabhängig von Swift/Kotlin lesbar.

### OHK.6 date-holidays Sync Workflow

- `tools/sync-date-holidays/` anlegen:
  - `sync.sh`
  - `generate.sh`
  - `validate.sh`
- `.github/workflows/sync-date-holidays.yml` anlegen.
- Workflow unterstützt:
  - `workflow_dispatch` mit `upstream_ref`
  - optional `schedule`
  - Checkout von `commenthol/date-holidays`
  - Kopieren von `data/countries`
  - Kopieren der upstream `LICENSE`
  - Schreiben von `UPSTREAM.md`
  - Generieren normalisierter Daten
  - Validieren von Daten und Fixtures
  - Erstellen eines PRs statt direktem Commit auf `main`

Verify:

- Ein manueller Workflow-Lauf erzeugt bei Änderungen einen PR.
- `UPSTREAM.md` enthält den exakten upstream Commit.
- Der Workflow bricht sichtbar ab, wenn unsupported YAML-Regeln nicht sauber gemeldet werden.

### OHK.7 Swift MVP

- `swift/Package.swift`
- `OpenHolidaysKit` Kernmodelle.
- Parser/Loader für V1-IR.
- Engine für fixe und ostersonntagsrelative Regeln.
- Tests gegen Golden Fixtures.

Verify:

- `swift test` grün.
- Bayern katholisch/Augsburg/protestantisch 2026 stimmen mit App-Fixtures überein.

### OHK.8 Kotlin MVP

- Kotlin Multiplatform Projekt.
- Gemeinsame Kernmodelle in `commonMain`.
- Engine für denselben V1-Regelsatz.
- Tests gegen dieselben Golden Fixtures.

Verify:

- `./gradlew test` grün.
- Kotlin-Ausgabe entspricht Swift-Golden-Output.

### OHK.9 Parity CI

- GitHub Actions:
  - Swift tests
  - Kotlin tests
  - Fixture validation
  - optional JS-reference parity
- CI muss auf PRs laufen.

Verify:

- Ein PR mit absichtlich falschem Datum schlägt zuverlässig fehl.
- Ein PR mit nicht unterstützter importierter Regel schlägt fehl oder erzeugt einen expliziten
  Unsupported-Report.

### OHK.10 Import-Tooling

- Kleines Tool unter `tools/import-date-holidays/`.
- Zunächst nur Länder-Subset importieren.
- Import erzeugt normalisierte IR und Attributionsdatei.

Verify:

- Import ist reproduzierbar.
- Manuelle Änderungen an generierten Daten sind vermeidbar oder klar markiert.

## Offene Fragen

- Wollen wir Daten dauerhaft aus `date-holidays` ableiten, oder nur API/Rule-Ideen übernehmen?
- Soll `OpenHolidaysKit` bewusst mit CC BY-SA Daten ausgeliefert werden?
- Welche Länder sind nach Bayern die nächsten Testländer?
- Soll die Rule-Spec möglichst kompatibel zu `date-holidays` bleiben oder sauberer und kleiner
  starten?
- Soll Kotlin primär Android oder Multiplatform/JVM-first werden?
- Soll es später ein CLI geben, um Feiertage aus YAML zu berechnen und Fixtures zu generieren?
- Soll die Datenversion separat von der Engine-Version veröffentlicht werden?
- Welche Mindestversionen gelten für Swift, macOS, iOS, Kotlin, JVM und Android?
- Soll der erste öffentliche Release bereits Maven Central vorbereiten oder nur GitHub Packages?

## Definition of Done für den Plan

- Projektname und Monorepo-Struktur sind entschieden.
- Lizenzstrategie ist vor Datenimport geklärt.
- MVP-Scope ist klein genug für einen ersten öffentlichen Commit.
- Swift und Kotlin teilen Fixtures und Spezifikation.
- Der Plan ist als eigenständiges Projekt verwendbar und enthält keine App-spezifischen
  Integrationsschritte.
