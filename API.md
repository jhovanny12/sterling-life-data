# Sterling Life API Documentation

## Overview

The Sterling Life API provides access to community events, food trucks, local businesses, and enrichment data for the Sterling Ranch community. All data is served as static JSON files via GitHub Pages.

## Base URL

```
https://jhovanny12.github.io/sterling-life-data/
```

## Endpoints

### Events

Get all community events and activities.

**Endpoint:** `GET /events.json`

**Response Structure:**
```json
[
  {
    "id": 1,
    "title": "Event Name",
    "description": "Event description",
    "startDate": "2024-11-15T19:00:00Z",
    "endDate": "2024-11-15T22:00:00Z",
    "location": "Event location",
    "category": "entertainment|food|market|family|community|holiday|fitness",
    "isFoodTruck": false,
    "foodTruckName": null,
    "externalLink": "https://example.com",
    "tags": ["tag1", "tag2"],
    "imageTemplate": "template-name"
  }
]
```

**Fields:**
- `id` (integer): Unique identifier for the event
- `title` (string): Event name
- `description` (string): Detailed event description
- `startDate` (string): ISO 8601 formatted start date/time
- `endDate` (string): ISO 8601 formatted end date/time
- `location` (string): Event venue or location
- `category` (string): Event category
- `isFoodTruck` (boolean): Whether this is a food truck event
- `foodTruckName` (string|null): Name of featured food truck if applicable
- `externalLink` (string|null): External URL for more information
- `tags` (array): Array of tag strings for filtering
- `imageTemplate` (string): Image template identifier

**Example Request:**
```bash
curl https://jhovanny12.github.io/sterling-life-data/events.json
```

**Example Response:**
```json
[
  {
    "id": 1,
    "title": "Karaoke Night at Sterling Center",
    "description": "Join us for a fun evening of karaoke!",
    "startDate": "2024-11-15T19:00:00Z",
    "endDate": "2024-11-15T22:00:00Z",
    "location": "Sterling Ranch Brewery, Sterling Center",
    "category": "entertainment",
    "isFoodTruck": false,
    "foodTruckName": null,
    "externalLink": "https://sterlingranchbrewery.com/events/karaoke",
    "tags": ["music", "nightlife", "adults", "social"],
    "imageTemplate": "karaoke"
  }
]
```

---

### Food Trucks

Get information about local food trucks including cuisine type, pricing, and dietary options.

**Endpoint:** `GET /food-trucks.json`

**Response Structure:**
```json
[
  {
    "id": 1,
    "name": "Food Truck Name",
    "description": "Food truck description",
    "cuisineType": "American|Mexican|Italian|Asian Fusion|BBQ|Desserts|Healthy",
    "priceRange": "$|$$|$$$",
    "specialDietary": ["vegetarian", "vegan", "gluten-free"],
    "menuURL": "https://example.com/menu",
    "websiteURL": "https://example.com",
    "socialMedia": {
      "facebook": "https://facebook.com/example",
      "instagram": "https://instagram.com/example",
      "twitter": "https://twitter.com/example"
    }
  }
]
```

**Fields:**
- `id` (integer): Unique identifier
- `name` (string): Food truck name
- `description` (string): Business description
- `cuisineType` (string): Type of cuisine offered
- `priceRange` (string): Price range indicator ($ = <$10, $$ = $10-20, $$$ = $20+)
- `specialDietary` (array): Special dietary options available
- `menuURL` (string): Link to menu
- `websiteURL` (string): Food truck website
- `socialMedia` (object): Social media links

**Example Request:**
```bash
curl https://jhovanny12.github.io/sterling-life-data/food-trucks.json
```

**Example Response:**
```json
[
  {
    "id": 1,
    "name": "The Burger Bus",
    "description": "Gourmet burgers and hand-cut fries",
    "cuisineType": "American",
    "priceRange": "$$",
    "specialDietary": ["vegetarian-options"],
    "menuURL": "https://burgerbus.com/menu",
    "websiteURL": "https://burgerbus.com",
    "socialMedia": {
      "facebook": "https://facebook.com/burgerbus",
      "instagram": "https://instagram.com/burgerbus",
      "twitter": "https://twitter.com/burgerbus"
    }
  }
]
```

