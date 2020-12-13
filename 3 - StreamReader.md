# 3 - StreamReader
- Namespaces
- System.Reflection
- Embedded files
- System. IO

## Namespaces
```csharp
// using <namespace>
using Xamarin.Forms;

// namespace: System.Diagnostics
// class: Debug
System.Diagnostics.Debug.Writeline("DEVPROG");
```
Namespaces inside your projects
```csharp
MyXamarinApp
	MyXamarinApp.Assets
	MyXamarinApp.Models
	MyXamarinApp.Repositories
	MyXamarinApp.Views
MyXamarinApp.Android
MyXamarinApp.iOS
MyXamarinApp.UWP
```

## System.Reflection
*“The classes in the System.**Reflection** namespace, together with System.Type , enable you to obtain information about loaded assemblies and the types defined within, such as classes, interfaces, and value types. You can also use **reflection** to create type instances at run time and to invoke them.”*

*Contains types that retrieve information about assemblies, modules, members, parameters, and other entities in managed code by examining their **metadata**. These types also can be used to manipulate instances of loaded types, for example to hook up events or to invoke methods.*

Gecompileerde Assembly onderzoeken, onderzoeken van metadata...

## System.IO
- System.IO --> Input / Output
+ System.IO.StreamReader
- System.IO.StreamWriter

## Read an embedded file in Xamarin
*File op Embedded Resource zetten, dan maakt hij een resource id.*

```csharp
// Assembly bijhouden in een variabele
var assembly = typeof(Foo).GetTypeInfo().Assembly;
// Foo is klasse die bestaat in je project

// Wat is mijn resource id?
string resourceID = "namespace_of_file.filename.csv";

// Stream bepalen = ophalen adhv resource id binnen die assembly
Stream stream = assembly.GetManifestResourceStream(resoruceID);

using (var reader = new System.IO.StreamReader(stream)) {
	// process file content
}

```

### Processing the file's content
- Wat doet **using**?
  - StreamReader initialiseren
  - StreamReader deftig openen
  - StreamReader op het einde sluiten
```csharp
using (var reader = new System.IO.StreamReader(stream)) {
	reader.ReadLine(); // ignore title row
	string line = reader.ReadLine(); // read first line
	while (line != null) {
		// process line
		// ...
		// read next line
		line = reader.ReadLine();
	}
}
```

## Belangrijk
- You understand the importance of **namespaces** , and
the techniques of using them in your own projects.
+ You can explain the very basics of the **System.IO** and
**System.Reflection** namespaces, and what they have to
do with **reading an embedded file** in Xamarin.
- You understand the how and why of the **ResourceID**
that’s being generated for an embedded file.
+ The secret hint to create your own custom
**code snippets** gave you a true epiphany
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTc2NTQ3MDEyOF19
-->