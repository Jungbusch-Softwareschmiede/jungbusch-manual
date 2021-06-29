# Privilegien

Das Jungbusch-Auditorium erkennt vor dem Ausführen von Audit-Schritten, ob es mit Root-Privilegien auf Linux, bzw. Administrator-Privilegien auf Windows ausgeführt wurde (nachfolgend der Lesbarkeit wegen Admin-Rechte genannt). Dies wird gemacht, damit festgestellt werden kann, ob das Jungbusch-Auditorium für das Ausführen aller Audit-Schritte ausreichende Rechte hat. Nachfolgend werden die vier möglichen Fälle erläutert:

1. In der Audit-Konfiguration sind **keine** Module definiert, die Admin-Rechte benötigen. Der Prozess wurde **nicht** mit Admin-Rechten gestartet. 
Das Auditorium wird wie gewohnt ausgeführt.

2. In der Audit-Konfiguration sind **keine** Module definiert, die Admin-Rechte benötigen. Der Prozess wurde mit Admin-Rechten gestartet. 
Es wird eine Warnung ausgegeben, welche je nach eingestelltem Verbosity-Level auf der Konsole ausgegeben und in den Log geschrieben wird. Das Auditorium wird davon abgesehen wie gewohnt ausgeführt.

3. In der Audit-Konfiguration sind Module definiert, die Admin-Rechte benötigen. Der Prozess wurde **nicht** mit Admin-Rechten gestartet. 
Es wird ein Error ausgegeben und das Jungbusch-Auditorium beendet, außer in der Programmkonfiguration wurde der Parameter `ignoreMissingPrivileges` gesetzt.

4. In der Audit-Konfiguration sind Module definiert, die Admin-Rechte benötigen. Der Prozess wurde mit Admin-Rechten gestartet. 
Das Auditorium wird wie gewohnt ausgeführt.

## Funktionsweise

Auf Unix-Systemen wird die effektive ID des Prozesses (EGID) abgefragt.

Auf Windows-Systemen wird überprüft ob `\\\\.\\PHYSICALDRIVE0` vom Prozess zugreifbar ist. Das Privilegien-System von Windows ist leider mit unterschiedlichen Arten von privilegierten Konten etwas kompliziert, dessen Umsetzung befindet sich aber außerhalb des Fokus für das Auditorium.

