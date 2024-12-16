# gitCommands

Kostenlose und gute git Schulung gibt es [hier.](https://www.udacity.com/course/version-control-with-git--ud123.)

[Git Dokumentation](https://git-scm.com/book/en/v2)

## Am haeufigsten verwendete git Befehle
| Kommando | Kommentar |
| ------ | ------ |
| git status |  |
| git add `<filename>` |  |
| git add . |  |
| git commit -m "eigener Kommentar" |  |
| git commit -am "eigener Kommentar" | siehe Beschreibung unten |
| git commit --amend | Commit Message kann nachträglich geändert werden (nur unmittelbar nach einem Commit) |
| git commit --amend -m "an updated commit message" | dito |
| git push |  |
| git diff |  |
| git checkout --`<filename>` |  |
| git rm `<filename>` |  |

## Die vier Ebenen von Git
| Stage | Kommentar |
| ------ | ------ |
| (optional) Git Remote-Server (github, gitlab, etc.) | Zur Kollaboration kann das Repo mit einem zentralen Server synchronisiert werden. |
| .git Repository | Committete Files bekommen einen eindeutigen Hashwert (SHA) und werden hier gesichert. |
| Staging Area | Hier können Dateien per 'commit' dem Repo hinzugefügt werden |
| Working Directory | Hier werden Dateien bearbeitet. Files können per 'git add ...' in die Staging Area gehoben werden.|

**Verlassen des Edit-Modus: ":q" (nicht speichern und verlassen.), ":wq" (speichern etc.)**

## Repository von der CLI erstellen
| Kommando | Kommentar |
| ------ | ------ |
| mkdir `<repository_name>` |  |
| cd `<repository_name>` |  |
| echo "# `<repository_name>`" >> README.md |  |
| git init |  |
| git add README.md |  |
| git commit -m "Initial commit" |  |
|  |  |
| git remote add origin https://gitlab.devops.telekom.de/vorname.nachname/repository_name.git | Erstellt Repo im Personal Bereich (Ordnername = git Username)  |
| git remote add origin https://gitlab.devops.telekom.de/ip-core/repository_name.git | Erstellt Repo im 'ip-core' Ordner |
| git push -u origin master |  |

## Repository von Gitlab nach lokal klonen
| Kommando | Kommentar |
| ------ | ------ |
| git clone https://gitlab.devops.telekom.de/ip-core/repository_name.git | Pfad wird in Gitlab etc. bereitgestellt |

## Repositorystatus anzeigen
| Kommando | Kommentar |
| ------ | ------ |
| git status | zeigt Zustand des Repos an |
| git diff `<filename>` | Unterschied zwischen bearbeiteter und Originaldatei im Working Directory |
| git diff HEAD <recent file> | dito |
| git diff `<filename 1>` `<filename 2>` |  |
| git diff `<SHA#1>` `<SHA#2>` | ... Unterschied zwischen zwei Commits |
| git diff `<branch#1>` `<branch#2>` | ... Unteschied zwischen zwei Branches |
| git blame `<date>` `<filename>` | Wer hat wann was gemacht? (Option der Zeilenauswahl: z. B.: -L 5, 15) |
| git log | Logfile aller Commit |
| git log --oneline | dito, One-Liner (nicht Onliner!) |
| git log --oneline -3 | ... die letzten drei commits |
| git log --oneline --since="2019-03-07“ |  |
| git log --since="1 week ago“ |  |
| git log --author=„Pohl" |  |
| git log --grep=„added" | ... commit enthaelt "Suchwort" |
| git log a04fdb1..05e337d |  von ... bis) |
| git log --format=short |  |
| git log --format=fuller |  |
| git log --pretty |  |
| git log `<SHA>` | bestimmten commit anhand seines Hashwerts anzeigen lassen |
| git log --stat |  |
| git log -p `<SHA>` | Zeigt die Codeänderungen eines bestimmten Commits an |
| git show -p | Zeigt die Codeänderungen des letzten Commits an |
| git show -p `<SHA>` | Zeigt ebenfalls die Codeänderungen eines bestimmten Commits an |
| git show `<SHA>` | dito |
| git show --stat |  |
| git log --oneline --decorate --graph --all | graphische Ansicht aller commits in allen branches |

## File- und Verzeichnis Historie anschauen
| Kommando | Kommentar |
| ------ | ------ |
| git ls-tree HEAD |  |
| git ls-tree HEAD~2 |  |
| git remote -v |  |

## Dateien in die Staging Area bringen (nötig um zu committen)

| Command | Comment |
| ------ | ------ |
| git add `<filename1>` `<filename2>` | ein oder mehrere Files stagen |
| git add . | alles stagen |

## Dateien aus der Staging Area entfernen/unstagen
# Zeiger auf unterschiedliche (Arbeits) Punkte im Projekt setzen
| Kommando | Kommentar |
| ------ | ------ |
| git reset HEAD `<filename>` | File unstagen |
| git reset HEAD~2 `<filename>`  | zwei commits zurück, etc.  |
| git reset hard HEAD | nachschlagen!!! |

## Änderungen rückgängig machen

### Dateien under Version Control (gestaged)
| Kommando | Kommentar |
| ------ | ------ |
| git restore --staged `<filename>` | letzte Änderungen verwerfen, ergo: File unstagen |
| git checkout `<SHA>` --`<filename>` |  |
|  |  |
| git mv `<filename alt>` `<filename neu>` | Datei umbenennen |
| git rm `<filename>` | Datei löschen |

### Commit rückgängig machen (geht nicht bei Merge)
| Kommando | Kommentar |
| ------ | ------ |
| git revert `<SHA-of-commit-to-revert>` |  Commit wird rückgängig gemacht aber nicht gelöscht (Änderungen bleiben dokumentatorisch erhalten |

### Commit löschen (geht auch bei Merge)
| Kommando | Kommentar |
| ------ | ------ |
| git reset --hard `<SHA-of-commit-to-rollback>` | Z <- A <- B <- C <- HEAD <= Rollback von C nach A mit HEAD auf A |
| git reset --soft `<SHA-of-old-HEAD>`| Hier D (loescht alles zwischen D und A) |
| git commit| Erzeugt neuen (Gesamt) Commit. Erfordert neuen beschreibenden Kommentar  |

### Dateien/Verzeichnisse nicht under Version Control (nicht gestaged) loeschen
| Kommando | Kommentar |
| ------ | ------ |
| git clean -n | Trockenuebung |
| git clean -f | Hannibal ante portas, Files werden geloescht |
|  |  |
| git rm -r --cached `<file>` | lokales File/Ordner bleibt erhalten, |
| git rm -r --cached `<foldername>` | ... Eintrag in gitlab wird geloescht |

### Repository komplett loeschen
| Kommando | Kommentar |
| ------ | ------ |
| rm -rf `<foldername>` | lokal |
| nur über Github etc. | remote, im entspr. Repo unter 'Settings' ganz unten bei 'Advanced' |

## Aenderungen committen (nötig, um zu pushen)
| Kommando | Kommentar |
| ------ | ------ |
| git commit -m „aussagekraeftiger Kommentar“ |  |
| git commit -am „aussagekraeftiger Kommentar“ | add and commit gleichzeitig (nur wenn Files vorher schon einmal der Staging-Area hinzugef. wurden) |
| git commit --amend | Commit Message kann nachträglich geändert werden (nur unmittelbar nach einem Commit) |
| git commit --amend -m "an updated commit message" | dito |
| git commit --amend --no-edit | Wenn man beim vorigen Commit vergessen hat ein weiteres File hinzuzufügen. Vorher: git add `<filename>` |

**Fetch before push!**
## Remote Repository mit dem Lokalen synchronisieren 'fetch/push'
| Kommando | Kommentar |
| ------ | ------ |
| git fetch | Remote repository importieren, (ohne autom. merge) |
| git pull | git fetch and git merge zusammen |

## Geaenderte Files aus der Staging Area nach remote 'pushen'
| Kommando | Kommentar |
| ------ | ------ |
| git push | lokales repository hochladen |
| git push -u origin master | bestimmte lokale repository branch hochladen |

## Dateien von der Versionskontrolle ausschliessen mit '.gitignore' file
| Kommando | Kommentar |
| ------ | ------ |
| touch .gitignore | ignore Datei erstellen etc. |
| git add .gitignore | relev. Files dort eintragen, dann stagen |
| git commit -m „message“ |  |

## Branching
| Kommando | Kommentar |
| ------ | ------ |
| git branch -M `<old branch name>` `<new branch name>` | vorhandene Branch umbenennen, z. B.: 'master' zu 'main' |
| git branch | zeigt alle Branches an (*=aktiv) |
| git branch `<branch name>` | legt eine neue Branch an |
| ls -la .git/refs/heads/ | zeigt alle Branchordner an |
| cat .git/HEAD | zeigt auf den Kopf d. akt. Branch |
| git checkout `<branch name>` | in andere Branch wechseln |
| git checkout -b `<new branch name>` | Branch anlegen und reinwechseln |
| git fetch (origin) | Lokale Branch mit Gitlab synchronisieren, bevor eine Remote Branch angezeigt werden kann |
| git checkout -b `<name remote branch>` origin/`<name remote branch>` | Ausgewählte Remote-Branch pullen und hineinwechseln |
| git branch -a (-v) | Zeigt alle (lokale u. remote) Branches an (v - verbose) |
| git branch -r (-v) | Zeigt nur remote Branches an (v - verbose) |
| git branch -m `<old branch name>` `<new branch name>` | Branch umbenennen |
| git branch --delete `<branch name>` | nicht aktive Branch loeschen |
| git branch -d `<branch name>` | Unmerged Branches löschen (s. u.) |
| git branch -D `<branch name>` | Unmerged Branches mit existierenden commits löschen |
| git push origin --delete `<remote-branch name>` | Remote Branch von der Konsole aus löschen |
| git push --set-upstream origin `<branch name>`  | Neu erstellte lokale Branch nach Gitlab pushen |
| git branch -d -r `<remote-branch name>`  | Anwenden, wenn die Remote Branch gelöscht wurde, aber noch ein lokaler Eintrag existiert |

## Noch nicht committete Aenderungen stashen/zwischenparken (ggfs. nötig bei Merge und beim Wechseln in eine andere Branch)
| Kommando | Kommentar  |
| ------ | ------ |
| git stash [-u] | Speichert geaenderte (-u: untracked) Files   |
| git stash save | Speichert Arbeitsstände mit Beschreibung |
| git stash list | Listet den Stash Stack mit allen Speichereinträgen |
| git stash show stash@{#} | Zeigt an welche Dateien in diesem Stash involviert sind |
| git stash show -p stash@{#} | Zeigt die tatsächlichen Änderungen für diesen Eintrag an |
| git stash pop stash@{#}  | Wendet den neuesten Stash Eintrag an und löscht diesen anschließend |
| git stash apply stash@{#}   | Wendet die Änderungen einer Speichernummer an |
| git drop stash@{#}    | Löscht die Änderungen einer Speichernummer  |
| git stash branch    | Speichert die Zwischenstände einer Branch |
| git stash clear   | Löscht alle Speicherstände    |

## Merging
| Kommando | Kommentar |
| ------ | ------ |
| git merge `<branch to merge from>` | von anderer Branch in die 'main' Branch importieren/speichern |
| git merge --no-ff fasty | erzeugt eine neuen SHA, merged SHA wird davor eingefügt |
| git merge --ff-only fasty | nur mergen wenn fast-forward möglich ist; ansonsten verwerfen |

#Merge Konflikte auflösen
| Kommando | Kommentar |
| ------ | ------ |
| git merge --abort |  |

## Tags and Tickets	// Tags werden nur explizit gepushed
| Kommando | Kommentar |
| ------ | ------ |
| git tag -a ticket123 -m "resolved ticket123 this commit cd1cfd1834876591“ |  |
| git tag list |  |
| git tag -l |  |
| git tag -l -n |  |
| git tag -d V2.4 | Tag "V2.4" loeschen |

## Bisecting (Commit finden, der einen Bug eingebracht hat)
Git durchsucht einen Bereich von Commits, indem es diesen Bereich bei jedem Aufruf in zwei gleich große Bereiche (bisecting) teilt und den mittleren Commit auswählt.
Dadurch gewährt git Zugriff auf den Repository Zustand des ausgewählten Commits, sodass der Code für diesen Commit getestet werden kann.
So grenzt bisecting die Anzahl der übriggebliebenen Commits immer mehr ein, bis der 'schädliche' Commit gefunden wurde oder nur noch ein Commit übrig bleibt.

Ist der relevante Commit gefunden, sucht man dort nach dem eigentlichen Bug. Ist dieser identifiziert, schließt man das bisecting ab (reset), um das Repository wieder in den Originalzustand zu versetzen, beseitigt den Bug im aktuellen Zustand und erstellt einen neuen Commit mit entsprechenden Hinweis. Bisecting reduziert durch seine binäre Aufteilung das Auffinden eines 'schädlichen' Commits im Vergleich der Einzelüberprüfung enorm.
Außerdem ist es ansonsten m. W. gar nicht oder nur sehr umständlich möglich vollumfänglich auf den Repository Zustand eines Commits zuzugreifen.

| Kommando | Kommentar  |
| ------ | ------ |
| git bisect start | Aktiviert git bisecting   |
| git bisect bad | Deklariert den aktuellen Repository Status als fehlerhaft (Hier ist der Bug ja vorhanden.) |
| git bisect good <SHA> | Damit deklariert man einen Commit, bei dem der Bug noch nicht vorhanden war. |

** git bisect reset nicht vergessen **

Bisecting teilt nun den Bereich in zwei gleich große Teile und wählt einen entsprechenden Commit aus, der auch angezeigt wird. Das Repository befindet sich nun in dem Zustand, der bei diesem Commit aktuell war.
Nun kann man seinen Code testen. Ist der Bug noch vorhanden, deklariert man diesen Commit als 'bad', ansonsten als 'good'. Dann wird von bisecting ein neuer Commit ausgewählt, bis der 'schädliche' Commit gefunden wurde.

| Kommando | Kommentar  |
| ------ | ------ |
| git status | Zeigt an, dass sich das Repository im Bisecting Modus befindet, indem HEAD auf einen Commit zeigt, der von bisecting ausgewählt wurde. |
| git bisect reset | WICHTIG: Versetzt das Repository wieder in den Originalzustand. |
