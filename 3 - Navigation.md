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

```csharp

```

## Navigate back


## Navigation stack


## Page types


## Exchanging data



<!--stackedit_data:
eyJoaXN0b3J5IjpbOTAyMTA0NzYwLC04MzI2ODA5NjhdfQ==
-->