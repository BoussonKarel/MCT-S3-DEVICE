# 5 - Performing CRUD operations on an API (JSON)
## From JSON data to a C# class
### Auto analyse vs. manual analysing
- **Auto analyse:** Edit > Paste special > Paste JSON as classes
- Not a good structure.
- Does not follow the C# naming conventions.

+ **Manual analysing**
+ Single item, array or a mix?

### Manual analysing
**Translate** property names is JSON to property names in C# (using Newtonsoft.Json).
```json
{
	"numberOfVotes": 5,
	"rating": 5.0,
	"id": "5a6e2e5e9e5d3fefe",
	"nl": "Alles suckt en zal altijd blijven sucken.",
	"author": "Hans"
}
```
```csharp
public class Quote {
	//[JsonProperty("id")]
	public string Id { get; set; }
	
	[JsonProperty("nl")]
	public string Content { get; set; }
	
	//[JsonProperty("author")]
	public string Author { get; set; }
	
	//[JsonProperty("rating")]
	public double Rating { get; set; }
	
	//[JsonProperty("numberOfVotes")]
	public int NumberOfVotes { get; set; }
}
```

- Analyse the JSON data yourself
- Select only the properties you need
- Choose clear names that follow the naming conventions
- Make use of an exisitng library like Newtonsoft

## GET data async

In QuoteRepository:
```csharp
	// define BASE URI
	private const string _BASEURI = "api-url.com/route";
```
```csharp
	// Prepare the HttpClient
	private static GetHttpClient() {
		HttpClient client = new HttpClient();
		
		// Type of data: JSON
		client.DefaultRequestHeaders.Add("Accept", "application/json");
		// ... (more headers)
		
		return client;
	}
```
```csharp
	// GET a single quote
	public static async Task<Quote> GetRandomQuote() {
		// URL from API documentation
		string url = $"{_BASEURI}/quotes/random";

		// Create and use HttpClient
		using (HttpClient client = GetHttpClient()) {
			try {
				// Ask for JSON data
				string json = await client.GetStringAsync(url);

				// Convert to a Quote object
				Quote quote = JsonConvert.DeserializeObject<Quote>(json);
				
				return quote;
			}
			catch (Exception ex) {
				throw ex; // ALWAYS add breakpoint here
			}
		}
	}
```
## Manipulate (PUT/POST/DELETE) data async
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA3Nzk1NTc2NCwxMzgwMzAwNjg0XX0=
-->