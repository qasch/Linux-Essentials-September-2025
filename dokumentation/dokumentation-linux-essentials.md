# Dokumentation Linux Essentials 

## Unterschied Terminal / Shell

Ein Terminal ist heutzutage ein Programm (früher ein physisches Gerät), das die Ein- und Ausgabe für eine Shell bereitstellt. Das Terminal zeigt an, was die Shell ausgibt und nimmt Tastatureingaben entgegen. Es ist eine Art _Benutzeroberfläche_ durch die wir mit einer Shell interagieren können.

Eine Shell ist ein _Kommando-Interpreter_. Sie nimmt Kommandos entgegen und interpretiert diese.

In Linux dient die Shell unter anderem dazu, als Vermittler zwischen Benutzer und Betriebssytem zu fungieren. Shells werden generell genutzt, um einzelne Befehle (z.B. einer Skriptsprache) zu interpretieren und auszuführen. 

Die Python Shell kann z.B. Python Kommandos ausführen, in einer MySQL Shell können Datenbanken erstellt und verwaltet werden usw.

Unter Linux nutzen wir in der Regel die _BASH_ (_Bourne Again Shell_) als Shell. Auch hier gibt es einige `sh` kompatible Varianten wie die _ZSH_, _KSH_, _Fish-Shell_ etc.

## Kommandos

### Aufbau von Kommandos:
```
<kommando> [-<kurzoption>]... [<argument>]...
<kommando> [--<langoption>]... [<argument>]...
```
Erklärung zur obigen Syntax (angelehnt an Manpages):

- `[  ]` was in eckigen Klammern steht, ist **optional** -> wir können also Optionen oder Argumente übergeben, **müssen** es aber nicht
- `...` die drei Punkte bedeuten, dass auch mehrere Optionen oder Argumente übergeben werden können

>[!NOTE]
> Es macht fast immer keinen Unterschied, ob wir die Option(en) vor oder nach den Argumenten schreiben:
> ```bash
> rm -r somedir
> rm somedir -r
>```

#### Beispiele
```
ls -l               # Übergabe der Option -l
ls /etc             # Übergabe des Arguments /etc
ls -la              # Übergabe mehrerer Optionen
ls -la /etc /home   # Übergabe mehrerer Optionen und Argumente
```
### Grundlegende Kommandos

- `whoami` gibt den aktuellen Benutzer aus
- `pwd` gibt das aktuelle Verzeichnis aus
- `ls` zeigt den Inhalt von Verzeichnissen an
- einige Optionen von `ls`:
  - `ls -a` ignoriert keine Einträge, die mit einem Punkt beginnen -> zeigt auch "versteckte" Dateien an
  - `ls -l` zeigt ausführliche Details zu den Dateien an
- `cat` gibt den Inhalt einer Datei auf der Kommandozeile aus
- `less` ist ein sogenannter *Pager*: gibt den Inhalt einer Datei aus, mit der Möglichkeit zu scrollen, zu suchen etc. (Benutzung siehe Manpages)
- `history` zeigt alle bisher eingegebenen Kommandos inkl. eines Indexes an (s.u.)
- `su` *Substitue User* -> Benutzer wechseln
  - `su -l root` eine Shell mit Root-Rechten öffnen
