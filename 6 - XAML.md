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
- A view's preferred alignment determines its position and size within the rectangle allocated for it by its container.

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

### Flash Quiz
Default **HorizontalOptions** is **Fill**, which causes WidthRequest to be ignored.

---
```xml
<StackLayout>
	<Label Text="Hello" HorizontalOptions="Center" BackgroundColor="Silver" />
</StackLayout>
```

HorizontalOptions != Fill and WidthRequest is not defined, so the size is based on its text.
![](https://i.imgur.com/mvgt2mO.png)

---
```xml
<StackLayout>
	<Label Text="Hello" HorizontalOptions="Center" WidthRequest="200" BackgroundColor="Silver" />
</StackLayout>
```
HorizontalOptions != Fill and WidthRequest is defined, so the requested width is respected.
![enter image description here](https://i.imgur.com/jrGLOTZ.png)

## Margin & padding
### Margin
- Margin is extra space around the outside of a view (available in all views, including containers)

### Padding
- Padding is extra space on the side of a layout that creates a gap between the children and the layout itself (applicable only to layouts)

### Flash Quiz
```xml
<StackLayout Padding="50">
	<BoxView Color="Silver" Margin="50" HeightRequest="50" />
	<BoxView Color="Blue" Margin="50" HeightRequest="100" />
</StackLayout>
```
Layout padding and view margin yield 100 here.

Each view has a margin of 50 and they are additive so the gap here is 100.
![](https://i.imgur.com/vFjbxVL.png)

## StackLayout
> StackLayout arranges its children in a single column or a single row
![enter image description here](https://i.imgur.com/N9vH4UP.png)
+ You can add children to a StackLayout in XAML
  + Layout order is determined by the order they were added to the Children collection (applies to both code and XAML)
- StackLayout's **Spacing** separates the children (default: 6)
+ StackLayout's **Orientation** property lets you choose a vertical column or a horizontal row (default: vertical)

### LayoutOptions against/with orientation
- In the direction *opposite* of its orientation StackLayout uses the Start, Center, End and Fill layout options.
```xml
<StackLayout Orientation="Vertical">
	<Label ... HorizontalOptions="Start" />
	<Label ... HorizontalOptions="Center" />
	<Label ... HorizontalOptions="End" />
	<Label ... HorizontalOptions="Fill" />
</StackLayout>
```
- In the direction of its orientation, StackLayout ignores the Start, Center, End and Fill layout options.
```xml
<StackLayout Orientation="Vertical">
	<Label ... VerticalOptions="Start" />
	<Label ... VerticalOptions="Center" />
	<Label ... VerticalOptions="End" />
	<Label ... VerticalOptions="Fill" />
</StackLayout>
```

### What is expansion?
- A view's expansion setting determines whether it would like the StackLayout to allocate available extra space to its rectangle.
![](https://i.imgur.com/96oBAph.png)

+ StackLayout expands children only in the direction of its orientation.
![](https://i.imgur.com/NXnm6ni.png)

#### How much extra space?
- StackLayout determines the amount of extra space using its standard layout calculation as if there were no expansion.
```xml
<StackLayout Orientation="Vertical">
	<Label Text="One" HeightRequest="100" ... />
	<Label Text="Two" ... />
	<Label Text="Three" HeightRequest="50" ... />
</StackLayout>
```
*Uses requested size if provided or "default" size if not.*

- To request expansion, use the "...AndExpand" version of the layout options in the direction of the StackLayout's orientation.

```xml
<StackLayout Orientation="Vertical">
	<Label ... VerticalOptions="StartAndExpand" />
	<Label ... VerticalOptions="CenterAndExpand" />
	<Label ... VerticalOptions="EndAndExpand" />
	<Label ... VerticalOptions="FillAndExpand" />
</StackLayout>
```

### Expansion vs. views size
- Enabling expansion can change the size of the view's layout rectangle, but doesn't change the size of the view unless it uses **FillAndExpand**
![enter image description here](https://i.imgur.com/8N4nczi.png)

#### No expansion against orientation
```xml
<StackLayout Orientation="Vertical">
	<Label ... HorizontalOptions="StartAndExpand" />
	<Label ... HorizontalOptions="CenterAndExpand" />
	<Label ... HorizontalOptions="EndAndExpand" />
	<Label ... HorizontalOptions="FillAndExpand" />
</StackLayout>
```
==
```xml
<StackLayout Orientation="Vertical">
	<Label ... HorizontalOptions="Start" />
	<Label ... HorizontalOptions="Center" />
	<Label ... HorizontalOptions="End" />
	<Label ... HorizontalOptions="Fill" />
</StackLayout>
```

## Apply Attached Properties
> An attached property is a property that is defined in once class but set on objects of other types.

![](https://i.imgur.com/vUMWnfk.png)

- Typically, a container will look for attached properties on its children.
  - *When a button is in a Grid, the grid reads the attached properties it needs...*

### Apply an attached property in code
```csharp
var button = new Button();

Grid.SetRow(button, 1);
Grid.SetColumn(button, 2);
```

### Apply an attached property in XAML
```xml
<Button Grid.Row="1" Grid.Column="2" ... />
```


## Grid
> Grid places its children into cells formed from rows and columns
![](https://i.imgur.com/EubZVAv.png)

### Grid rows/columns
- You specify the shape of the grid by defining each row and column individually

![](https://i.imgur.com/BHYCkaW.png)

### What is GridLength
- Gridlength encapsulates two things: unit and value
  - GridUnitType  **GridUnitType** (can be Absolute, Auto, Star)
  - double **Value**

#### Absolute Gridlength
Specifies a fixed row height or column width
```csharp
var row = new RowDefinition() { Height = new GridLength(100) };
```
```xml
<RowDefinition Height="100" />
```
*Value is in platform-independent units.*

#### Auto Gridlength
Lets the row height or column width adapt, it automatically becomes the size of the largest child.
```csharp
var row = new RowDefinition() {Height = new GridLength(1, GridUnitType.Auto)};
// value is irrelevant for Auto, it is typical to use 1 as the value when creating in code
```
```xml
<RowDefinition Height="Auto" />
```

#### Star Gridlength
Shares the available space proportionally among all rows/columns that use star sizing.
```csharp
var row = new RowDefinition() { Height = new GridLength(2.5, GridUnitType.Star) };
```
```xml
<RowDefinition Height="2.5*" />
```
- *XAML type converter uses * instead of Star using in code*
- "1*" and "*" are equivalent in XAML

#### Combinations
It is common to mix different GridLength settings in the same grid.
![enter image description here](https://i.imgur.com/kyCYQa6.png)

#### Default size
Rows and columns deault to '"1*" size

### Row/column numbering
Starts at 0 (row 0, column 0)

### Grid position properties
Grid defines four attached properties used to position children
| Attached property | Value |
|--|--|
| Column | int; Column in which the item will appear |
| ColumnSpan | int; Number of columns the item will span |
| Row | int; Row in which the item will appear |
| RowSpan | int; Number of rows the item will span |

### Cell specification
Apply the Row and Column attached properties to each child

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4Nzg0MjExNCw4ODg1NTUxNjUsLTQ3Mz
k1MzEwMSwtMTE2Mjk0NTc2OCwxNjgxNTg4MDc0XX0=
-->