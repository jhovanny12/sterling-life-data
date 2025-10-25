# Sterling Ranch Community Data

A JSON data repository for the Sterling Ranch community app, providing centralized access to community events, food truck schedules, and local business information.

## 📋 Contents

This repository contains the following data files:

- **events.json** - Community events and activities with tags, dates, and categories
- **food-trucks.json** - Food truck schedules, menus, dietary options, and contact information
- **businesses.json** - Local business directory with hours, social media, and details
- **enrichment.json** - Event categorization, image templates, and community amenities
- **images/** - Image assets organized by category
- **API.md** - Complete API documentation for iOS app integration

See **[API.md](API.md)** for complete API documentation and usage examples.

## 🚀 Quick Start

### Accessing the Data

All JSON files can be accessed directly via GitHub Pages:

```
https://jhovanny12.github.io/sterling-life-data/events.json
https://jhovanny12.github.io/sterling-life-data/food-trucks.json
https://jhovanny12.github.io/sterling-life-data/businesses.json
https://jhovanny12.github.io/sterling-life-data/enrichment.json
```

### Using in Your Application

#### JavaScript/Node.js
```javascript
// Fetch events data
fetch('https://jhovanny12.github.io/sterling-life-data/events.json')
  .then(response => response.json())
  .then(data => console.log(data));
```

#### Python
```python
import requests

# Fetch food trucks data
response = requests.get('https://jhovanny12.github.io/sterling-life-data/food-trucks.json')
data = response.json()
```

#### Swift (iOS)
```swift
let url = URL(string: "https://jhovanny12.github.io/sterling-life-data/businesses.json")!
URLSession.shared.dataTask(with: url) { data, response, error in
    // Handle data
}.resume()
```

## 📦 Data Structure

### Events (events.json)
Each event contains:
- `id` - Unique identifier
- `title` - Event name
- `description` - Event details
- `startDate` - ISO 8601 formatted start date/time (e.g., "2024-11-15T19:00:00Z")
- `endDate` - ISO 8601 formatted end date/time
- `location` - Venue location
- `category` - Event type (entertainment, food, market, family, community, holiday, fitness)
- `isFoodTruck` - Boolean indicating if event features a food truck
- `foodTruckName` - Name of featured food truck (if applicable)
- `externalLink` - URL for more information or registration
- `tags` - Array of tags for filtering (e.g., ["music", "nightlife", "adults"])
- `imageTemplate` - Image template identifier for Cloudinary integration

### Food Trucks (food-trucks.json)
Each food truck contains:
- `id` - Unique identifier
- `name` - Food truck name
- `description` - Business description
- `cuisineType` - Type of cuisine (American, Mexican, Italian, etc.)
- `priceRange` - Price indicator ($ = <$10, $$ = $10-20, $$$ = $20+)
- `specialDietary` - Array of dietary options (vegetarian, vegan, gluten-free, etc.)
- `menuURL` - Link to online menu
- `websiteURL` - Food truck website
- `socialMedia` - Object with Facebook, Instagram, Twitter links

### Businesses (businesses.json)
Each business contains:
- `id` - Unique identifier
- `name` - Business name
- `description` - Business description
- `category` - Business category (Food & Beverage, Healthcare, Fitness, etc.)
- `phoneNumber` - Contact phone number
- `website` - Website URL
- `hours` - Operating hours by day of week
- `logoURL` - Path to business logo
- `socialMedia` - Object with Facebook, Instagram, Twitter links

### Enrichment Data (enrichment.json)
Contains:
- `eventCategories` - Category definitions with colors, icons, and descriptions
- `imageTemplates` - Image template mappings for Cloudinary
- `tagDefinitions` - Tag metadata with icons and categories
- `priceRanges` - Price range definitions
- `dietaryOptions` - Dietary option definitions with icons
- `amenities` - Community amenities (pool, gym, pickleball courts, etc.) with hours and features

## 🖼️ Images

Images are organized in the following structure:
```
images/
├── events/           # Event images
├── food-trucks/      # Food truck images
├── businesses/       # Business logos
└── amenities/        # Community amenity images
```

See **[images/IMAGE_GUIDELINES.md](images/IMAGE_GUIDELINES.md)** for:
- Image naming conventions
- Optimization guidelines
- Cloudinary integration examples
- File format specifications

## 🔄 Contributing

To update the data:

1. Clone the repository:
   ```bash
   git clone https://github.com/jhovanny12/sterling-life-data.git
   cd sterling-life-data
   ```

2. Make your changes to the JSON files

3. Validate your JSON:
   ```bash
   # Using Python
   python -m json.tool events.json > /dev/null && echo "Valid JSON"
   
   # Using Node.js
   node -e "JSON.parse(require('fs').readFileSync('events.json'))" && echo "Valid JSON"
   ```

4. Commit and push your changes:
   ```bash
   git add .
   git commit -m "Update community data"
   git push origin main
   ```

Changes will be automatically available via GitHub Pages within a few minutes.

## 📄 GitHub Pages

This repository uses GitHub Pages to serve JSON data files. The site is available at:

**Base URL:** `https://jhovanny12.github.io/sterling-life-data/`

### Available Endpoints:
- Events: `https://jhovanny12.github.io/sterling-life-data/events.json`
- Food Trucks: `https://jhovanny12.github.io/sterling-life-data/food-trucks.json`
- Businesses: `https://jhovanny12.github.io/sterling-life-data/businesses.json`
- Enrichment: `https://jhovanny12.github.io/sterling-life-data/enrichment.json`

GitHub Pages is already configured and serves data automatically from the `main` branch.

## 🛠️ Development

### Prerequisites
- Git
- Text editor or IDE
- JSON validator (optional)

### Local Setup
```bash
# Clone the repository
git clone https://github.com/jhovanny12/sterling-life-data.git

# Navigate to directory
cd sterling-life-data

# View data files
cat events.json | python -m json.tool
```

### Adding New Events
```json
{
  "id": 13,
  "title": "New Community Event",
  "description": "Detailed event description",
  "startDate": "2024-12-01T18:00:00Z",
  "endDate": "2024-12-01T21:00:00Z",
  "location": "Sterling Ranch Community Park",
  "category": "community",
  "isFoodTruck": false,
  "foodTruckName": null,
  "externalLink": null,
  "tags": ["community", "family-friendly"],
  "imageTemplate": "community-event"
}
```

### Adding New Food Trucks
```json
{
  "id": 8,
  "name": "New Food Truck",
  "description": "Description of the food truck",
  "cuisineType": "Cuisine Type",
  "priceRange": "$$",
  "specialDietary": ["vegetarian-options"],
  "menuURL": "https://example.com/menu",
  "websiteURL": "https://example.com",
  "socialMedia": {
    "facebook": "https://facebook.com/example",
    "instagram": "https://instagram.com/example",
    "twitter": null
  }
}
```

### Adding New Businesses
```json
{
  "id": 13,
  "name": "New Business",
  "description": "Business description",
  "category": "Category",
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
  "logoURL": "images/businesses/new-business-logo.png",
  "socialMedia": {
    "facebook": "https://facebook.com/example",
    "instagram": null,
    "twitter": null
  }
}
```

## 📞 Support

For questions or issues, please open an issue in this repository.

## 📝 License

This data is provided for use with Sterling Ranch community applications.

---

**Last Updated:** November 2024  
**API Version:** 2.0  
**Documentation:** See [API.md](API.md) for complete API documentation
