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
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTcwNDg1NTgyMywtMTE2Mjk0NTc2OCwxNj
gxNTg4MDc0XX0=
-->