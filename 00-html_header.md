---
title:  'Jungbusch-Auditorium: Benutzerhandbuch'

subtitle: |
  Dies ist das Benutzerhandbuch für das Jungbusch-Auditorium.
  Das Jungbusch-Auditorium `(JBA)` ist ein Framework, welches das Durchführen eines Sicherheitsaudits auf einer Maschine erleichtern soll. 
  
  Es wurde spezifisch für die Auslieferung an einen Kunden designed. Das bedeutet, dass die Software vollständig konfiguriert ausgeliefert werden kann und daraufhin keinerlei Nutzereingaben, angeben von Commandline-Parametern oder sonstige Konfiguration mehr benötigt. 
 
  Das JBA wird mit einer Vielzahl an Modulen für viele bekannte Betriebssysteme und Architekturen ausgeliefert, welche häufig verwendete Funktionalität zur leichten Verwendung verallgemeinern. Außerdem ist das Erstellen von nutzereigenen Modulen in Golang möglich, ohne dass Code des Frameworks selbst angepasst werden muss.
  
  Für das Definieren von Audit-Schritte wurde das JSON-ähnliche `.jba`-Dateiformat entwickelt, in welchem Auditschritte definiert, verschachtelt und mit Variablen oder Bedingungen untereinander verknüpft werden können. 
  
  Sobald alle Audit-Schritte abgeschlossen sind, wird eine detailreiche Output-Datei erstellt, welche nicht nur die Ergebnisse sammelt, sondern vor Allem auch mit dem Ziel entworfen wurde, die Ergebnisse nachvollziehbar zu machen. Um dies zu erreichen sammelt das Jungbusch-Auditorium jegliche Artefakte, die beim Ausführen der Schritte verwendet wurden. Dies beeinhaltet ausgelesene Dateien, ausgeführte Konsolen-Befehle und Systemcalls.
---