# 2 - C# Syntax
> Beware of the curly brackets

## Python vs C#
**{ }**
```python
if (pythonToCsharp == true):
	removeColonFromIf()
	addCurlyBrackets
	addSemiColons
```
```csharp
if (pythonToCsharp == true)
{   // single or multiple lines
	removeColonFromIf();
	addCurlyBrackets();
}

if ( pythonToCsharp == true)
	addSemiColons(); // single line
```
**indenting, next line**
```python
if (pythonToCsharp == true):
	removeColonFromIf()
	addCurlyBrackets
	addSemiColons
```
```csharp
if (pythonToCsharp == true) {
removeColonFromIf();
addCurlyBrackets();
addSemiColons();
}

if ( pythonToCsharp == true
	&& newToThis == true)
{ breathe(); askForHelp(); }

if (oGodWhy) runForIt();
```

## Datatypes
| Type | Omschrijving | Waarde | |
|--|--|--|--|
| **Gehele getallen** | | Minimum | Maximum |
| int | integer | *-2^31^* | *2^31^* |
| long | long integer | *-2^63^* | *2^63^* |
| **Reële getallen** | | Minimum | Maximum |
| float | kommagetal (+/-) | *1,5 x 10^-45^* | *3,4 x 10^38^* |
| double | preciezer kommagetal (+/-) | *-2^31^* | *2^31^* |
| decimal | geldbedragen |  |
| **Tekst** | | |
| string | tekenreeks | | |
| **Andere types** | | |
| char | 1 teken | | |
| bool | booleaanse waarde | *0 (waar)* | *1 (onwaar)* |

## Collections
**Array, Dictionary\<TKey, TValue>, List\<T>**

### Arrays
```csharp
// initialize int array with 10 positions:
int[] numbers = new int[10];

// save number 13 in the first position
numbers[0] = 13;

// print the value of the first number in the array:
Debug.WriteLine(("The first number is: " + numbers[0]);

// intialize and fill another array with 4 numbers:
int [] startPositions = { 4, 1, 9, 3 };
```

### Dictionary\<TKey, TValue>
```csharp
// declare dictionary with key type & value type
Dictionary<string, int> studentScores = new Dictionary<string, int>();

// add two elements (key value pairs)
studentScores.Add("Jean Jacques", 13);
studentScores.Add("Jean Jacques", 4);

// get the score of Jean Jacques
int score = studentScores["Jean Jacques"];
```

### List\<T>
```csharp
// declare list, fill one by one:
List<string> emailList = new List<string>();
emailList.Add("karel.bousson@student.howest.be");
emailList.Add("bousson.karel@gmail.com");

// get elements out (two ways):
string frist = emailList.ElementAt(0);
string second = emailList[0];

// declare + fill list
List<string> teacherList = new List<string> { "SWC", "FWA" };
```

### Collection type = fixed
```csharp
Person[] teacherArr = new Person[10];
List<Person> teacherList = new List<Person>();

// You can only add Person objects to these
```

## Selections
**if / else if / else**
```csharp
if (findTheoryTeacher == true) {
	email1 = "frederik.waeyaert@howest.be";
	email2 = null;
}
else if (findLabTeacher == true) {
	email1 = "stijn.walcarius@howest.be";
	email2 = "frederik.waeyaert@howest.be";
}
else {
	email1 = email2 = null;
}
```

**switch**
```csharp
switch (teacher) {
	case "SWC":
		email = "stijn.walcarius@howest.be";
		break;
	case "FWA":
		email = "frederik.waeyaert@howest.be";
		break;
	default:
		email = "info@howest.be";
		break;
}
```

## Loops
**for**
```csharp
//loop 100 times
for (int i = 0; i < 100; i++) {
	//do something
}
```

**foreach**
```csharp
List<string> teacherList = new List<string> { "SWC", "FWA" };

foreach (string teacher in teacherList) {
	// do something
}
```

**while**
```csharp
while (endOfClass == false) {
	// might never be executed
}
```

**do while**
```csharp
do {
	// executed at least once!
} while (endOfClass == false);
```

## Classes
```csharp
public class Person {
	// property
	public string Name { get; set; }
	
	// constructor
	public Person (string name) {
		this.Name = name;
	}
	
	// method
	public void Subscribe() {
		// do something
	}
}
```

```csharp
// based on the constructor
Person p1 = new Person("Karel");
```

## Properties
### Fields vs properties
**Fields**
private of protected
Enkel binnen die klasse kan je er iets mee doen.
```csharp
// field
private string _name;
private int _id;
```

**Properties**
```csharp
// property with visible field
public string Name {
	// I want to GET the value of Name
	get {
		return _name;
	};
	// I want to SET the value of Name
	set {
		_name = value;
	};
}

// property with auto-implemented field (hidden field)
public double Alcohol { get; set; }
```

### Property usage
Properties to manage field access
```csharp
// property which you can't SET outside of this class
private int _id;
public int Id { 
	get { return _id; }
	private set { _id = value }
}
```

Check the input using SET
```csharp
public double Alcohol { 
	get { return _alcohol; }
	set {
		if (value < 0)
			_alcohol = 0;
		else if (value > 100)
			_alcohol = 100;
		else
			_alcohol = value;
	}
}
```

Control the output using GET
```csharp
// property which you can't SET outside of this class
public string Name { 
	get {
		if (string.IsNullorWhiteSpace(_name))
			return "Unknown";
		else
			return _name;
	}
	set { _name= value }
}
```

**Calculated properties** 
= properties build on other properties
- no field required
- reusability
```csharp
public int Description{ 
	get {
		return $"{this.Name} is being brewed in ${this.Brewery}";
	}
}
```

### Default values for properties
```csharp
public string Brewery { get; set; } = "Belgian Brewery";
```
```csharp
private Guid _id = Guid.NewGuid();

public Guid Id {
	get {
		return _id;
	}
	private set {
		_id = value
	};
}
```

``
## Constructors
Set default values
```csharp
public class Person() {
	public Person (string name) {
		this.Color = "Unknown";
	}
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5NjI2NDczMTMsLTY5MzIxMjgxOSwtMT
I4Mjc1MTY4LC05OTY5MjE2MDMsMjUwOTQ4NDA3LC0yMDA1ODQ0
MTk2XX0=
-->