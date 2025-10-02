Ein direktes Hochladen einer Zip-Datei als neues Repository ist in Gitea nicht möglich, weil Gitea – wie auch andere Git-Plattformen – keine Funktion bietet, ein Repository direkt aus einem Zip-Archiv zu erstellen. Stattdessen geht es folgendermaßen:[9]

### Vorgehensweise mit einem Zip-Archiv

- Das Zip-Archiv muss lokal entpackt werden.
- Im entpackten Ordner ein neues Git-Repository initialisieren (`git init`).
- Die Dateien mit `git add .` und `git commit -m "Initial commit"` dem Repository hinzufügen.
- Ein neues, leeres Repository in Gitea anlegen.
- Die lokale Repository-Konfiguration um die Remote-URL von Gitea ergänzen (`git remote add origin <URL>`).
- Die Dateien mit `git push origin main` (bzw. `master`, je nach Standard-Branch) ins Remote-Repository hochladen.[3][7]

### Gitea-Webinterface

Im Webinterface kann höchstens eine Zip-Datei als normale Datei hochgeladen werden, aber diese wird nicht als Projektstruktur erkannt. Sie befindet sich dann lediglich als einzelnes (Binär-)File im Repository, nicht als entpacktes Projekt mit Git-Verlauf.[9]

### Zusammenfassung

Ein Zip muss also entpackt und als normales Git-Projekt hochgeladen werden. Ein direktes „Zip → neues Repository“ gibt es weder in Gitea noch in anderen gängigen Git-Plattformen.[7][3][9]

[1](https://docs.github.com/de/get-started/start-your-journey/uploading-a-project-to-github)
[2](https://selftaughttxg.com/2024/09-24/how-to-create-a-new-github-repository-from-a-zip-file-project/)
[3](https://git-scm.com/book/de/v2/Git-Grundlagen-Ein-Git-Repository-anlegen)
[4](https://www.youtube.com/watch?v=euzEv60KeyE)
[5](https://docs.github.com/de/repositories/working-with-files/managing-files/adding-a-file-to-a-repository)
[6](https://www.reddit.com/r/github/comments/tcohe9/im_new_to_github_and_i_was_wondering_how_to_use/)
[7](https://www.atlassian.com/de/git/tutorials/setting-up-a-repository)
[8](https://www.trupeer.ai/de/tutorials/how-to-upload-a-folder-to-github)
[9](https://www.howtoforge.de/anleitung/so-installierst-du-die-gitea-devops-plattform-mit-docker-unter-debian-12/)
[10](https://docs.github.com/de/get-started/start-your-journey/downloading-files-from-github)
