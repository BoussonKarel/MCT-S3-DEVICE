# 3 - Navigation
## Modal vs Modeless
- **Modal**
- Requires user input to continue.
- *bijvoorbeeld een pop-up*

+ **Modeless page**
+ User can go back any time he wants
+ No input required

## Navigate forward
```csharp
Navigation.PushAsync(new Foopage());
// Wanneer je naar een modal page wil sturen, waar effectief input verwacht wordt
Navigation.PushModalAsync(new Foopage());
```

**Opgelet: App.xaml.cs aanpassen**
```csharp
// MainPage = new MainPage();
MainPage = new NavigationPage(new MainPage());
```

## Navigate back
### Modeless page
- Default physical back buttons' behavior
- Own buttons:
```csharp
Navigation.PopAsync();
```

### Modeless page
- Disable physical back buttons' default behavior
- Own buttons:
```csharp
if (...) { Navigation.PopModalAsync() };
```

## Navigation stack
Soort pak kaarten
![Navigation Stack](https://i.imgur.com/yZfogLF.png)

![Navigation Stack extra's](https://i.imgur.com/7Quir4l.png)

## Page types
![](https://i.imgur.com/5lEE1Bl.png)
ContentPage e

## Exchanging data



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQxMzYxNTMyMCwtMTAxOTM3MTk3NCwtOD
MyNjgwOTY4XX0=
-->