---

### Businesses

Get information about local Sterling Ranch businesses.

**Endpoint:** `GET /businesses.json`

**Response Structure:**
```json
[
  {
    "id": 1,
    "name": "Business Name",
    "description": "Business description",
    "category": "Food & Beverage|Healthcare|Fitness|Beauty|Pet Services|Grocery|Education|Automotive",
    "phoneNumber": "303-555-0000",
    "website": "https://example.com",
    "hours": {
      "monday": "09:00-17:00",
      "tuesday": "09:00-17:00",
      "wednesday": "09:00-17:00",
      "thursday": "09:00-17:00",
      "friday": "09:00-17:00",
      "saturday": "Closed",
      "sunday": "Closed"
    },
    "logoURL": "images/businesses/logo.png",
    "socialMedia": {
      "facebook": "https://facebook.com/example",
      "instagram": "https://instagram.com/example",
      "twitter": null
    }
  }
]
```

**Fields:**
- `id` (integer): Unique identifier
- `name` (string): Business name
- `description` (string): Business description
- `category` (string): Business category
- `phoneNumber` (string): Contact phone number
- `website` (string): Business website URL
- `hours` (object): Operating hours by day of week
- `logoURL` (string): Path to business logo
- `socialMedia` (object): Social media links

**Example Request:**
```bash
curl https://jhovanny12.github.io/sterling-life-data/businesses.json
```

**Example Response:**
```json
[
  {
    "id": 1,
    "name": "Sterling Ranch Brewery",
    "description": "Local craft brewery serving artisan beers",
    "category": "Food & Beverage",
    "phoneNumber": "303-555-0301",
    "website": "https://sterlingranchbrewery.com",
    "hours": {
      "monday": "15:00-22:00",
      "tuesday": "15:00-22:00",
      "wednesday": "15:00-22:00",
      "thursday": "15:00-23:00",
      "friday": "12:00-00:00",
      "saturday": "12:00-00:00",
      "sunday": "12:00-21:00"
    },
    "logoURL": "images/businesses/brewery-logo.png",
    "socialMedia": {
      "facebook": "https://facebook.com/sterlingranchbrewery",
      "instagram": "https://instagram.com/sterlingranchbrewery",
      "twitter": null
    }
  }
]
```

---

### Enrichment Data

Get enrichment data for event categorization, image templates, tags, and community amenities.

**Endpoint:** `GET /enrichment.json`

**Response Structure:**
```json
{
  "eventCategories": { ... },
  "imageTemplates": { ... },
  "tagDefinitions": { ... },
  "priceRanges": { ... },
  "dietaryOptions": { ... },
  "amenities": [ ... ]
}
```

**Sections:**
- `eventCategories`: Category definitions with colors, icons, and descriptions
- `imageTemplates`: Image template mappings for Cloudinary integration
- `tagDefinitions`: Tag metadata with icons and categories
- `priceRanges`: Price range definitions
- `dietaryOptions`: Dietary option definitions
- `amenities`: Community amenities with hours and features

**Example Request:**
```bash
curl https://jhovanny12.github.io/sterling-life-data/enrichment.json
```

---

## Usage Examples

### Swift (iOS)

```swift
import Foundation

// Fetch events
func fetchEvents() {
    let url = URL(string: "https://jhovanny12.github.io/sterling-life-data/events.json")!
    
    URLSession.shared.dataTask(with: url) { data, response, error in
        guard let data = data, error == nil else {
            print("Error: \(error?.localizedDescription ?? "Unknown error")")
            return
        }
        
        do {
            let events = try JSONDecoder().decode([Event].self, from: data)
            // Process events
        } catch {
            print("Decode error: \(error)")
        }
    }.resume()
}

// Event model
struct Event: Codable {
    let id: Int
    let title: String
    let description: String
    let startDate: Date
    let endDate: Date
    let location: String
    let category: String
    let isFoodTruck: Bool
    let foodTruckName: String?
    let externalLink: String?
    let tags: [String]
    let imageTemplate: String
}
```

### JavaScript

