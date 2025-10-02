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

### Verzeichnisse erstellen - mkdir
Mit dem Kommando `mkdir` (*make directory*) können wir Verzeichnisse erstellen.
```bash
mkdir <name-des-verzeichnisses>
mkdir <pfad-zum-verzeichniss>
```
### Dateien erstellen - touch

Dateien können auf vielfältige Art und Weise erstellt werden. Ein einfacher Weg, leere Dateien zu erstellen, ist mit dem Kommando `touch`.
```bash
touch <name-der-datei>
touch <name-der-datei-1> <name-der-datei-2> ...
touch <pfad-zur-datei>
```
Dateien können aber auch z.B. mit einem Editor wie `nano` erstellt werden.
```bash
nano <name-der>
```
### Editor nano

`nano` ist ein einfacher Editor, der auf den meisten Linux Distributionen vorinstalliert ist. Als Hilfe zur Bedienung wird unten ein Menü mit Tastenkürzeln angezeigt. Hier bedeutet das Zeichen `^` die Taste `STRG`.

Einige wichtige Tastenkombinationen:

- `STRG+O` Datei speichern unter...  (Name kann/muss angegeben werden)
- `STRG+S` Datei speichern (unter dem gleichen Namen)
- `STRG+X` Editor verlassen (bei ungespeicherten Änderungen werden wir gefragt, ob wir diese speichern möchten)

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

## Dateisystembaum / Verzeichnisstruktur

| Verzeichnis | Bedeutung | enthält |
| ----------- |:-------------: | --------- |
| `/bin` | *binary* |  ausführbare Dateien, die von allen Benutzern ausgeführt werden können. Normalerweise ein *Symlink* auf `/usr/bin`. |
| `/sbin` | *superuser binary* |  auch ausführbare Dateien, die allerdings nur von `root` genutzt werden können. Auch ein Symlink auf `/usr/sbin`. |
| `/boot` | |  den/die Linux Kernel (`vmlinuz-6.1.0-25.amd64`), die zugehörige Initiale RAM Disk (`initrd.img-6.1.0-25-amd64`), weitere für den Bootvorgang wichtige Dateien und die Konfiguration des Bootloaders, z.B. `grub`. |
| `/dev` | *devices* |  *Gerätedateien*, z.B. für die vorhanden Speichermedien und Partitionen, `/dev/null`, `/dev/random`, die Filedescriptoren `stdin`, `stdout`, `stderr`, Terminals etc. Dieses Verzeichnis wird automatisch vom Dienst `udev` (*Userspace Dev*) überwacht und gepflegt. |
| `/etc` | *et cetera* / *etsy* |  systemweite Konfigurationsdateien. Diese können für gewisse Programme durch die benutzerspezifischen Konfigurationsdateien (im Heimatverzeichnis der Benutzer) überschrieben werden (`/etc/bash.bashrc` -> `~/.bashrc`). |
| `/home` | | Heimatverzeichnisse der regulären Benutzer |
| `/media` `/mnt` | *mount* |  Verzeichnisse für die *Mountpoints* weiterer/externer Datenträger |
| `/opt` | *optional* | hier können Pakete ihre Dateien ablegen, die nicht über die Standardpaketquellen installiert wurden |
| `/proc` | *processes* |  Dateien/Informationen über das laufende System: laufende Prozesse, Hardware, Kernelkonfiguration. Existiert nur im RAM, ist ein sog. *virtuelles* oder *Pseudodateisystem* |
| `/root` | | Heimatverzeichnis des *Superusers* `root` |
| `/sys` | *system* | ähnlich wie `/proc` bzw. eine nachträgliche Erweiterung,  vor allem Dateien/Informationen zur Hardware, auch ein *virtuelles-* bzw. *Pseudodateisystem*. |
| `/tmp` | *temp* |  temporäre Dateien |
| `/usr` | *Unix System Resources* |  Verzeichnisse für die ausführbaren Dateien, Libraries, Source Code, Dokumentationen etc. |
| `/var` | *variable* |  viele wichtige Dateien wie z.B. *Logdateien* (`/var/log`), E-Mails (`/var/mail`), Cache (`/var/cache`) ... |

# Textströme und Standardkanäle

Es gibt drei Standardkanäle unter Linux:

| Kanalbezeichnung | Filedescriptor | Nummer |
| ---------------- | -------------- | ------ |
| *Standareingabekanal*  | `stdin` | 0 |
| *Standardausgabekanal*|  `stdout` | 1 |
| *Standardfehlerkanal*  | `stderr` | 2 |

Jeder Prozess der gestartet wird, wird mit diesen drei Standardkanälen verbunden. Über diese Kanäle erhält der Prozess Daten und gibt sie auch wieder aus. So können Ein- und Ausgaben unabhängig voneinander verarbeitet und auch umgeleitet werden.

Die Kanäle jedes Prozesses, der in einer Shell gestartet wird, sind automatisch mit der Shell verbunden.

Durch dieses Konzept können wir durch die Kombination simpler Kommandos komplexe Aufaben lösen (-> *Kommandopipelines*) 

Wir könne so z.B. auch Ausgaben von Kommandos in Dateien umleiten (-> *Redirects*).

### Redirects

Mit Redirects kann die der Standardausgabekanal oder der Standardfehlerkanal in eine **Datei** umgeleitet werden. Es gibt zwei Arten von Redirects:

- `>` - einfacher Redirect: Erstellt eine Datei falls nicht vorhanden, **leert** eine bereits vorhandene Datei
- `>>` - doppelter Redirect: Erstellt eine Datei falls nicht vorhanden, **hängt Ausgabe an**

