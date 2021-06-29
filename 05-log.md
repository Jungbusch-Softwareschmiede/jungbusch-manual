# Log

Der Log ist neben dem Ergebnis die einzige Möglichkeit für den Benutzer um nachzuverfolgen, was das Jungbusch-Auditorium konkret macht. Der `Logger` ist zuständig für die Konsolenausgaben, aber auch für das Schreiben einer Log-Datei. Die Log-Datei wird im [Output](todo)-Ordner des Auditoriums abgelegt. 

## Ausgabe-Stufen

Das Jungbusch-Auditorium bietet fünf unterschiedliche Verbosity-Stufen, die über Parameter gesetzt werden können:

0 = NONE  
1 = ERROR  
2 = WARNING  
3 = INFO  
4 = DEBUG  

Bei der Stufe `NONE` wird überhaupt nichts ausgegeben. Es empfiehlt sich, diese Stufe maximal für die Konsole anzugeben.

Bei der Stufe `ERROR` werden ausschließlich die Nachrichten kritischer Fehler ausgegeben. Tritt ein kritischer Fehler auf, ist die weitere Ausführung des Programms nicht möglich.

Bei der Stufe `WARNING` werden die Nachrichten kritischer Fehler und Warnungen ausgegeben. Eine Warnung wird beispielsweise dann ausgegeben, wenn das Programm möglicherweise nicht korrekt konfiguriert ist, oder ein Fehler auftritt, der aber innerhalb des Programms behandelt werden kann.

Bei der Stufe `INFO` werden die Nachrichten kritischer Fehler, Warnungen und zusätzliche Informationen ausgegeben, wie beispielsweise in welchem Programmteil sich der Prozess befindet und welche Schritte aktuell abgearbeitet werden.

Bei der Stufe `DEBUG` werden die Nachrichten aller vorherigen Stufen, sowie eine Vielzahl von zusätzlichen Informationen ausgegeben. Diese können dafür verwendet werden, Fehler in Modulen oder im Rest des Frameworks zu identifizieren.

## Auftreten eines Fehlers vor Initialisierung des Loggers
 
Bevor der Logger initialisiert werden kann, muss die Programmkonfiguration eingelesen und der Output-Ordner erstellt werden. In diesen Programmteilen können möglicherweise bereits unerwartete Fehler auftreten (beispielsweise durch einen ungültigen Output-Pfad in der Konfigurationsdatei). In diesem Fall versucht das Jungbusch-Auditorium trotzdem eine Log-Datei zu erstellen um sicherzustellen, dass der Benutzer den Fehler nachverfolgen kann.

Es wird versucht, Log-Dateien an unterschiedlichen Pfaden in der folgenden Reihenfolge zu erstellen. Schlägt dies Fehl, beispielsweise aufgrund von fehlenden Berechtigungen, wird der nächste Pfad probiert.

- Log-Datei im angegebenen Output-Ordner

- Log-Datei am Pfad der Executable

- Log-Datei in der Working-Directory

- zusätzlich:

**Windows**:

- Log-Datei im Pfad `%appdata%\JungbuschAuditorium`

**Unix-Systeme**:

- Log-Datei im Pfad `/var/log/JungbuschAuditorium`

An welchem Pfad eine Log-Datei erstellt wurde, wird unabhängig vom Log-Level auf der Konsole ausgegeben. Konnte an keinem der Pfade eine Log-Datei erstellt werden, wird der aufgetretene Fehler unabhängig vom Log-Level auf der Konsole ausgegeben.

