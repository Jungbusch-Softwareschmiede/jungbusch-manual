# Betriebssysteme

## Der OS-Detector

Das Jungbusch-Auditorium erkennt das Betriebssystem des auszuführenden Systems automatisch. Das Ergebnis des Detectors kann mit einem Parameter überschrieben werden.

## OS-Kompatibilität in Modulen

Die einzelnen Module geben in ihrer `Initialize`-Methode eine Liste an kompatiblen Betriebssystemen an. Ein Modul ist zum Aufruf aus der Audit-Konfiguration nur verfügbar, wenn sich das aktuelle Betriebssystem in der Liste der Betriebssysteme des Moduls befindet. 

Module können folgende Betriebssysteme angeben:
```
ubuntu
debian
centos
rhel               // RedHat
sles               // Suse
sles_sap           // Suse SAP

windows10          // beinhaltet alle Versionen von Windows10
windowsserver2012
windowsserver2016
windowsserver2020
windows8
windows7
windowsxp

macos11.0
macos10.15
macos10.14
```

### Wildcards

Des Weiteren können folgende Wildcards angegeben werden:
```
all
windows
linux
darwin
```
Damit kann ein Modul als kompatibel mit allen Systemen einer Gruppe markiert werden.

## Beeinflussen der Kompatibilitäts-Überprüfung 

Mit dem Flag `skipModuleCompatibilityCheck` kann der gesamte Modul-Kompatibilitätscheck übersprungen werden. Somit werden alle Module geladen, die mit der Architektur des Systems kompatibel sind. 

Mit dem Flag `forceOS` kann das Ergebnis des OS-Detectors überschrieben werden. 