```javascript
// Fetch events
async function fetchEvents() {
    try {
        const response = await fetch('https://jhovanny12.github.io/sterling-life-data/events.json');
        const events = await response.json();
        console.log(events);
    } catch (error) {
        console.error('Error fetching events:', error);
    }
}

// Fetch with filter
async function fetchEventsByCategory(category) {
    const response = await fetch('https://jhovanny12.github.io/sterling-life-data/events.json');
    const events = await response.json();
    return events.filter(event => event.category === category);
}
```

### Python

```python
import requests
from datetime import datetime

# Fetch events
def fetch_events():
    url = 'https://jhovanny12.github.io/sterling-life-data/events.json'
    response = requests.get(url)
    
    if response.status_code == 200:
        events = response.json()
        return events
    else:
        print(f"Error: {response.status_code}")
        return []

# Filter upcoming events
def get_upcoming_events():
    events = fetch_events()
    now = datetime.now().isoformat()
    return [e for e in events if e['startDate'] > now]
```

---

## Error Handling

### HTTP Status Codes

- `200 OK`: Successful request
- `304 Not Modified`: Resource not modified (use cached version)
- `404 Not Found`: Endpoint does not exist
- `500 Internal Server Error`: Server error (GitHub Pages issue)

### Best Practices

1. **Cache responses**: Implement client-side caching to reduce API calls
2. **Handle network errors**: Always implement error handling for network failures
3. **Check data freshness**: Consider implementing cache invalidation strategies
4. **Validate data**: Always validate JSON structure before processing

### Example Error Handling (Swift)

```swift
func fetchData<T: Decodable>(from urlString: String, completion: @escaping (Result<T, Error>) -> Void) {
    guard let url = URL(string: urlString) else {
        completion(.failure(URLError(.badURL)))
        return
    }
    
    URLSession.shared.dataTask(with: url) { data, response, error in
        if let error = error {
            completion(.failure(error))
            return
        }
        
        guard let httpResponse = response as? HTTPURLResponse,
              (200...299).contains(httpResponse.statusCode) else {
            completion(.failure(URLError(.badServerResponse)))
            return
        }
        
        guard let data = data else {
            completion(.failure(URLError(.dataNotAllowed)))
            return
        }
        
        do {
            let decoded = try JSONDecoder().decode(T.self, from: data)
            completion(.success(decoded))
        } catch {
            completion(.failure(error))
        }
    }.resume()
}
```

---

## Rate Limiting

GitHub Pages does not have explicit rate limits, but follow these best practices:

- **Recommended**: Cache data locally for at least 5-10 minutes
- **Maximum frequency**: No more than 1 request per second per endpoint
- **Avoid**: Polling for real-time updates (data is static)

### Caching Strategy

```swift
class DataCache {
    private var cache: [String: (data: Data, timestamp: Date)] = [:]
    private let cacheLifetime: TimeInterval = 600 // 10 minutes
    
    func get(key: String) -> Data? {
        guard let cached = cache[key] else { return nil }
        
        if Date().timeIntervalSince(cached.timestamp) > cacheLifetime {
            cache.removeValue(forKey: key)
            return nil
        }
        
        return cached.data
    }
    
    func set(key: String, data: Data) {
        cache[key] = (data: data, timestamp: Date())
    }
}
```

---

## Data Updates

The data is updated periodically by the repository maintainers. Check the repository's commit history for update frequency:

```
https://github.com/jhovanny12/sterling-life-data/commits/main
```

---

## Support

For questions, issues, or data corrections:
- **GitHub Issues**: https://github.com/jhovanny12/sterling-life-data/issues
- **Repository**: https://github.com/jhovanny12/sterling-life-data

---

## Changelog

### Version 2.0 (November 2024)
- Updated JSON structure for iOS app compatibility
- Added `startDate` and `endDate` fields to events
- Added `isFoodTruck` and `foodTruckName` to events
- Added `tags` and `imageTemplate` to events
- Added `cuisineType`, `priceRange`, and `specialDietary` to food trucks
- Added `phoneNumber`, `logoURL`, and `socialMedia` to businesses
- Created enrichment.json with categorization data
- Added Sterling Ranch specific events and amenities
- Migrated to GitHub Pages URLs

### Version 1.0 (October 2024)
- Initial release with basic event, food truck, and business data
