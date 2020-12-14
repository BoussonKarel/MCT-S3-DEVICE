# 4 - OO Design Continued
## Inheritance
### What?
```csharp
public class Advisor {
	//properties
	public string Name { get; set; }

	// methods
	public void Advise() { }
}
```

```csharp
public class MinisterOfDefense: Advisor {
	// ...
}

public class MinisterOfHealthcare: Advisor {
	// ...
}
```

![Inheritance: specialisation, generalisation](https://i.imgur.com/xF19WbB.png)
- **Generalize** properties (**equal for all**) by putting them in the **base class**
- **Specify** properties (**specific for one**) by putting them in the **deriving class**

### Constructors
Constructor van de base class (Object) wordt opgeroepen, dan parent klasse, dan klasse zelf.

---
- Constructors are not inherited.
- Constructor without parameters in base class?
  - **Automatically** being called by deriving class.
```csharp
public class Soldier {
	public Soldier()
	{debug.WriteLine("Soldier reporting in")};
}

public class Medic : Soldier {
	public Medic()
	{debug.WriteLine("Who needs healing")};
}
```
> [0:] Soldier reporting in
> [0:] Who needs healing?
---
- No constructor without parameters in base class?
  - **Explicitly** call it in deriving classes.
  - Verplicht oproepen voor klasses die geen default constructor hebben.
```csharp
public class Soldier {
	public Soldier(bool canShoot)
	{debug.WriteLine("Soldier reporting in")};
}

public class Medic : Soldier {
	public Medic() : base(true)
	{debug.WriteLine("Who needs healing")};
}
```
> [0:] Soldier reporting in
> [0:] Who needs healing?

### Access Modifiers
| Modifier  | Applies to | Description |
|--|--|--|
| public | Any type or members | The item is visible to any other code |
| protected | Any member of a type, also the any nested type | The item is only visible in class and subclasses |
| private | Any type or members | The item is only visible in the class |
| internal | Any member of a type, also the any nested type | The item is only visible in it's containing assembly |

### Properties / Methods: VIRTUAL & OVERRIDE
**virtual** geeft de mogelijkheid om te overriden in de subclasse. *Je kan hem overriden, maar het hoeft niet.*

```csharp
public class Vliegtuig {
	public virtual void Vlieg() {
		Console.WriteLine("Het vliegtuig vliegt rustig door de wolken.");
	}
}

public class Raket : Vliegtuig {
}

new Vliegtuig().Vlieg();
new Raket().Vlieg();

```
> [0:] Het vliegtuig vliegt rustig door de wolken.
> [1:] Het vliegtuig vliegt rustig door de wolken.
```csharp
public class Raket : Vliegtuig {
	public override void Vlieg() {
		Console.Writeline("De raket verdwijnt in de ruimte.");
	}
}

new Vliegtuig().Vlieg();
new Raket().Vlieg();
```
> [0:] Het vliegtuig vliegt rustig door de wolken.
> [1:] De raket verdwijnt in de ruimte.

### Properties / Methods: ABSTRACT & OVERRIDE
**abstract** betekent dat je kan overerven, maar er geen instantie van kan maken.
```csharp
public abstract class Animal
	public int Name { get; set; }
}

public class Horse : Animal
	// ...
}

Animal animal = new Animal(); // ERROR
Wolf lilWolf = new Wolf(); // OK
```

## Polymorphism

## Interfaces

## Composition

<!--stackedit_data:
eyJoaXN0b3J5IjpbNzcyMTYwMDQsMTI5MjY0MjY1MV19
-->