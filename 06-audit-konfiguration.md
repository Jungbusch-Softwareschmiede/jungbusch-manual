# Die Audit-Konfiguration

Die Audit-Konfigurationsdatei ist die wichtigste Schnittstelle des Jungbusch-Auditoriums. In ihr werden alle durchzuführenden Audit-Schritte definiert. Ihr Syntax wurde mit dem Ziel entworfen, dass sie übersichtlich und auch für außenstehende möglichst leicht verständlich ist. Ihr Syntax ist JSON-ähnlich.

## Audit-Schritte

Die Audit-Konfigurationsdatei (nachfolgend: Audit-Datei) besteht aus [Audit-Schritten](#audit-schritt). Der Syntax eines einzelnen Schritts wird nachfolgend anhand eines Beispiels beschrieben. 

```
{
    module:"FileContent"
    stepid:"3"
    description:"Ensure no legacy + entries exist in shadow"
    passed: if("%result% == ''")
	
	file:"/etc/shadow"
    grep:"^\+:"
},
```

Jeder Schritt steht in geschweiften Klammern, und wird mit einem Komma von dem darauffolgenden Schritt getrennt. In der ersten Zeile wird dafür das zu verwendende Modul aufgerufen, hier `FileContent`. Die `StepID` ist die einzigartige Erkennung des Schritts. Mit dem Parameter `description` kann eine kurze Beschreibung des Schritts definiert werden. Der Parameter `passed` legt fest, wann der Schritt als erfolgreich gilt (Siehe [Bedingungen](#bedingungen)). Die letzten beiden Parameter sind sogenannte `Modul-Parameter`. Jedes Modul erwartet unterschiedliche Eingabeparameter. 

Ein großer Teil aller Module hat den optionalen Parameter `grep`. Mit ihm kann das Ergebnis (`%result%`) des Moduls manipuliert werden, um das Überprüfen mit einer Bedingung zu vereinfachen.

## Parameter

- Groß- und Kleinschreibung wird bei den Parameternamen nicht berücksichtigt.

- Die Reihenfolge, in der die Parameter angegeben werden, macht keinen Unterschied.

- Schreibweise: `Name:"Wert"` (Ausnahme: [Bedingungen](#bedingungen)). 

- Zusätzlich zu den Parametern der Audit-Konfiguration selbst besitzt jedes Modul eigene Eingabe-Parameter. Siehe [Liste aller Module](#module-1).

### Ausführreihenfolge

Unabhängig davon, in welcher Reihenfolge die Parameter in der Audit-Konfiguration angegeben werden, wird ein Schritt immer in der selben Reihenfolge ausgeführt.

1. `Condition` - Es wird überprüft, ob die Ausführbedingung zutrifft

2. `Module` - Ausführen des Moduls

3. `Passed` - Es wird überprüft, ob die Passed-Bedingung zutrifft

4. `Print` - Wurde ein Print-Parameter spezifiziert, wird dieser ausgegeben

### Parameter der Audit-Konfiguration

#### module
- Name: module
- Alias: mod, modul
- Zwingend anzugeben: Ja
- Beschreibung: Mit diesem Parameter wird festgelegt, welches Modul der Audit-Schritt ausführen soll. Es gilt zu beachten, dass die Groß- und Kleinschreibung bei dem Name des Moduls berücksichtigt werden muss. Siehe [Liste aller Module](#module-1).

#### stepid
- Name: stepid
- Alias: stepidentification, id, identifikation
- Zwingend anzugeben: Ja
- Beschreibung: Die StepID ist die einzigartige Bezeichnung für den Schritt. Sie kann sowohl Zahlen als auch Zeichen enthalten. Sie ermöglicht die Zuordnung des Ergebnisses zu einem Audit-Schritt.

#### description
- Name: description
- Alias: desc, beschreibung, definition
- Zwingend anzugeben: Nein
- Beschreibung: Mit diesem Parameter kann eine Beschreibung gesetzt werden, die später sowohl im Log, als auch im Ergebnis wiederzufinden ist. 

#### passed
- Name: passed
- Alias: bestanden, erfolgreich
- Zwingend anzugeben: Nein
- Beschreibung: Mit diesem Parameter kann festgelegt werden, unter welcher Bedingung der Schritt als erfolgreich anzusehen ist. Wird `passed` nicht angegeben, ist der Schritt unabhängig vom Ergebnis erfolgreich, solange bei der Ausführung kein Fehler auftritt. Siehe auch: [Bedingungen](#bedingungen).

#### condition
- Name: condition
- Alias: cond, bedingung
- Zwingend anzugeben: Nein
- Beschreibung: Mit diesem Parameter kann eine Ausführ-Bedingung für den jeweiligen Audit-Schritt festgelegt werden. Der Schritt wird nur ausgeführt, wenn die angegebene Bedingung zutrifft. Siehe auch: [Bedingungen](#bedingungen).

#### requiresElevatedPrivileges
- Name: requiresElevatedPrivileges
- Alias: requiresAdmin, requiresRoot, requiresPrivileges, rootOnly, adminOnly
- Zwingend anzugeben: Nein
- Beschreibung: Mit diesem Parameter können die benötigten Privilegien eines Moduls überschrieben werden. Die einzelnen Module legen jeweils für sich selbst fest, ob sie zum Ausführen erhöhte Privilegien benötigen oder nicht. (Siehe [Liste aller Module](#module-1)). 

Allerdings gibt es Module, wie beispielsweise `FileContent`, welches den Inhalt der angegebenen Datei ausliest und für diese Aufgabe erstmal keine Privilegien benötigt. Möchte man allerdings beispielsweise `/etc/shadow` auslesen, benötigt man erhöhte Privilegien und sollte nun diesen Parameter auf `"true"` setzen. Wird der Parameter in solchen Fällen nicht korrekt angegeben, kann vor Starten der Ausführung der Audit-Schritte nicht sichergestellt werden, dass diese Fehlerfrei durchgeführt werden können. Weiterführende Informationen: [Privilegien](privilegien).

#### print
- Name: print
- Alias: ausgeben
- Zwingend anzugeben: Nein
- Beschreibung: Mit dem Print-Parameter können Text oder Variablen auf der Konsole und im Log ausgegeben werden. Der Print-Parameter wird verarbeitet, nachdem das Modul ausgeführt wurde. 

**Beispiel:** 
Ausgeben des Ergebnisses und des Passed-Werts

```print: "Modul-Ergebnis: %result%, Passed: %passed%"```

### Das Verwenden von Variablen in Parametern

Variablen können in Modul-Parametern verwendet werden. Sie können alleine oder zwischen anderem Text verwendet werden. Es gilt zu beachten, dass in jedem Fall um Modulparameter Anführungszeichen verwendet werden müssen. Der Name der Variable wird 1:1 mit ihrem gesetzten Wert ersetzt.

Siehe auch: [Variablen](#variablen).

**Beispiele:**
```
key: "HKEY_USERS\%sid%\Software\Policies\..."
sid: "%sid%"
```

## Bedingungen

Bedingungen werden im Jungbusch-Auditorium für den [Passed](#passed)- und [Condition](#condition)-Parameter verwendet. Bedingungen werden mit [GOJA](https://github.com/dop251/goja) ausgewertet und sind daher im ECMAScript 5.1-Syntax gehalten. Eine Bedingung muss in eine Zeile passen. Es können in der Auditkonfiguration deklarierte [Variablen](#variablen) verwendet werden.

Um Bedingungen können Anführungszeichen oder Backticks verwendet werden. Backticks haben den Vorteil, dass innerhalb der Bedingung weiterhin wie gewohnt Anführungszeichen verwendet werden können. Benutzt man um die Bedingung stattdessen Anführungszeichen, sollte man in der Bedingung selbst Hochkommas (`'`) verwenden.

```
passed: if("%result% >= '24'")
passed: if(`%result% >= "24"`)
```

### Das Verwenden von Variablen in Bedingungen

Variablen können auf unterschiedliche Arten in Bedingungen verwendet werden.

Das Jungbusch-Auditorium versucht, die Datentypen von Variablen zu erkennen und sie korrekt zu konvertieren. So kann man, vorausgesetzt das verwendete Modul gibt `true` oder `false` in seinem Ergebnis zurück, die `%result`-Variable selbst überprüfen:

```
passed: if("%result%")
```

Bei strings bietet es sich an, ECMAScript-Methoden wie beispielsweise `.includes()` zu verwenden: 

```
passed: if("%result%.includes('targeted')")
```

Zahlen werden ebenfalls konvertiert und können auf die gewohnte Art und Weise verglichen werden:

```
passed: if("%result% >= '24'")
```

### Multiline-Bedingungen

Mit dem [Script-Modul](#script) kann mehrzeiliger ECMAScript-Code ausgeführt werden. So können Werte beliebig bearbeitet werden und später in der Audit-Konfiguration weiterverwendet werden.

### Beispiele

Das Ergebnis eines Schritts wird als Bedingung für einen verschachtelten Schritt verwendet:

```
{
    module:"FileContent"
	...
    %auditrules% = %passed%
    {
        condition: if("%auditrules%")
        ...
    },
},
```

Zur Auswertung einer Passed-Bedingung wird ECMAScript-Syntax verwendet:

```
passed: if("%result%.includes('targeted') || %result%.includes('mls')")
```

```
passed: if("%result%.includes('= 0')")
```

```
passed: if("%result% == 'disabled'")
```

## Variablen

In der Audit-Konfiguration können neuen Variablen Werte zugewiesen werden, oder die Werte von Umgebungsvariablen beispielsweise in Bedingungen verwendet werden.

#### Syntax

Variablennamen werden immer von Prozentzeichen umschlossen, auch in Bedingungen. Einen Wert weist man ihnen mit einem `=`-Zeichen zu. Einer neuen Variable können die Werte von anderen Variablen, Umgebungsvariablen oder ein Wert in Anführungszeichen zugewiesen werden.

Eine einzelne Variable darf pro Schritt einmalig gesetzt werden. 

Variablennamen dürfen Buchstaben, Zahlen und `_` Unterstriche enthalten.

> **Vorsicht:** Bei Variablen ist die Groß- und Kleinschreibung nicht relevant. Das bedeutet, die Variable `%test%` und `%TesT` sind ein und dasselbe.

```
%myValue% = "Mein Wert"
%module_1_Result% = %result%
```

### Das Verwenden von Variablen

Variablen können im Script-Modul verwendet werden: [Script](#script)

Variablen können in Bedingungen verwendet werden: [Variablen in Bedingungen](#das-verwenden-von-variablen-in-bedingungen)

Variablen können in Parametern verwendet werden: [Verwendung von Variablen in Parametern](#das-verwenden-von-variablen-in-parametern)

### Umgebungsvariablen

Es stehen einige Umgebungsvariablen zur Verfügung, mit denen bspw. auf das Ergebnis eines Audit-Schritts zugegriffen werden kann. So kann man aus dem Ergebnis eine Bedingung bauen, sodass ein anderer Schritt nur ausgeführt wird, wenn diese zutrifft.

#### Sichtbarkeit von Umgebungsvariablen

Umgebungsvariablen sind, im Gegensatz zu herkömmlichen Variablen, nur in dem aktuellen Schritt gültig. Sie sind also nur innerhalb der geschweiften Klammern sichtbar und werden auch nicht an Kinder weitergegeben. Das bedeutet, dass wenn man den Wert einer Umgebungsvariable eines Schritts in dessen Kind verwenden möchte, man den Wert in eine herkömmliche Variable zwischenspeichern muss. Siehe [Beispiele](#beispiel-1).

#### %result%
In dieser Variable wird das Ergebnis des Schritts in Textform gespeichert. Es kann mit dem `grep`-Parameter, den viele Module implementieren, beeinflusst werden.

#### %passed%
Diese Variable ist entweder `true` oder `false`, je nachdem ob die `Passed`-Bedingung des Moduls zutrifft. Tritt beim Ausführen des Moduls ein Fehler auf (-> %unsuccessful% = `true`), dann ist Passed automatisch `false`.

#### %unsuccessful%
`true`, wenn die Ausführung des Moduls fehlgeschlagen ist. Umkehrschluss: Ist diese Variable `false`, dann wurde das Modul ohne Fehler ausgeführt.

#### %os%
Enthält das aktuelle Betriebssystem. Siehe [Betriebssysteme](#os-kompatibilität-in-modulen).

#### %currentmodule%
Enthält den Namen des aktuellen Moduls.

### Herkömmliche Variablen

#### Sichtbarkeit

Variablen eines Audit-Schritts sind für alle seine Kinder (also verschachtelte Module), sowie alle Kinder der Kinder sichtbar. 

```
{
	...
	%variable% = "wert"
	
	{
		...
		// sichtbar
		
		{
			...
			// sichtbar
			...
		},
		
		...
	},
	
	...
},

{
	...
	// Nicht sichtbar
},
```

#### Beispiel

```
{
	module:"FileContent"
	stepid: "5"
	description:"Ensure kernel module loading and unloading is collected"
	
	file:"/etc/audit/rules.d/audit.rules"
	grep:"modules"
	
	passed: if("%result% == '-w /sbin/insmod -p x -k modules\n-w /sbin/rmmod -p x -k modules\n-w /sbin/modprobe -p x -k modules\n-a always,exit -F arch=b64 -S init_module -S delete_module -k modules'")
	
	// Zwischenspeichern des Ergebnisses
	%auditrules% = %passed%
	
	{
		// Schritt wird nur ausgeführt, wenn die Passed-Bedingung des vorherigen Schritts zutrifft
		condition: if("%auditrules%")
	
		module:"Auditctl"
		stepid:"5.1"
		description:"Ensure kernel module loading and unloading is collected"
		
		grep:"modules"
		
		passed: if("%result% == '-w /sbin/insmod -p x -k modules\n-w /sbin/rmmod -p x -k modules\n-w /sbin/modprobe -p x -k modules\n-a always,exit -F arch=b64 -S init_module -S delete_module -k modules'")
	},
},
...
```

### Globale Variablen

Wenn die Verschachtelung der Module zum weitergeben der Variablen an Kinder keine Option ist, sondern bestimmte Werte über die gesamte Audit-Konfiguration verwendet werden, gibt es die Option der globalen Variablen. Diese können nur unter folgenden Bedingungen gesetzt werden:

1. Ein Audit-Schritt ist dann global, wenn er Variablen enthält, die den Prefix "%g_" haben.
2. Ein `globaler Schritt` darf nur der allererste Schritt in der Audit-Konfiguration sein.
3. Soll es mehrere globale Schritte geben, müssen sie, **ohne von non-globalen Schritten unterbrochen zu werden**, ebenfalls am Anfang der Datei stehen. Also: globale Schritte dürfen ausschließlich **vor** dem ersten non-globalem Schritt stehen.
4. Globale Schritte dürfen weder selbst verschachtelt sein, noch verschachtelte Schritte beeinhalten.

Die so definierten globale Variablen dürfen in non-globalen Schritten nur verwendet, aber nicht überschrieben werden (Read-Only).

#### Beispiel

Beispiel aus der Windows-Education JBA-Datei:

```
//
// Set global variables
//
{
	stepid: "0-DumpSecuritySettings"
	description: "Dump the current security-settings in a file."
	module: "DumpSecuritySettings"

	%g_dumpCreated% = %passed%
},
{
	stepid: "0-GetGuestName"
	description: "Get the name of the local guest account."
	module: "GetAccountName"

	typ: "Guest"
	%g_guest% = %result%
},
{
	stepid: "0-GetCurrentUsername"
	description: "Get the name of the current local user."
	module: "GetAccountName"

	typ: "User"
	%g_user% = %result%
},
{
	stepid: "0-GetSIDOfCurrentUser"
	description: "Get the SID of the current local user."
	module: "GetUserSID"

	userName: "%g_user%"
	%g_userSID% = %result%
},

//
// Start audit process
//
{
	condition: if("%g_dumpCreated%")
	stepid: "1.1.1"
    desc: "Ensure 'Enforce password history' is set to '24 or more password(s)' (Automated)"
    module: "SecuritySettingsQuery"

	valueName: "PasswordHistorySize"
	passed: if("%result% >= '24'")
},
...
```