#### Umleitung des Standareingabekanals
```bash
echo huhu 1> hallo.txt   # die 1 gibt hier die Kanalnummer an
echo huhu 1>> hallo.txt  # die 1 gibt hier die Kanalnummer an
echo huhu > hallo.txt    # kann bei stdout auch weggelassen werden
```
```bash
ls -l /etc > ls-ausgabe.txt
ls -l /etc >> ls-ausgabe.txt
```
#### Umleitung des Standardfehlerkanals
```bash
ls mich-gibts-nicht  2> ls-fehler.txt     # hier muss die 2 stehen, da wir stderr umleiten
ls mich-gibts-nicht  2>> ls-fehler.txt    # hier muss die 2 stehen, da wir stderr umleiten
```
#### Umleitung beider Kanäle
##### in separate Dateien
```bash
ls mich-gibts/ mich-gibts-nicht/ > ergebnis.txt 2>fehler.txt
```
##### in die gleiche Datei
```bash
ls mich-gibts/ mich-gibts-nicht/ > ausgabe-und-fehler.txt 2>&1
```
>[!NOTE]
> Das `&` gibt hier an, dass wir einen *Kanal*/*Filedescriptor* meinen, ansonsten würden die Fehler in eine Datei mit dem Namen `1` umgeleitet werden.

```bash
ls mich-gibts/ mich-gibts-nicht/ &> ausgabe-und-fehler.txt
```
>[!NOTE]
> Verkürzte Schreibweise

### /dev/null

`/dev/null` ist soetwas wie das *Schwarze Loch* eines Linux Systems. Alles was wir dorthin leiten, verschwindet. Wir nutzen einen Redirect nach `/dev/null` ganz bewusst, um z.B. Fehlermeldungen eines Kommandos zu unterdrücken. Oder auch in Skripten, um den normalen Output eines Kommandos zu unterdrücken.

#### Beispiel find und 2>/dev/null
Wir wollen als regulärer Benutzer mit `find` unser gesamtes Dateisystem nach `.pdf` Dateien durchsuchen. Mit folgendem Kommando erhalten wir aber sehr viele `Permission Denied` Fehlermeldungen:
```bash
find / -name "*.pdf"
```
Wir leiten also ganz bewusst alle Fehler bzw. `stderr` nach `/dev/null` um die Ergebnisse (auf `stdout`) klarer sehen zu können:
```bash
find / -name "*.pdf" 2>/dev/null
```
## KISS Prinzip

- "Keep it stupid simple"
- "Keep it super simple"
- "Keep it simple, stupid!"

## UNIX Philosophie
Die Unix-Philosophie ist ein Satz von Prinzipien für Software-Design, die ursprünglich in den 1970er Jahren mit dem Unix-Betriebssystem entwickelt wurden. Sie betont Einfachheit, Modularität und Wiederverwendbarkeit.

Douglas McIlroy, der Erfinder der Unixpipes, fasste die Philosophie folgendermaßen zusammen:

- Schreibe Computerprogramme so, dass sie nur eine Aufgabe erledigen und diese gut machen.
- Schreibe Programme so, dass sie zusammenarbeiten.
- Schreibe Programme so, dass sie Textströme verarbeiten, denn das ist eine universelle Schnittstelle.

> "Write programs that do one thing and do it well."

## Kommandopipelines
Kommandopipelines sind ein mächtiges Werkzeug, mit dem sich erst die ganze Stärke der Kommandozeile nutzen lässt.

Syntax:
```bash
<kommando1> | <kommando2>
```
Mit der *Pipe* (`|`) wird `stdout` von `<kommando1>` mit `stdin` von `<kommando2>` verbunden, so dass `<kommando2>` die Ausgabe von `<kommando1>` entgegenehmen und weiterverarbeiten kann.

Wir können durchaus mehrere Kommandos mit Pipes verbinden, sog. *Pipelines*. Die Anzahl ist einzig durch Hardware-Resourcen beschränkt.

```bash
<kommando1> | <kommando2> | <kommando3> | <kommando4> | <kommando5> ...
```
### Beispiele:
**Konzept der UNIX Philosophie und Nutzung der Pipe**

`ls` kann super gut den Inhalt von Verzeichnissen anzeigen, bei grösseren Verzeichnissen müssen wir aber (falls überhaupt möglich) die Maus nutzen, um den Anfang der Ausgabe sehen zu können. 

Wir leiten die Ausgabe also an den *Pager* `less` weiter, der super gut darin ist, Textströme seitenweise anzuzeigen, darin zu scrollen, zu suchen usw.
```bash
ls -l /etc/ | less       # der Output von ls -l wird an den Pager less geleitet
```
**Nur die Usernamen der realen Benutzer anzeigen lassen**

Wir filtern die Datei `/etc/passwd` zuerst nach den Zeilen mit den Usern, die eine Shell (`/bin/bash`, `/bin/sh`, `/bin/zsh` o.ä.) zugewiesen haben. Anschliessend nutzen wir `cut`, um uns nur das erste Feld mit den Usernamen ausgeben zu lassen.

Das Dollarzeichen `$` ist eil eines *regulären Ausdrucks* und steht für das Ende einer Zeile (mehr dazu z.B. in der Manpage von `grep` oder unter `man regex`).
```bash
grep "sh$" /etc/passwd | cut -d: -f1
```
**Anzahl der realen User ausgeben lassen**
```bash
grep "sh$" /etc/passwd | cut -d: -f1 | wc -l
```
> [!NOTE]
> Pipelines bauen wir am besten Stück für Stück auf, wie in einem Baukastensystem. Wir untersuchen die Ausgabe eines Kommandos, nutzen die History um das Kommando erneut aufzurufen, hängen eine Pipe dran, lassen uns das Ergebnis anzeigen, nutzen die History usw.

### `grep`

Mit `grep` können wir Textströme zeilenweise filtern.

`grep` nimmt ein `PATTERN`, also einen Suchbegriff bzw. genauer gesagt einen *Regulären Ausdruck* entgegen und gibt nur die Zeilen eines Textstroms aus, in denen dieses `PATTERN` vorkommt.

`grep` steht für *Global Regular Expression Print*

#### Beispiele:
##### nur die Benutzerkonfiguration von root ausgeben
```bash
grep "root" /etc/passwd     
```
##### -i --ignore-case 
`grep` ignoriert Gross-und Kleinschreibung

hier: sowohl alias als auch Alias wird gefunden
```bash
grep -i alias ~/.bashrc
```
##### -v --invert 
`grep` gibt all das aus, was *nicht* auf das PATTERN passt.

hier: Ausgabe aller Benutzerkonfigurationen, die *nicht* die BASH nutzen
```bash
grep -v bash /etc/passwd
```
##### -c --count 
`grep` zählt die Ergebnisse, hier also die Anzahl der Benutzer, die BASH als Login-Shell nutzen, es wird nur die Anzahl ausgegeben, nicht die Zeilen, die PATTERN enthalten
```bash
grep -c bash /etc/passwd    
```
##### -r --recursive 
`grep` kann so auch ganze Verzeichnisse durchsuchen

hier: gesamtes Home-Verzeichnis von tux nach etwas zu aliasen durchsuchen
```bash
grep -r alias /home/tux 
```
### `cut`

Mit `cut` können wir Textströme **spaltenweise** filtern. 

Für `cut` können wir ein Trennzeichen / *Delimiter* definieren, anhand dessen `cut` einen Textstrom in Spalten / *Fields* unterteilt und nur das oder die gewünschten Felder ausgibt.

#### Beispiele
```bash
cut -d: -f1 /etc/passwd     # nur die Login-Namen der Benutzer ausgeben
cut -d: -f7 /etc/passwd     # nur die Shells der Benutzer ausgeben
cut -d: -f1,7 /etc/passwd   # nur die Shells der Benutzer und deren Shells  ausgeben

cat /etc/passwd | cut -d: -f1 # geht auch, sog. Useless Use of Cat
```
### tail

`tail` gibt standardmässig die letzten 10 Zeilen einer Datei aus. 

Die Anzahl der Zeilen kann über die Option `-n` angegeben werden.

Eine sehr nützliche Option von `tail` ist die Option `-f` / `--follow`. Damit können wir Änderungen an einer Datei sozusagen *live* beobachten. Wird oft in Verbindung mit Log-Dateien genutzt, um zu verfolgen, was gerade passiert. 

#### Beispiele
```bash
tail -n 5 ~/.bashrc     # die letzten 5 Zeilen der bashrc ausgeben
tail -f /var/log/apache2/access.log   # Zugriffe auf den Webserver verfolgen
```
### head

`head` gibt standardmässig die ersten 10 Zeilen einer Datei aus. 

Die Anzahl der Zeilen kann über die Option `-n` angegeben werden.

#### Beispiele
```bash
head -n 5 ~/.bashrc     # die ersten 5 Zeilen der bashrc ausgeben
```
### sort

Mit `sort` können wir Textströme (nach bestimmten Kriterien) sortiert ausgeben.

### uniq

Mit `uniq` könne wir direkt aufeinanderfolgende gleiche Zeilen zu einer einzigen zusammenfassen.

Um z.B. alle Dublikate/gleiche Zeilen aus einem Textstrom zu entfernen, kombinieren wir (KISS Prinzip) `uniq` und `sort`

#### Beispiele
Anzahl der verschiedenen Shells in /etc/passwd zählen
```bash
cut -d: -f7 /etc/passwd | sort | uniq | wc -l 
```
>[!NOTE] 
> `sort` hat übrigens die Option `-u` eingebaut, mit der wir gleiches erreichen können.

```bash
cut -d: -f7 /etc/passwd | sort -u | wc -l 
```
## Prozesse

Ein Prozess ist ein sich in der Auführung befindliches Programm. Ein Programm resultiert immer in mindestens einem Prozess. Prozesse laufen jeweils in einem von anderen unabhängigen "Resourcenraum", haben eine eigene PID, kennen nur die PID des Prozesses, von dem sie gestartet wurden (Elternprozess). Prozesse sind also hierarchisch organisiert. Prozesse können mit dem Kommando `kill` über Signale beeinflusst werden.

Wird der Elternprozess beendet, so werden gleichzeitig alle Kindprozesse mit beendet. Es sei denn, wir treffen bestimmte treffen bestimmte Massnahmen, dass dies nicht passiert (`nohup`, `screen`, `tmux`).

### Vorder- und Hintergrundprozesse

Auf der Shell kann immer nur ein einzelner Prozess im Vordergrund ausgeführt werden, die Shell wird für den Zeitraum der Ausführung *blockiert*, kann also keine anderen Kommandos verarbeiten. Prozesse können mit der Tastenkombination `STRG+Z` angehalten und in den Hintergrund geschickt werden. Mit dem Kommando `bg` kann dieser Prozess dann im Hintergrund fortgesetzt werden, `fg` holt den Prozess in den Vordergrund zurück.

Wir können einen Prozess beim Start aber auch direkt in den Hintergrund schicken und starten (durch Anhängen eines `&`):
```bash
 kommando &
 sleep 200 &
```
### Laufende Prozesse anzeigen lassen
- `ps` : Anzeige aller in der aktuellen Shell laufenden Prozesse
 - `ps -aux`: Anzeige aller laufende Prozessez auf dem System
 - `ps -ef`: auch Anzeige aller laufenden Prozesse auf dem System
 - `ps --forest`: Prozesshirarchie (Baumstruktur) anzeigen
 - `jobs`: Anzeigen der Hintergrundprozesse
 - `fg`: letzten/aktuellen/default Job in den Vordergrund holen
 - `fg %<jobnummer>`: Job mit Jobnummer `<jobnummer>` in den Vordergrund holen
 - `bg`: Hintergrundprozess fortsetzen
 - `bg %<jobnummer>`: Hintergrundprozess mit Jobnummer `<jobnummer>` in fortsetzen

### kill

 `kill` sendet Signale an Prozesse. Es muss die PID des Prozesses angegeben werden, Prozessname funktioniert nicht.

 - `kill -s <signal> <PID>`: sendet <signal> an den Prozess mit der PID <PID>
 - `kill -<signal> <PID>`: sendet <signal> an Prozess mit der PID <PID>

 Die PID eines Prozesses kann auf mehrere Arten ermittelt werden:
```bash
ps -ef | grep <prozessname>
pgrep <prozessname>
```
### einige wichtige Signale

- `SIGTERM` (15): Standard, falls kein bestimmtes Signal angegeben wird. Sendet eine "freundliche" Aufforderung an den Prozess, sich doch bitte zu beenden. Im Prozess selbst ist festgelegt, wie er sich beendet, z.B. werden noch gewisse Aufräumarbeiten durchgeführt etc.
- `SIGINT` (2): sendet eine etwas deutlichere Aufforderung an den Prozess, sich zu beenden, wird bei der Tastenkomnination `STRG+C` (_Cancel_) gesendet
- `SIGKILL` (9): rabiateste Methode, Signal wird nicht an den Prozess, sondern direkt an den Scheduler gesendet, der daraufhin den entsprechenden Prozess aus seiner Liste löscht, der Prozess somit keine CPU Zeit mehr zur Verfügung gestellt bekommt und s## Archivierung und Komprimierungomit zwangsläufig beendet wird.
- `SIGSTOP` (19): hält Prozess an und schickt ihn in den Hintergrund (`STRG+Z`)
- `SIGCONT` (18): startet angehaltene Prozesse

### pkill und killall

- `pkill`: analog zu oben, `pkill` erwartet aber den Namen bzw. einen Teil des Namens eines Prozesses anstatt der PID. Falls mehrere Prozesse auf den Namen passen, wird das Signal an **alle** diese Prozesse

## Archivierung und Komprimierung

### Archivierung mit `tar`

*Archivierung* bezeichnet das Zusammenfassen **mehrerer** Dateien und Verzeichnisse in eine **einzige** Datei, ohne zwingende Kompression. Dadurch bleibt die ursprüngliche Struktur der Dateien erhalten, so können mehrere Dateien einfacher gespeichert oder übertragen werden.

Unter Linux wird das Kommando `tar` (*Tape Archiver*) zur Archivierung verwendet. `tar` ist ein sehr altes Programm und die Syntax (freundlich ausgedrückt) etwas gewöhnungsbedürftig. Kurzoptionen haben oft keine direkte Entsprechung zu den Langoptionen.

Ein `tar`-Archiv kann man sich mit dem Kommando `cat` anzeigen lassen:

![Ausgabe tar Archiv mit cat](./images/ausgabe-tar-archiv-mit-cat.png)

> [!NOTE]
> Alle numerischen Angaben hier sind im *Oktalformat*. Dies hat historische Gründe. Möchte man den Zeitstempel umrechnen, kann man sich von der BASH helfen lassen:
> ```bash
> echo $(( 8#14757403716 ))
> ```

Einige wichtige Optioenen zu `tar`:

>[!NOTE]
> Bei `tar` ist die Option `-f` sehr wichtig. Damit müssen wir immer den Namen des Archivs angeben, mit dem wir arbeiten wollen. Die Option `-f` erwartet zwingend ein Argument (den Namen/Pfad zu einem Archiv. Der Name muss **direkt** hinter der Option folgen.

**Beispiele:**
```bash
tar -cvf archive.tar file1 file2    # korrekt, funktioniert
tar -tf archive.tar                 # korrekt, funktioniert

tar -cfv archive.tar file1 file2    # funktioniert NICHT
tar -ft archive.tar                 # funktioniert NICHT
```

#### Archiv aus Dateien erstellen
```bash
tar -cf archive.tar file1.txt file2.txt file3.txt 
tar --create --file archive.tar file1.txt file2.txt file3.txt 
```
#### Archiv aus einem Verzeichnis erstellen
```bash
tar -cf archive.tar /absolute/path/to/dir
tar -cf archive.tar relativ/path/to/dir
```
#### Dateien aus Archiv extrahieren
```bash
tar -xf archive.tar
tar --extract --file archive.tar
```
#### Die Option -v / --verbose gibt eine Rückmeldung darüber, was tar macht
```bash
tar -xvf archive.tar
tar --extract --verbose --file archive.tar
```
#### Inhalt eines Archivs anzeigen/auflisten
```bash
tar -tf archiv.tar
tar --list --file archive.tar
```
#### Datei einem bestehenden Archiv hinzufügen
```bash
tar -rf archive.tar other_file.txt
tar --append --file archive.tar other_file.txt
```
> [!NOTE] 
> Pfadangaben werden immer mit archiviert! Wir müssen uns also im Vorhinein Gedanken machen, ob wir z.B. einen relativen oder absoluten Pfad angeben.

### Komprimierung

Durch die Komprimierung können wir **eine einzelne** Datei mit Hilfe bestimmter Algorithmen (verlustfrei) in ihrer Grösse verkleinern.

*Analogie Komprimierung:* getrocknete Handtücher, die im Wasser wieder gross werden

*Analogie Archivierung:* einzelne Blumen werden zu einem Strauss gebunden

Um **mehrere** Dateien oder ganze Verzeichnisse zu komprimieren, müssen wir zusätzlich im Vorfeld die *Archivierung* anwenden. Bestimmte Programme in Windows-Systemen vereinen diese beiden Konzepte unter einer Haube. Wir müssen uns jedoch merken, dass dies grundsätzlich zwei komplett verschiedene Konzepte sind.

Auch unter Linux ist es möglich beide Schritte auf einmal mit dem Kommando `tar` durchzuführen, dabei ruft `tar` im Hintergrund jedoch die jeweiligen Kommandos zur Komprimierung auf.

Unter Linux nutzen wir standardmässig drei verschiedene Tools zur Komprimierung: `gzip`, `bzip2` und `xz`.

>[!NOTE]
> Sowohl bei der Komprimierung als auch bei der Dekomprimierung wird die jeweilige Originaldatei nicht behalten, sondern ersetzt.
> Dies können wir mit der Option `-k` (`--keep`) umgehen.

### Vergleich der drei Komprimierungsalgorithmen

Vergleich der Geschwindigkeiten und resultierenden Grössen beim Komprimieren:

![vergleich-komprimierung](./images/vergleich-komprimierung.png)
Vergleich der Geschwindigkeiten beim Dekomprimieren:

![vergleich-dekomprimierung](./images/vergleich-dekomprimierung.png)
Zusammenfassend lassen sich folgende Aussagen über die drei Komprimierungsalgorithmen treffen:

- `gzip` ist am schnellsten bei der Komprimierung, die komprimierte Datei ist aber nicht besonders klein
- `bzip2` braucht lange für die Komprimierung und die Dekomprimierung, erzeugt aber eine ziemlich kleine Datei
- `xz` braucht ziemlich lange bei der Komprimierung, erzeugt liegt bei der Kompressionsrate zwischen den beiden anderen, ist aber sehr schnell bei der Dekomprimierung

Es gibt also für alle drei bestimmte Anwendungsfälle, in denen sie ihre Stärken ausspielen können.

>[!NOTE] Unser Beispiel begünstigt ältere Komprimierungsalgorithmen. In einem echten Beispiel würde `xz` neben der schnellsten Dekomprimierung auch die höchste Kompressionsrate erzielen.

### Erstellen und Entpacken eines komprimierten Archivs direkt mit `tar`

#### gzip komprimiertes Archiv erstellen
```bash
tar -czf archiv.tar.gz somdir/
tar -czvf archiv.tar.gz somdir/     # verboser Output
```
#### bzip2 komprimiertes Archiv erstellen
```bash
tar -cjf archiv.tar.bz2 somdir/
tar -czjf archiv.tar.bz2 somdir/     # verboser Output
```
#### xz komprimiertes Archiv erstellen
```bash
tar -cJf archiv.tar.xz somdir/
tar -cJvf archiv.tar.xz somdir/     # verboser Output
```
#### Komprimiertes Archiv entpacken
##### mit gzip komprimiertes Archiv entpacken
```bash
tar -xzf archiv.tar.gz
tar -xzvf archiv.tar.gz
```
##### mit bzip2 komprimiertes Archiv entpacken
```bash
tar -xjf archiv.tar.bz2
tar -xzjf archiv.tar.bz2
```
##### mit xz komprimiertes Archiv entpacken
```bash
tar -xJf archiv.tar.xz
tar -xJvf archiv.tar.xz
```
##### automatisch jeweiligen Algorithmus ermitteln, Archiv dekomprimieren und Dateien extrahieren
```bash
tar -xf archiv.tar.gz
tar -xf archiv.tar.bz2
tar -xf archiv.tar.xz
```
#### Erklärung der Optionen:

- `c` = create  erstellt ein neues Archiv
- `x` = extract  entpackt ein Archiv
- `f` = file  gibt den Dateinamen des Archivs an (immer direkt danach)
 
- `z` = gzip  wendet gzip-Kompression an
- `j` = bzip2  wendet bzip2-Kompression an
- `J` = xz  wendet xz-Kompression an

## Benutzerkonten

### Root Acount

Der Benutzer `root` ist der *SuperUser* eines Linux Systems. Er ist der einzige Benutzer, welcher volle Rechte auf das System hat, also alles darf. Er muss auf jedem System existieren, damit dieses lauffähig ist, beispielsweise um während des Bootvorgangs einzelne Dienste zu starten usw.

### Reguläre Benutzer

Alle *regulären* Benutzer haben **eingeschränkte** Rechte. Sie dürfen z.B. nicht alle Kommandos ausführen oder generell irgendwelche Änderungen am System vornehmen. 

Im Hintergrund wird das mehr oder weniger alles über die Berechtigungen an Dateien geregelt.

Reguläre Benutzer können sich am System anmelden und interaktiv Kommandos ausführen. Dazu haben sie in der `/etc/passwd` eine *Login Shell* zugewiesen.

### Systembenutzer / Servicenutzer / Pseudobenutzer

Es gibt eine weitere Bentuzergruppe mit eingeschränkten Rechten. Das fällt uns auf, wenn wir die Datei `/etc/passwd` inspizieren. Die Mehrzahl der Benutzer haben wir gar nicht selbst angelegt, sie wurden automatisch vom System erzeugt, als bestimmte Dienste/Services installiert wurden.

Genau das ist der Sinn dieser Benutzer: So können bestimmte Dienste bzw. Prozesse mit deren Berechtigungen ausgeführt werden um die Sicherheit des Systems zu erhöhen. Ein kompromittierter Dienst erhält so also nicht direkt Zugriff auf das gesamte System.

Beispiel: `www-data` für Webserver wie *Apache oder Nginx* - selbst wenn ein Angreifer den Webserver übernimmt, kann er nicht auf andere Systemdateien zugreifen.

Pseudobenutzer haben keine Login-Shell, ihnen wird `/usr/sbin/nologin` zugewiesen. Sie können sich also nicht am System anmelden und Kommandos ausführen.

## Benutzer und Gruppen

### Benutzer anlegen mit `useradd`

Mit `useradd` (auf allen Linux Systemen verfügbar) können wir Benutzer anlegen.

Obwohl ein Eintrag für ein Home-Verzeichnis in der `/etc/passwd` erzeugt wird, wird dies **nicht** angelegt
```bash
useradd <user>
```
Die Option `-m` bewirkt, dass unterhalb von `/home` ein Verzeichnis mit dem Namen des Benutzers erzeugt und alle Dateien aus `/etc/skel` dorthin kopiert werden.
```bash
useradd -m <user>
useradd --create-home <user>
```
Benutzer eine Login-Shell zuweisen
```bash
useradd -s /bin/bash <user>
useradd --shell /bin/bash <user>
```
Kommentarfeld für den vollen Namen des Benutzers und weitere Informationen
```bash
useradd -c "Voller Name des Benutzers" <user>
useradd --comment "Voller Name des Benutzers" <user>
```
Neuen User eine bestimmte Primäre Gruppe zuordnen:
```bash
useradd -g <primary-group> <user>
```
Neuen User einer Liste von zusätzlichen Gruppen zuordnen:
```bash
useradd -G <supplementary-group-1>,<supplementary-group-2> <user>
```
Standarbeispiel zum Anlegen eines Benutzers:
```bash
useradd -m -c "Tux Tuxedo" -s /bin/bash tux
```
### Benutzerkonfiguration ändern

Mit dem Kommando `usermod` können wir die Benutzerkonfiguration nachträglich wieder ändern. Die Optionen sind denen von `useradd` sehr ähnlich. 

Ändern der Login Shell von `korni` zur `ksh`:

```bash
usermod -s /usr/bin/ksh korni
```
### Passwörter
Passwörter werden nicht in der `/etc/passwd` gespeichert, sondern in der Datei `/etc/shadow`. Dafür gibt es mindestens zwei Gründe:

1. Die Datei `/etc/passwd` muss von allen Usern auf dem System lesbar sein, wir wollen aber vermeiden, dass die Passwort-Hashes auslesbar sind
2. In der Datei `/etc/passwd` werden Informationen über die User gespeichert, in der `/etc/shadow` Informationen über Passwörter (*Separation of Concern*)

Passwörter liegen sind immer gehasht und zusätzlich gesaltet, d.h. dass vor dem Hashen des Passworts eine bestimmte zufällig generierte Zeichenkette vor das Passwort geschrieben und dann der kommplette String (Salt + Passwort) gehasht wird.

So wird zum einen vermieden, dass zwei gleiche Klartextpasswörter den gleichen Hash erhalten, zum anderen werden Attacken über *Rainbow Tables* (riesige Tabellen mit Hash-Werten und den dazugehörigen Klartextpasswörtern) vermieden.

Das Kommando `useradd` kann selbst keine Passwörter generieren! Wir rufen dazu nach dem Erstellen eines neuen Users das Kommando `passwd` auf.

>[!NOTE] Wir können dem Benutzer auch bereits beim Erzeugen ein Passwort mitgeben. 

**Wichtig:** Hier muss ein für das System passender *gesaltener* HASH angegeben werden. Der Eintrag wird exakt so in die `/etc/shadow` eingetragen.
```bash
useradd -p "PASSWORDHASH" <user>
useradd --password "PASSWORDHASH" <user>
```
Schwer ist das nicht wirklich - wir können dazu das Kommando `openssl` verweden:
```bash
openssl passwd -6 PASSWORT
```
Die Option `-6` weist `openssl` an, den für Linux empfohlenen sicheren *SHA-512* Algorithmus zu verwenden.

In einem Rutsch sähe das folgendermassen aus:
```bash
useradd -m -c "User mit Passwort" -p $(openssl passwd -6 'My!Secret#Password') -s /bin/bash userwithpass
```
### passwd
Das Kommando ermöglicht die Änderung von Passwörtern. Mit Root-Rechten können so die Passwörter aller Benutzer geändert werden:
```bash
passwd <user>
```
Als regulärer Benutzer kann man damit sein eigenes Paswsort ändern:
```bash
passwd
```
### chsh
Mit `chsh` kann ein Benutzer seine Login Shell ändern bzw. kann `root` die Login Shells jedes Users ändern.
```bash
chsh -s /bin/bash
```
### adduser

`adduser` ist ein Perl-Skript, welches u.a. die Kommandos  `useradd` und `passwd` ausführt. Es ist *interaktiv*, wir brauchen keine Optionen zu übergeben, bestimmte Einstellungen werden abgefragt, vor allem fragt `adduser` direkt nach einem Passwort für den neuen Benutzer. Es sind andere Default-Werte gesetzt als bei `useradd`, z.B. die `bash` als Login-Shell.

Dieses Kommando ist aber standardmässig nur auf Debian-basierten Distributionen vorinstalliert.

#### Relevante Dateien
Beim Anlegen von Benutzern passiert übrigens nur folgendes:

- Ein Eintrag in der `/etc/passwd` mit den Benutzerinformationen wird erzeugt
- Das Passwort wird in die `/etc/shadow` eingetragen
- Die primäre Gruppe wird zur `/etc/group` hinzugefügt (und eventuell andere Gruppenzugehörigkeiten angepasst)
- In der `/etc/gshadow` wird ein Eintrag ohne Passwort erzeugt (diese Datei bzw. Gruppenpasswörter werden eh nicht genutzt)

Das war's. Nichts weiter. Keine Magie, nichts im Hintergrund. Nur Veränderung von Textdateien. Das ist ein gutes Beispiel dafür, wie die Konfiguration eines Linux System generell funktioniert. 

### Gruppen

Mit Gruppen können mehrere Benutzer zusammengefasst und ihnen gemeinsame Berechtigungen auf Dateien und Verzeichnisse gegeben werden.

Im Unterschied zu Windows können Gruppen nur einzelne Benutzer enthalten, keine weiteren Gruppen.

Für die Anzeige der Gruppenzugehörigkeiten kann man die Kommandos `groups` oder `id` benutzen.

#### Primäre Gruppe
Jeder Benutzer hat genau eine primäre Gruppe. Diese ist in `/etc/passwd` eingetragen. In der Regel hat sie den gleichen Namen wie der Benutzer. Sie ist nötig, da z.B. beim Erstellen von Dateien diese einem Benutzer und einer Gruppe zugewiesen werden.

#### Sekundäre Gruppen
Ein Benutzer kann aber auch mehreren zusätzlichen Gruppen angehören. Die Zugehörigkeiten sind in der `/etc/group` eingetragen.

### Gruppe erstellen:
Auf allen Linux Systemen existiert das Kommando `groupadd`
```bash
groupadd <gruppe>
```
### Benutzer einer Gruppe hinzufügen:
Auch die Gruppenzugehörigkeiten passen wir mit dem Kommando `usermod` an:
```bash
usermod -g <primary-group> <user>
usermod -G <absolute-list-of-supplementary-groups> <user>
usermod -aG <group1>,<group2>,<group3> <user>
```
Vorsicht mit der Option `-G`, diese erwartet eine absolute Liste von Gruppen, die der User angehören soll. Gehört der User einer Gruppe an, die hier nicht genannt ist, wird er aus dieser Gruppen entfernt.

Möchten wir einen User einer Gruppe hinzufügen, die bestehenden Gruppenzugehörigkeiten aber nicht verändern, nutzen wir zusätzlich die Opione `-a` (steht für `--append`).

Damit Gruppenzugehörigkeiten gültig werden, muss die Datei `/etc/group` neu eingelesen werden. Dies geschieht z.B. wenn der Benutzer muss sich neu anmeldet bzw. eine neue Login-Shell startet. 

Um die Gruppenzugehörigkeit in der aktuellen Shell zu aktualisieren, kann auch das Kommando `newgrp <gruppe>` genutzt werden.

## sudo 

Mittels `sudo` (*Superuser do*) können Kommandos als ein anderer Benutzer ausgeführt werden. Standardmässig wird es genutzt, um als normaler Benutzer Root-Rechte zu erlangen, ohne sich als User `root` anmelden zu müssen.

#### Vorteile von `sudo`

- Benutzer gibt sein **eigenes** Passwort ein, nicht das von `root`
- Passwort von `root` muss nicht geteilt werden (sehr sinnvoll bei mehreren Administratoren)
- sehr fein granulare Rechtevergabe möglich: z.B. als ein bestimmter Bentuzer nur bestimmte Kommandos ausführen etc.
- kann auch so konfiuriert werden, dass gar kein Passwort eingegeben werden muss (nur unter ganz bestimmten Bedingungen sinnvoll)
- das eingegebene Passwort wird für eine gewisse Zeit (15 min) gespeichert und muss nicht immer wieder eingegeben werden und muss nicht immer wieder eingegeben werden
- alle `sudo` Kommandos werden in `/var/log/autho.log` protokolliert und sind zusätzlich in der History der jeweiligen Benutzer
- es wird vermieden, dass Benutzer aus Faulheit dauerhaft eine Root-Shell offen haben

#### Nachteile von `sudo`
- `sudo` ist Software und Software ist **nie fehlerfrei**
- Sicherheitslücken in `sudo` könnten ausgenutzt werden
- könnte falsch/unsicher konfiuriert werden

#### Konfiguration
Generell erfolgt die Konfiguration in der Datei `/etc/sudoers`. Diese sollte **nie direkt** sondern **immer** mit dem Kommando `visudo` bearbeitet werden.

Der einfachste Weg, einem User Root-Rechte mittels `sudo` zu gewähren, besteht darin, diesen User der Gruppe `sudo` bzw. `wheel` (je nach Distribution) hinzuzufügen.

Von einem Eintrag des/der User in die `/etc/sudoers` ist abzuraten, es sei denn, `sudo` soll feiner konfiuriert werden

>[!NOTE] 
> Falls man das vorherige Kommando erneut mit Root-Rechten ausführen will ist das Kommando `sudo !!` sehr nützlich. 
> 
> Das erste `!` steht für die History Expansion, das zweite für das vorherige Kommando.

## Berechtigungen

Berechtigungen in Linux steuern den Zugriff auf Dateien und Verzeichnisse für *Benutzer* und *Gruppen*. Sie legen fest, wer lesen (`r`), schreiben (`w`) und ausführen (`x`) darf.

Der folgende Auszug von `ls -l file1.txt` sagt folgendes aus:
```bash
  u  g  o
-rw-r--r-- 1 tux tux 5 Feb 12 13:09 file1.txt
```
- Der User/Besitzer (`u`) darf den Inhalt der Datei lesen und ändern (`rw`)
- Mitglieder der Gruppe (`g`) dürfen den Inhalt der Datei nur lesen (`r`)
- Alle anderen Benutzer, die weder der Besitzer, noch Mitglieder der Gruppe sind, dürfen den Inhalt der Datei lesen (`r`)

### Bedeutung der Berechtigungen für Dateien

`r` (*read*) -> Dateiinhalt lesen
`w` (*write*) -> Dateiinhalt ändern -> aber **nicht** Datei löschen
`x` (*eXecute*) -> Datei ausführen

### Bedeutung der Berechtigungen für Verzeichnisse

`r` (*read*) -> Verzeichnisinhalt lesen bzw. das Auflisten der Namen der Dateien
`w` (*write*) -> Verzeichnisinhalt ändern -> Dateien erstellen, verschieben und löschen
`x` (*eXecute*) -> Verzeichnis betreten 

>[!IMPORTANT] 
> Es macht **keinen wirkliche Sinn** wenn das Execute Bit bei Verzeichnissen **nicht** gesetzt ist. Dann wird alles etwas seltsam... Wir brauchen dieses Bit, damit Verzeichnisse wie gewünscht funktionieren.

### Symbolische Rechtevergabe
Hierbei werden *Symbole* für die Berechtigungen verwendet. Diese Art der Rechtevergabe ist sehr intuitiv und eignet sich besonders dafür, einzelne Berechtigungen hinzuzufügen oder zu entfernen, ohne die bestehenden Berechtigungen zu verändern. Es ist auch einfach, diese Vorgänge wieder rückgängig zu machen.

#### Symbole

`r` -> read
`w` -> write
`x` -> eXecute

`u` -> user/owner
`g` -> group
`o` -> others (weder owner noch group)
`a` -> all

`+` -> hinzufügen
`-` -> entziehen
`=` -> setzten

Der Gruppe Schreibrechte hinzufügen:
```bash
chmod g+w file1.txt
```
Dem Besitzer Leserechte entfernen:
```bash
chmod o-r file1.txt
```
Besitzer und Gruppe Schreib- und Leserechte
```bash
chmod ug+rw file1.txt
```
Dem Besitzer Ausführungsrechte hinzufügen, der Gruppe Schreibrechte entziehen, allen anderen Leserechte hinzufügen.
```bash
chmod u+x,g-w,o+r file1.txt
```
### Numerische/Oktale Rechtevergabe
Die numerische oder oktale Rechtevergabe verwendet Zahlen des Oktalsystems, um Berechtigungen gleichzeitig für Besitzer, Gruppe und Others zu vergeben. 

Es eignet sich besonders für Situationen, in denen wir eine Datei oder Verzeichnis in einen expliziten Zustand versetzten wollen.

Interessant ist die Herkunft der Zahlen für die Berechtigungen. Übersetzen wir sie doch einmal ins Binärsystem:

| Symbol | Okal | Binär |
| ------ | ---- | ----- |
| `r` | `4` | `100` |
| `w` | `2` | `010` |
| `x` | `1` | `001` |
| `-` | `0` | `000` |

Wir sehen, dass das gesetzte Bit *wandert* bzw. sich immer um eine Position verschiebt. Sehen wir uns das einmal im Listing von `ls -l` an:
```bash
  7  6  4
 111110100
-rwxr--r-- 1 tux tux 5 Feb 12 13:09 file1.txt

111 -> 7
110 -> 6
100 -> 4
```
Ist also ein bestimmtes Recht gesetzt, bedeutet dass, das hier binär auch eine `1` steht. Wir sehen sozusagen ein Abbild dessen, was wirklich im Speicher passiert. Toll, oder?

### Sonderbits
Zusätzlich gibt es noch drei Sonderbits, die gewisse Dinge ermöglichen, damit unser System funktioniert:

#### SUID Bit

Auf eine **ausführbare Binärdatei** gesetzt, bewirkt das SUID Bit, dass die Datei mit den Berechtigungen des **Besitzers** der Datei ausgeführt wird und **nicht** mit den Berechtigungen des aufrufenden Users.

##### Beispiel `/etc/passwd`
```bash
ls -l /usr/bin/passwd

-rwsr-xr-x 1 root root 68248 Feb 24  2025 /usr/bin/passwd

ls -l /etc/shadow

-rw-r----- 1 root shadow 1619 Feb 24 2025 /etc/shadow
```
Das Kommando kann also von einem regulären Benutzer ausgeführt werden, läuft dann aber mit den Rechten des Users `root` und kann somit den Inhalt der Datei `/etc/shadow` ändern.

#### SGID Bit

Auf eine **ausführbare Binärdatei** gesetzt, bewirkt das SGID Bit, dass die Datei mit den Berechtigungen der **Gruppe** der Datei ausgeführt wird und **nicht** mit den Berechtigungen des aufrufenden Users.

Auf ein Verzeichnis gesetzt, bewirkt es, dass neu darin erstellte Dateien der Gruppe zugewiesen werden, der das Verzeichnis gehört und nicht der primären Gruppe des erstellenden Users.

```bash
ls -ld /var/mail

drwxrwsr-x 2 root mail 4096 Feb 20 09:26 /var/mail/
```
So werden alle E-Mails der Gruppe `mail` zugeordnet und können vom Mailserver hinzugefügt und auch gelöscht werden.

#### Sticky Bit

Auf ein Verzeichnis gesetzt, bewirkt es, dass darin enthaltene Dateien nur noch vom Besitzer der Datei genändert oder gelöscht werden dürfen.
```bash
ls -ld tmp

drwxrwxrwt 8 root root 4096 Feb 20 09:30 /tmp
```
So ist es einem regulären Benutzer nicht möglich, Dateien eines anderen Benutzers zu ändern oder zu löschen.

## Links

### Symbolische Links / Symlinks
Sind im Prinzip das Gleiche wie Verknüpfungen unter Windows. Ein Symlink verweist auf eine andere Datei oder gesamtes Verzeichnis, genauer gesagt *auf den Pfad* zu einer Datei oder Verzeichnis. Es ist eine zusätzliche Inode, die auf ein Ziel verweist. Symlinks können auch über Partitionsgrenzen hinaus bestehen. Wird das Original gelöscht, bleibt ein sog. *toter* oder *verwaister* Link zurück, der nicht mehr funktioniert.
```bash
ln -s original.txt symlink.txt
ln -s originalverzeichnis symlinkverzeichnis
```
Symlinks werden z.B. von Webservern genutzt: 
- `/etc/apache2/sites-available` -> alle vorhandenen Konfigurationsdateien für Websites (Original)
- `/etc/apache2/sites-enabled` -> nur die *aktiven* Konfigurationsdateien für Websites (Symlink)

### Hardlinks
Hardlinks sind eigentlich lediglich Dateinamen. Mehrere Dateinamen bzw. Hardlinks können auf den gleichen Bereich im Speicher bzw. die gleiche Datei zeigen. Ein Hardlink ist nicht mehr vom Original zu unterscheiden, er hat die selbe Inode wie das Original. Wird das "Original" gelöscht, ist die Datei weiterhin über den "Link" bzw. jetzt neuen Dateinamen zu erreichen.

Hardlinks funktionieren daher natürlich **nicht** auf Verzeichnisse oder über Partitionsgrenzen hinaus.
```bash
ln original.txt hardlink.txt
```
Man kann die Anzahl der Hardlinks mit `ls -l` sehen (Spalte direkt nach den Berechtigungen) bzw. in der Ausgabe des Kommandos `stat`:
```bash
ln file1.txt hardlink-file1
ls -l file1.txt

-rw-r--r-- 2 tux tux 5 Feb 12 13:09 file1.txt

stat file1.txt

  File: file1.txt
  Size: 5         	Blocks: 8          IO Block: 4096   regular file
Device: 254,1	Inode: 1177496     Links: 2
Access: (0644/-rw-r--r--)  Uid: ( 1000/     tux)   Gid: ( 1000/     tux)
Access: 2025-02-17 08:55:39.987803189 +0100
Modify: 2025-02-12 13:09:04.146349786 +0100
Change: 2025-02-24 17:31:49.220713220 +0100
 Birth: 2025-02-12 11:45:38.078409807 +0100
```
Hardlinks werden im System verwendet, um Speicherplatz zu sparen z.B. für bestimmte Systemkommandos. Auch nutzen manche Backup Lösungen Hardlinks um inkrementelle Backups zu erstellen.







