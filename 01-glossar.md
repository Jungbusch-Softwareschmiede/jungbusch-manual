# Glossar

## Konfiguration
Die **Konfiguration** (Config, Config.ini, Programmkonfiguration) ist die `.ini`-Datei in welcher die Programm-Konfiguration gespeichert werden kann. Die Config-Datei ist die Alternative zum [CLI](#commandline-interface). Diese Datei ist nicht zwingend anzugeben.

## Commandline-Interface
Das **Commandline-Interface** (CLI) ist die Programmkonfiguration per Konsole durch das angeben von Parametern.

## Audit-Konfiguration
Die **Audit-Konfiguration** (Audit-Config, DotJBA) enthält den gesamte Ablauf des durchzuführenden Audits. Sie besteht jeweils aus einem oder mehreren [Audit-Schritt](#audit-schritt)en. 

## Audit-Schritt
Ein **Audit-Schritt**, oder auch **Audit-Modul**, ist ein einzelner in der [Audit-Konfiguration](#audit-konfiguration) definierter Schritt. 

## Modul
Ein Modul ist ein austauschbarer Programmteil im Jungbusch-Auditorium. "Austauschbar" bedeutet, dass Module unabhängig vom [Framework](#framework) entfernt und hinzugefügt werden können. Module werden aus der [Audit-Konfiguration](#audit-konfiguration) aufgerufen, erwarten Eingabeparameter und führen dann Kommandos oder System-Calls aus, oder lesen Dateien ein. Auf ihr Ergebnis kann in der Audit-Konfiguration per Variable zugegriffen werden und es wird automatisch in die Ergebnis-Datei geschrieben. Des Weiteren merkt sich jedes Modul selbst, welche Artefakte es verwendet hat. Später werden diese von allen Modulen gesammelt, sortiert und abgespeichert.

## Framework
Das Framework ist im Falle des `Jungbusch-Auditoriums` alles außer den Modulen. Unter anderem das Commandline-Interface, der OS-Detector sowie der Parser und Interpreter der Audit-Konfiguration.

