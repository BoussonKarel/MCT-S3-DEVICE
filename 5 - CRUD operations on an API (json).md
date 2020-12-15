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
	private const string _BASEURI = "api-url.com/api/v1";
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
	public static async Task<Quote> GetRandomQuoteAsync() {
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

- Use your own **model**
- Browse through the documentation to find the correct **endpoints**

+ Create the **repository functions**:
  + Use the **async** keyword
  + Wrap the **return type** in a **Task** (void) or **Task\<T>** object

- When **calling** these **async functions**:
  - Decide if it's necessary to **await or not**
  - The **return type** should be wrapped in a **Task** (void) or **Task<T>** object!

## Manipulate (PUT/POST/DELETE) data async
In QuoteRepository:
### PUT an object to the API to update it
```csharp
// UPDATE a single quote
	public static async Task UpdateQuoteAsync(Quote updatedQuote) {
		// URL from API documentation
		string url = $"{_BASEURI}/quotes";

		// Create and use HttpClient
		using (HttpClient client = GetHttpClient()) {
			try {
				// Serialize C# object to JSON string
				string json = JsonConvert.SerializeObject(updatedQuote);
				
				// Build the stringcontent with this serialize JSON object
				StringContent content = new StringContent(json, Encoding.UTF8, "application/json");
				
				// Request PUT using URL and the StringContent
				
			}
			catch (Exception ex) {
				throw ex; // ALWAYS add breakpoint here
			}
		}
	}
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzODgzMTM0MTgsMTM4MjY4OTExLC01OT
EwNDAxOTcsMjA5MDY1MzU4MSwtNTI0MzkwMzg0LDIwNzc5NTU3
NjQsMTM4MDMwMDY4NF19
-->