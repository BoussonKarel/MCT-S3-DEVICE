# 5 - Consuming webservices
## Asynchronous programming
Using the **async** and **await** keywords

### Synchronous
One thing at a time. User interface is blocked while the repository is doing an API / DB request.

### Asynchronous
The UI is still reponsive, it doesn't have to wait for repositories to finish requests.

### WHY asynchronous programming?
Continue to respond to user interaction, while...
![asychronous tasks](https://i.imgur.com/j6yU5s3.png)

### Creating an asynchronous function
**Return type void: Task**
```csharp
// synchronously
public static void SavePreferences()

// asynchronously
public static async Task SavePreferencesAsync()
```

**Return type T: Task\<T>**
```csharp
// synchronously
public static List<NewsItem> GetNewsItems()

// asynchronously
public static async Task<List<NewsItem>> GetNewsItemsAsync()
```

### Call an async method
```csharp
// MainPage.xaml.cs
public asynk Task FillNewsItemsAsync() {
	List<NewsItem> results = await NewsRepository.GetNewsItemsAsync();
	lvwNewsItems.ItemsSource = results;
}

// NewsRepository.cs
public static class NewsRepository {
	public static async Task<List<NewsItem>> GetNewsItemsAsync() {
		// load news items asynchronously
	}
}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODc4OTE1MTcsNjIwOTQ4NTI4LC0xOT
Y2MDc0MDYzXX0=
-->