# Sterling Ranch Community Data

A JSON data repository for the Sterling Ranch community app, providing centralized access to community events, food truck schedules, and local business information.

## 📋 Contents

This repository contains the following data files:

- **events.json** - Community events and activities
- **food-trucks.json** - Food truck schedules, menus, and contact information
- **businesses.json** - Local business directory with hours and details
- **images/** - Image assets organized by category

## 🚀 Quick Start

### Accessing the Data

All JSON files can be accessed directly via raw GitHub URLs:

```
https://raw.githubusercontent.com/jhovanny12/sterling-life-data/main/events.json
https://raw.githubusercontent.com/jhovanny12/sterling-life-data/main/food-trucks.json
https://raw.githubusercontent.com/jhovanny12/sterling-life-data/main/businesses.json
```

### Using in Your Application

#### JavaScript/Node.js
```javascript
// Fetch events data
fetch('https://raw.githubusercontent.com/jhovanny12/sterling-life-data/main/events.json')
  .then(response => response.json())
  .then(data => console.log(data));
```

#### Python
```python
import requests

# Fetch food trucks data
response = requests.get('https://raw.githubusercontent.com/jhovanny12/sterling-life-data/main/food-trucks.json')
data = response.json()
```

#### Swift (iOS)
```swift
let url = URL(string: "https://raw.githubusercontent.com/jhovanny12/sterling-life-data/main/businesses.json")!
URLSession.shared.dataTask(with: url) { data, response, error in
    // Handle data
}.resume()
```

## 📦 Data Structure

### Events (events.json)
Each event contains:
- `id` - Unique identifier
- `title` - Event name
- `date` - Event date (YYYY-MM-DD)
- `time` - Start time (HH:MM)
- `location` - Venue location
- `description` - Event details
- `category` - Event type (entertainment, market, family, community, holiday, fitness)
- `image` - Image path
- `organizer` - Organizing entity
- `registrationRequired` - Boolean flag

### Food Trucks (food-trucks.json)
Each food truck contains:
- `id` - Unique identifier
- `name` - Food truck name
- `cuisine` - Type of cuisine
- `description` - Business description
- `schedule` - Array of schedule objects (day, time, location)
- `menu` - Array of menu items with prices
- `contact` - Contact information (phone, email, website)
- `image` - Image path
- `rating` - Customer rating

### Businesses (businesses.json)
Each business contains:
- `id` - Unique identifier
- `name` - Business name
- `category` - Business category
- `description` - Business description
- `address` - Physical address
- `phone` - Contact phone number
- `email` - Contact email
- `website` - Website URL
- `hours` - Operating hours by day
- `image` - Image path
- `rating` - Customer rating
- `featured` - Boolean flag for featured businesses

## 🖼️ Images

Images are organized in the following structure:
```
images/
├── events/
├── food-trucks/
└── businesses/
```

Upload images to the appropriate directory and reference them in the JSON files using relative paths.

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

## 📄 GitHub Pages

This repository is configured with GitHub Pages. Visit the GitHub Pages site to view formatted documentation.

To enable GitHub Pages:
1. Go to repository Settings
2. Navigate to Pages section
3. Select source branch (main)
4. Save

The site will be available at: `https://jhovanny12.github.io/sterling-life-data/`

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
  "id": 9,
  "title": "New Event",
  "date": "2024-12-01",
  "time": "10:00",
  "location": "Sterling Ranch Community Park",
  "description": "Event description",
  "category": "community",
  "image": "images/events/new-event.jpg",
  "organizer": "Sterling Ranch HOA",
  "registrationRequired": false
}
```

### Adding New Food Trucks
```json
{
  "id": 6,
  "name": "New Food Truck",
  "cuisine": "Type",
  "description": "Description",
  "schedule": [
    {
      "day": "Monday",
      "time": "11:00-14:00",
      "location": "Sterling Ranch Town Center"
    }
  ],
  "menu": [],
  "contact": {
    "phone": "303-555-0000",
    "email": "info@example.com",
    "website": "https://example.com"
  },
  "image": "images/food-trucks/new-truck.jpg",
  "rating": 4.5
}
```

### Adding New Businesses
```json
{
  "id": 11,
  "name": "New Business",
  "category": "Category",
  "description": "Description",
  "address": "Address",
  "phone": "303-555-0000",
  "email": "info@example.com",
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
  "image": "images/businesses/new-business.jpg",
  "rating": 4.5,
  "featured": false
}
```

## 📞 Support

For questions or issues, please open an issue in this repository.

## 📝 License

This data is provided for use with Sterling Ranch community applications.

---

**Last Updated:** October 2024
