# 6 - XAML
## XAML in Xamarin.Forms
E**x**tensible **A**pplication **M**arkup **L**anguage
- XAML was created by Microsoft specifically to describe UI

![](https://i.imgur.com/69Yi3cx.png)
![](https://i.imgur.com/eNY1NYt.png)
![XAML](https://i.imgur.com/XW7trfY.png)

- Easy designing of a UI
- Designer Friendly
- Separation of UI from Behavior

## Pages
Xamarin.Forms Pages represent closs-platform mobile application screens.
*ContentPage, MasterDetailPage, NavigationPage, TabbedPage, TemplatedPage, CarouselPage...*

### Adding a XAML Page
There are two Item Templates available to add XAML content
![enter image description here](https://i.imgur.com/RfEOKSi.png)
Een View kan je ook apart maken en hergebruiken in andere pagina's.

### Describing a screen in XAML
- XAML is used to construct object graphs, in this case a visual Page
![Element tags](https://i.imgur.com/7qFIa9b.png)

![Attributes](https://i.imgur.com/lAiRkO1.png)

![Child nodes](https://i.imgur.com/abApGdS.png)

### XAML + Code behind
- XAML and code behind files are tied together
![](https://i.imgur.com/9dTl4uS.png)

- Code behind constructor has to call ```InitializeComponent()``` which is responsible for loading the XAML and creating the objects.

![](https://i.imgur.com/ZXPOnl3.png)

### Naming Elements in XAML
- Use x:Name to assign field name
  - Allows you to reference element in XAML and code behind

+ Adds a private field to the XAML-generated partial class (.g.cs)

- Name must confirm to C# naming conventions and be unique in the file

```XML
<Entry x:Name="PhoneNumber" Placeholder="Number" />
```
```csharp
public partial class MainPage : ContentPage {
	private Entry PhoneNumber();
	
	private void InitializeComponent() {
		this.LoadFromXaml(typeof(MainPage));
		PhoneNumber = this.FindByName<Entry>("Phonenumber");
	}
}
```

### Handling events in XAML
- Can also wire up events in XAML - event handler must be defined in the code behind and have a **proper signature**.

Adding an event in XAML:
```XML
<Entry Placeholder="Number" TextChanged="OnTextChanged" />
```
Adding an event in code:
```csharp
public partial class MainPage : ContentPage {
	public MainPage() {
		InitializeComponent();
		
		PhoneNumber.TextChanged += OnTextChanged;
	}
}
```
The event:
```csharp
public partial class MainPage : ContentPage {
	void OnTextChanged(object sender, TextChangedEventArgs e) {
		...
	}
}
```

- Many developers prefer to wire up all events in code behind by naming the XAML elements and adding event handlers in code
  - Keep the UI layer "pure" by pushing all behavior + management into the code behind
  - Names are validated at compile time, but event handlers are not
  - Easier to see how logic is wired up

+ Pick the approach that works for your team / preference

## Layout in Xamarin.Forms
Using layout containers to calculate view size and position helps your UI adapt to varied screen dimensions and resolutions.

*Size/positions are recalculated automatically when device rotates*

### What is a layout?
A layout is a Xamarin.Forms container that determines the size and position for a collection of children.
![Layouts](https://i.imgur.com/cDOjC3j.png)

### What is a view?
Xamarin.Forms views are the building blocks of cross-platform mobile user interfaces.

Views are user-interface objects such as labels, buttons and sliders that are commonly known as controls or widgets in other graphical programming environments.

![views](https://i.imgur.com/k1HwGrD.png)

## Working with sizes
The rendered size of a view is a collaboration between the view itself and its layout container.
![enter image description here](https://i.imgur.com/2wAMIJb.png)

Layout panel asks each child how much room it would like, but then tells each child how much it gets.
![enter image description here](https://i.imgur.com/xaN0sQx.png)

## Flash Quiz
- Default **HorizontalOptions** is **Fill**, which causes WidthRequest to be ignored.

### Default view sizing
- By default, most views try to size themselves just large enough to hold their content.
  - *E.g. by default, Labels are sized based on their text.*

### View preferences
- A view has four properties that influence the rendered size; they are all requests and may be overruled by the layout container

![enter image description here](https://i.imgur.com/jCuJP8k.png)

### Size Units
- Explicit sizes in Xamarin.Forms have no intrinsic units; the values are interpreted by each platform according to that platform's rules

![enter image description here](https://i.imgur.com/JfuT5VD.png)

### Alignments
- A view's preferred alignment determines its position and size within the rectangle allocated for it by it's container.

```xml
<StackLayout>
	<Label Text="Start" HorizontalOptions="Start" BackgroundColor="Silver" />
	<Label Text="Center" HorizontalOptions="Center" BackgroundColor="Silver" />
	<Label Text="End" HorizontalOptions="End" BackgroundColor="Silver" />
	<Label Text="Fill" HorizontalOptions="Fill" BackgroundColor="Silver" />
</StackLayout>
```
![enter image description here](https://i.imgur.com/QZtGtxI.png)

### Size requests vs. Fill
- The Fill layout option generally overrides size preferences

Fill causes WidthRequest to be ignored.

## Flash Quiz
Default **HorizontalOptions** is **Fill**, which causes WidthRequest to be ignored.

---
```xml
<StackLayout>
	<Label Text="Hello" HorizontalOptions="Center" BackgroundColor="Silver" />
</StackLayout>
```

HorizontalOptions != Fill, so the size is based on it's text.
![](https://i.imgur.com/mvgt2mO.png)

---



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTU3MDczMjEsLTExNjI5NDU3NjgsMT
Y4MTU4ODA3NF19
-->