- `exit` beendet die aktuell laufende Shell 
- `clear` *leert* die Seite, so dass unser *Prompt* sich ganz oben befindet, wir können aber auch die Tastenkombination `STRG+L` verwenden
- `touch` erstellt eine leere Datei
- `mkdir` erstellt ein Verzeichnis
- `echo` gibt alle übergebenen Argumente aus (Äquivalent zu `print()` in `python`

### Shell-Builtins
In die Shell (in unserem Fall BASH) eingebaute Kommandos. Sie sind essenziell bzw. wichtig, damit die Shell an sich funktioniert, z.B. das Kommando `cd`. 

Builtins haben keine eigene Manpage, ihre Funktionsweise ist in der Manpage der BASH erklärt. Eine Kurzhilfe zu den Builtins erhält man mit dem Kommando `help`.

### Extern realisierte Kommandos
Die meisten Kommandos sind _extern realisiert_, d.h. sie sind nicht in die BASH eingebaut. So gut wie alle _extern realisierten_ Kommandos haben eine Manpage (`man <kommando>`) in welcher die Art wie das Kommando zu benutzen ist und sämtliche Optionen mit Erklärungen angegeben sind.

## Hilfe auf der Kommandozeile

### Manpages

*Manual Pages*: eine Art Handbuch zu einzelnen Kommandos, mit Erklärungen zur Syntax, allen Optionen, teilweise Beispielen etc.

- `man <kommando>` 
- z.B. `man ls` Handbuchseite zum Kommando `ls`
- Suche in den Manpages: Eingabe von `/` gefolgt vom Suchbegriff, z.B. `/-l` sucht nach der Option `-l`
- zum nächsten Suchbegriff mit `n`
- zum vorherigen Suchbegriff mit `N`
- Manpage schliessen mit `q`
- zum Anfang der Manpage springen mit `g`
- ans Ende mit `G`

### Help

*Kurzhilfe* zu einem Kommando durch Übergabe der Option `--help` -> `ls --help`

## History

Eine Liste aller bisher eingegebenen Kommandos

- Blättern durch die History mit den Pfeiltasten oder `STRG+P` bzw. `STRG+N`
* gezielt ein bestimmtes Kommando aufrufen:
- nach Eingabe von `history` Aufruf von `!<index>` -> `<index>` ist der Index des Kommandos

## Dateioperationen

### Dateien und Verzeichnisse kopieren - cp

Dateien und Verzeichnisse können mit dem Kommando `cp` (*copy*) kopiert werden.
```bash
cp <quelle> <ziel>
cp <pfad-zur-quelle> <pfad-zum-ziel>
```
**Vorsicht:** Wenn wir eine bestehende Datei als Ziel angeben, wird die Zieldatei **ohne Nachfrage** ersetzt und nicht etwas der Inhalt der Quelldatei an die Zieldatei angefügt.

Beim Kopieren von Verzeichnissen müssen wir an die Option `-r` (*rekursiv*) denken. 
```bash
cp -r <quellverzeichnis> <zielverzeichnis>
```
Der Grund ist, dass ein Verzeichnis nicht leer ist, die Kopieraktion also wiederholt/_rekursiv_ ausgeführt werden muss.

### Dateien und Verzeichnisse löschen - rm

Dateien und Verzeichnisse können mit dem Kommando `rm` (*remove*) gelöscht werden.

Analog zum Kopieren von Verzeichnissen müssen wir auch beim Löschen von Verzeichnissen die Option `-r` angeben.

> [!NOTE] 
> Dies gilt übrigens für sehr viele Kommandos: funktioniert die Anwendung eines Kommandos auf eine Datei, nicht aber auf ein Verzeichnis, so feht oft einfach nur die Option `-r`.

```bash
rm <pfad-zur-datei>
rm -r <pfad-zum-verzeichniss>
```
>[!NOTE]
> Wenn wir eine Datei löschen, so löschen wir nicht die Datei an sich. Wir entfernen lediglich den Dateinamen bzw. Pointer auf die Daten der Datei auf dem Speichermedium. Dieser Bereich im Speicher wird dann als wieder überschreibbar gemeldet.
>
> Die Daten könnten also solange keine weitere Schreiboperation auf diesen Speicherbereich erfolgt ist wiederhergestellt werden.

#### Leere Verzeichnisse löschen

**Leere** Verzeichnisse können zusätzlich mit dem Kommando `rmdir` gelöscht werden.

### Dateien und Verzeichnisse verschieben / umbenennen

Dateien und Verzeichnisse können mit dem Kommando `mv` (*move*) verschoben und umbenannt werden.

Beim Verschieben von Verzeichnissen dürfen wir die Option `-r` *nicht* angeben. Der Grund dafür ist, dass beim Verschieben nicht wie vielleicht angenommen eine Art *ausschneiden* und *einfügen* stattfindet, sondern wie beim Löschen lediglich der Dateiname ersetzt wird. 

Es muss also keine rekursive Operation auf dem Speichermedium stattfinden. Das ist auf unten stehendender Illustration vielleicht besser zu erkennen.
```bash
mv <quelle> <ziel>
mv <quellverzeichnis> <zielverzeichnis>
mv <alter-name> <neuer-name>
```
### Illustration kopieren, löschen, verschieben

![illustration-cp-rm-mv](./images/cp-mv-rm.png)

### relative und absolute Pfadangaben

Immer wenn wir eine Dateioperation durchführen, müssen wir den Pfad (eine Art *Wegbeschreibung*) zu der jeweiligen Datei angeben. Diese Angabe können wir auf zwei unterschiedliche Arten und Weisen machen: *relativ* oder *absolut*.

#### absolute Pfadangaben

Eine *absolute Pfadangabe* beschreibt den Weg ausgehend von der Wurzel `/` (bzw. `\` bzw. z.B. `C:` in Windows) des Dateisystembaums.
```bash
cp /home/tux/somefile /home/tux/Somedir
```
Absolute Pfadangaben können wir immer daran erkennen, dass das erste Zeichen des Pfades ein Slash `/` ist.

Einzige Ausnahme ist die Tilde `~`, welche den absoluten Pfad zum Heimatverzeichnis des aufrufenden Benutzers symbolisiert. Folgende Pfadangaben sind identisch:
```bash
cd ~/Somedir
cd /home/tux/Somedir
```
#### relative Pfadangaben

Eine *relative Pfadangabe* beschreibt den Weg ausgehend vom **aktuellen Standort** (aktuelles Verzeichnis) im Dateisystem.
```bash
cp somefile Somedir/
```
##### spezielle Verzeichniseinträge (Special Directory Entries) . und ..

- Sie gehören zur Kategorie der relativen Pfadangaben (Relative Pathnames)
- Sie werden auch als *Pseudodirektoren* (Pseudo-Directories) bezeichnet
- Manchmal nennt man sie auch *Implizite Links* oder *Selbstreferenzierende Einträge*
- Formal sind sie aber einfach reguläre Einträge im Dateisystem, die bei jedem Verzeichnis automatisch vorhanden sind.

- `.` (Punkt) symbolisiert das aktuelle Verzeichnis
- `..` (doppelter Punkt) symbolisiert das übergeordnete Verzeichnis (Parent Directory)

## Aliase

Aliase sind selbstdefinierte Abkürzungen für Kommandos mit Optionen. Wir verwenden Aliase z.B. für häufig verwendete Kommandos mit Optionen oder auch Argumenten wie Pfadangaben.

Das Kommando `alias` an sich zeigt alle in der aktullen Shell gültigen Aliase an.

### Definition von Aliasen
```bash
alias <name-des-aliases>='<kommando> -<option> <argument>'
alias la='ls -a'
alias rm='rm -i'
alias somedir='cd ~/path/to/specific/dir/'
```
Wenn wir Aliase einfach so auf der Kommandozeile definieren, sind diese nur in der aktullen Shell gültig. Wollen wir Aliase persistent definieren (für alle neu geöffneten Shells bzw. auch nach einem Reboot), so müssen wir die Definition in dafür vorgesehene Dateien eintragen.

Dieses Konzept gilt nicht nur für Aliase, sondern generell für die Konfiguration unseres Systems.

Aliase werden z.B. direkt in der Datei `~/.bashrc` oder besser noch in der Datei `~/.bash_aliases` definiert (wenn wir als Shell die BASH verwenden).

#### Löschen von Aliasen
```
unalias <name-des-aliases>
unalias lsa
```
Definierte Aliase können mit dem Kommando `unalias` wieder gelöscht werden.

Die Opione `-a` löscht alle Aliase (`unalias -a`).

### Pattern Matching

Ein *Pattern* ist ein *Muster*, bzw. ein *Platzhalter* oder *Wildcard* welches auf eine Zeichenfolge passt, so dass wir damit z.B. nach Dateien bzw. Pfadangaben suchen können (mit entsprechenden Kommandos).

Wir können in einem *Pattern* bestimmte Sonderzeichen verwenden, um dieses allgemeingültiger zu machen:

*Globbing Characters:*

- `*` (*Asterisk*) -> Steht für beliebige Zeichen, welche beliebig oft vorkommen können (auch keinmal)
- `?` -> Steht für jedes beliebige Zeichen, welches **exakt** einmal vorkommt

Weitere Möglichkeiten für Pattern Matching:

- `!(pattern)` Exkludiert das angegebene Pattern (in dem Pattern dürfen auch wieder die oben angegebenen *Globbing Characters* vorkommen

Beispiele:
```bash
rm *.jpg       # löscht alle Dateien mit der Endung .jpg
ls datei?.txt  # zeigt nur Dateien an, bei denen nach der Zeichenfolge datei noch ein weiteres beliebiges Zeichen folgt und die die Endung .txt haben
mv !(o*) ../somdir/    # verschiebt alle Dateien des aktuellen Verzeichnisses nach ../somedir, ausser Dateien, die mit einem o beginnen
```
## Escaping / Maskieren von Sonderzeichen
Bestimmte Zeichen haben eine Sonderbedeutung für die BASH. Das wohl wichtigste Sonderzeichen ist das *Leerzeichen*: 

> Das Leerzeichen ist ein Sonderzeichen. Das Leerzeichen ist das **Trennzeichen**. Das Trennzeichen ist elementar wichtig für die Shell, um z.B. ein Kommando von seinen Optionen und Argumenten unterscheiden zu können.

Weitere Sonderzeichen sind:
```bash
*       # Asterisk
?       
#       # Kommentarzeichen
$       # Subsitution
!       # History Expansion
\       # Backslash
'
"
```
Sonderzeichen können durch das sogenannte *Escaping* oder *Maskieren* bzw. *Quoting* ihrer Sonderbedeutung entledigt werden, so dass sie von der Shell wie reguläre Satzzeichen und nicht wie Sonderzeichen behandelt werden.

Zum Maskieren gibt es drei verschiedene Wege:

1. Maskieren mit dem Backslash `\`: Der Backslash maskiert (nur) das **direkt darauffolgende** Zeichen

2. Maskieren mit einfachen Hochkommata `'`: Einfache Hochkommata maskieren **jedes** in ihnen eingeschlossene Zeichen.

3. Maskieren mit doppelten Hochkommata `"`: Doppelte Hochkommata maskieren **fast** alle in ihnen eingeschlossene Zeichen, nicht aber

- `$` (Dollar) - Variablensubstitution funktioniert weiterhin
- `` ` `` (Backticks) - Kommandosubstitution funktioniert weiterhin
- `\` (Backslash) - behält seine Escape-Funktion
- `!` (Ausrufezeichen) - History Expansion in bash (je nach Einstellung)

## Subshells

Innerhalb einer laufenden Shell können weitere Shells gestartet werden. Dies sind sogenannte *Subshells* oder *Kindshells*. Diese können entweder aktiv, z.B. durch die Eingabe des Kommandos `bash` gestartet werden. 

Subshells sind separate Instanzen der Shell, die von der Hauptshell gestartet werden. Sie sind ein fundamentales Konzept in Linux/Unix-Systemen.

Subshells werden aber auch oft gestartet, ohne dass wir dies merken.

Z.B. werden Kommandos, Funktionen, Skripte in Subshells ausgeführt, auch wenn wir davon direkt gar nichts mitbekommen. Auch Pipes und runde Klammern `()` erzeugen Subshells. 

Es ist wichtig zu wissen, dass z.B. Aliase und Variablen **nicht** automatisch in Subshells vererbt werden!

Auch beim Wechsel in einen anderen Benutzeraccount wird eine Subshell mit den Berechtigungen dieses Benutzers gestartet.

Wir können uns einen Überblick über die momentan laufenden Shells bzw. Subshells mit dem Kommando `ps` verschaffen, oder in der BASH über die Variable `BASH_SUBSHELL`
```
echo $BASH_SUBSHELL   # zeigt 0 in Hauptshell, >0 in Subshells
(echo $BASH_SUBSHELL) # zeigt 1
((echo $BASH_SUBSHELL)) # zeigt 2
```
##### Eigenschaften von Subshells
**Vererbung**:

- **Umgebungs**variablen werden vererbt (als **Kopie**)
- Funktionen werden vererbt
- Arbeitsverzeichnis wird vererbt

**Isolation**:

- Änderungen in der Subshell beeinflussen die Parent-Shell **nicht**
- (neue) Shellvariablen werden nicht vererbt/sind nicht sichtbar
- `cd` in einer Subshell ändert nicht das Verzeichnis der Parent-Shell

##### Praktische Beispiele
###### Variablen-Isolation
```
var="parent"
(var="child"; echo "In Subshell: $var")
echo "In Parent-Shell: $var"
# Ausgabe: "child" dann "parent"
```
###### ArbeitsverzeichnisIsolation
```
pwd                   # z.B. /home/tux
(cd /tmp; pwd)        # zeigt /tmp
pwd                   # zeigt wieder /home/tux
```
###### Typisches Problem mit Pipes
```
count=0
echo -e "1\n2\n3" | while read line; do
    ((count++))       # läuft in Subshell!
done
echo "Count: $count"  # zeigt 0, nicht 3!

# Lösung:
count=0
while read line; do
    ((count++))
done < <(echo -e "1\n2\n3")
echo "Count: $count"  # zeigt 3
```
## Variablen

### Umgebungsvariablen / Environment Variables

### Shellvariablen / Shell Variables

Sind systemweit gültig, enthalten wichtige Informationen, damit unser System wie gewünscht funktioniert, bestimmte Kommandos greifen auf diese Variablen zurück. Umgebungsvariablen werden nach Konvention komplett in Grossbuchstaben geschrieben.

Einige Beispiele:
```bash
$HOME       # Heimatverzeichnis des aktuellen Benutzers
$PWD        # absoluter Pfad des aktuellen Verzeichnisses
$USER       # Login Name des aktuellen Benutzers
$SHELL      # Shell des aktuellen Benutzers
$PATH       # Liste der Verzeichnisse, die nach ausführbaren Dateien durchsucht werden, so dass wir diese ohne eine Pfadangabe aufrufen können
```
Systemvariablen können unterschiedliche Werte enthalten, je nachdem welcher Benutzer angemeldet ist. 

### Shellvariablen / Shell Variables

Sind nur gültig in der aktuellen Shell, können vom Benutzer selbst definiert werden. Werden **nicht** automatisch in Subshells vererbt, es sei denn sie werden mit dem Kommando `export` exportiert.
```bash
foo=bar         # weist der Variablen foo den Wert bar zu
export foo      # macht die Variable foo auch in Subshells gültig
export hallo=huhu # weist der Variablen hallo den Wert huhu zu und macht diese in Subshells gültig
```
### Variablensubstitution

Bei der Variablensubstitution wird der Name der Variablen mit dem in ihr hinterlegten Wert ersetzt.

```bash
echo $foo       # gibt den Wert der Variablen foo aus
echo ${foo}     # gibt den Wert der Variablen foo aus
```
### Kommandosubstitution

Durch die *Kommandosubstitution* können wir Variablen die Ausgabe eines Kommandos zuweisen. Genauer gesagt wird eine *Subshell* gestartet, in welcher das Kommando ausgeführt wird.
```bash
aktuelles_datum=$(date)
aktuelles_datum=`date`     # veraltete Syntax
```
### Rechnen mir Variablen / Arithmetic Operations

Wir können auch einfache Rechenoperationen in der BASH durchführen:
```bash
zahl1=3
zahl2=4
summe=$(( zahl1 + zahl2 ))
summe=$((zahl1+zahl2))
let summe = $zahl1 + $zahl2 
```
## Dateien finden

### locate
Durchsucht das Dateisystem nach einem *Pattern* bzw. Suchbegriff.

`locate` ist sehr schnell, denn es durchsucht eine Datenbank (also eine Art Index/Glossar), die Suche ist so deutlich schneller möglich, als wenn jede Datei einzeln angeschaut werden müsste.

Die Datenbank wird vom System über einen sog. `cronjob` automatisch periodisch erneuert.

Manuell können wir die Datenbank mit dem Kommando `updatedb` aktualisieren. Dafür sind `root` Rechte nötig.

`locate` hat einige Optionen, die wichtigste davon ist vielleicht `-i` (*ignore-case*), 

## Distributionen

### Was ist eine Linux-Distribution?
Eine **Linux-Distribution** ist im Prinzip ein komplettes Betriebssystem, das einen Linux-Kernel und zusätzlich Softwarepakete, Paketverwaltung, Systemdienste und oft eine Desktop-Umgebung beinhaltet.

Eine Distribution kombiniert also:

- **Linux-Kernel**: Herzstück des Systems, das die Hardware initiert und steuert und grundlegende Systemfunktionen bereitstellt.
- **GNU-Basiswerkzeuge**: Standardprogramme für Dateiverwaltung, Shell, Systemdienste...
- **Paketverwaltungssystem**: Installieren, Aktualisieren und Entfernen von Software (z. B. `apt`, `dnf`, `pacman`).
- **Systemdienste**: Netzwerk, Benutzerverwaltung, Logging usw.
- **Anwendungssoftware**: Browser, Office, Multimedia usw.
- Optional **Desktop-Umgebung**: z. B. GNOME, KDE, XFCE.

Die verschiedenen Distributionen haben jeweils eigene Paketquellen (*Repositories*) und evtl. auch Tools zur Systemverwaltung.

Sie unterscheiden sich in Zielgruppe, Philosophie, Stabilität, Update-Zyklus, Standardsoftware...

### Beispiele für Distributionen

- **Debian** → stabil, Fokus auf FLOSS (*Free Libre Open Source Software*), oft als Server Betriebssytem eingesetzt
- **Ubuntu** (basiert auf Debian unstable / sid ) →  benutzerfreundlich, Desktop und Server
- **Red Hat Enterprise Linux (RHEL)** →  kommerziell, Unternehmensumgebungen (Server und Desktop), Firmen zahlen für Support
- **Fedora** →  von Red Hat, kostenlos, aktuellste Software, Entwicklerorientiert, eher Desktop
- **Arch Linux** →  folgt dem KISS Prinzip, nach Insatllation absolut minimalistisch, Rolling Release, eher für erfahrenere User, Desktop
- **openSUSE** →  Desktop und Server, YaST als Admin-Tool (grafisches Tool, mit dem sämtliche administrativen Aufgaben erfüllt werden können

## Release-Modelle

- **Fixed Release**:  Stabile Versionen in festen Intervallen. Nur mit einer neuen Version der Distribution kommt auch neue Version von Software. Weniger aktuell, dafür stabiler. (Debian, Ubuntu, RHEL, openSUSE Leap)
- **Rolling Release**: Kontinuierliche Updates, keine festen Versionen, aktuelle Software kommt direkt in die Repos. Sehr aktuell (*Bleeding Edge*), dafür tendentiell weniger stabil. (Arch Linux, openSUSE Tumbleweed)
- **Hybrid**:  Kombination aus stabilen Releases und optionalen Rolling-Komponenten. (Fedora (teils), Manjaro (basiert auf Arch Linux))

Release basierte Distributionen haben oft auch noch zusätzlich verschiedene interne Releases. Beispiel Debian:

- **stable:** die offizielle, stabile Version, Software ist ca. 2 Jahre alt
- **testing:** enthält Pakete, die in *unstable* waren aber noch nicht in *stable* akzeptiert wurden, wird zur nächsten *stable* Version, Software ist bis zu 1 Jahr alt
- **unstable:** neueste Software, theoretisch instabil, Basis für Ubuntu

## Supportzeitraum und LTS (Long Term Support)

Die einzelnen Versionen der Release basierten Distributionen werden über einen bestimmten Zeitraum hinweg mit Updates versorgt, bis sie ihren EOL (End of Life) erreichen und keine Updates mehr bekommen.

**LTS** steht für Long Term Support (Langzeit-Unterstützung). LTS-Versionen bekommen besonders lange Updates (mindestens 5 Jahre) und sind besonders für Unternehmen, Server und Systeme wichtig, die über Jahre stabil laufen sollen, ohne dass man sich um häufige Upgrades (des gesamten Systems) kümmern muss.

Es gibt sogar Versionen von Ubuntu und RHEL, die über mehr als 10 Jahre lang (Sicherheits-)Updates erhalten (*ELS - Extended Lifecycle Support* bzw. *ESM - Extended Security Maintenance*), dann aber auch (teilweise) kostenpflichtig sind.








