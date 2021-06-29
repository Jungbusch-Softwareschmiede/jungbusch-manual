# Programmoutput

Im Output-Ordner des Jungbusch-Auditoriums befinden sich der Log, die `report.json`-Datei, sowie der `artifacts`-Ordner.

## Der Report

Zu Beginn des Reports werden generelle Informationen und Statistiken über die Audit-Schritte gelistet. In die Kategorie `not_executed` fallen Schritte dann, wenn ihre Ausführbedingung nicht zutrifft oder wenn sie verschachtelte Schritte eines Schritts sind, der nicht ausgeführt wurde.

Danach sind die Audit-Schritte und ihre Ergebnisse aufgelistet. In der Audit-Konfigurationsdatei geschachtelte Schritte behalten diese Verschachtelung auch im Report bei. 

Bei Schritten, bei denen das result `PASSED` ist, wird die Schritt-ID, die Beschreibung sowie Artefakte aufgelistet. Bei Schritten, welche `NOTPASSED` sind, wird zusätzlich die angegebene Bedingung und das tatsächlich erhaltene Ergebnis angegeben. `UNSUCCESSFUL` ist ein Schritt dann, wenn bei dem Ausführen des Moduls ein Fehler aufgetreten ist. Dieser Fehler wird zusätzlich zu den Werten eines `NOTPASSED`-Schrittes ausgegeben.

## Der artifacts-Ordner

In diesem Ordner werden alle von den Audit-Schritten verwendete Dateien und Befehle gespeichert. Es werden jeweils Unter-Ordner erstellt, die dem Name der Schritt-ID entsprechen. Hat ein Schritt keine Artefakte, wird kein Ordner erstellt.

