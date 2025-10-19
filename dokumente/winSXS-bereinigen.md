# Platz schaffen in Windows

Terminal als Admin Starten
```
DISM /Online /Cleanup-Image /StartComponentCleanup
```
Achtung der Befehl löscht die Restore Daten für Updates. Kein zurück mehr möglich ... !
```
DISM /Online /Cleanup-Image /StartComponentCleanup /ResetBase
```

Zum Fehler Beheben das machen

```
DISM /Online /Cleanup-Image /RestoreHealth
```

```
sfc /scannow
```

Infos aus diesem Video https://www.youtube.com/watch?v=OrK8mXa1lbo 
