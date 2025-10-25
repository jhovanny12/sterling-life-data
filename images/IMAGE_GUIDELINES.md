# Image Organization Guidelines

## Directory Structure

```
images/
├── events/           # Event images
│   ├── karaoke.jpg
│   ├── trivia.jpg
│   ├── comedy.jpg
│   └── ...
├── food-trucks/      # Food truck images
│   ├── burger-bus.jpg
│   ├── taco-express.jpg
│   └── ...
├── businesses/       # Business logos and images
│   ├── brewery-logo.png
│   ├── coffee-house-logo.png
│   └── ...
└── amenities/        # Community amenity images
    ├── pool.jpg
    ├── gym.jpg
    └── ...
```

## Naming Conventions

### General Rules

1. **Use lowercase**: All filenames should be lowercase
2. **Use hyphens**: Separate words with hyphens (kebab-case)
3. **Be descriptive**: Filename should describe the content
4. **Keep it short**: Aim for 2-3 words maximum
5. **Include version**: For logos/templates, include version number if needed

### Examples

**Good:**
- `karaoke-night.jpg`
- `burger-bus.jpg`
- `brewery-logo-v2.png`
- `pool-party.jpg`

**Bad:**
- `IMG_1234.jpg` (not descriptive)
- `Karaoke Night.jpg` (spaces and capitals)
- `karaoke_night_at_sterling_ranch_brewery.jpg` (too long)
- `kn.jpg` (too short/unclear)

## File Formats

### Events
- **Format**: JPG or WebP
- **Dimensions**: 1200x800px (3:2 aspect ratio)
- **File size**: < 500KB
- **Quality**: 85% JPEG quality

### Food Trucks
- **Format**: JPG or WebP
- **Dimensions**: 800x800px (1:1 aspect ratio)
- **File size**: < 300KB
- **Quality**: 85% JPEG quality

### Business Logos
- **Format**: PNG (with transparency) or SVG
- **Dimensions**: 400x400px minimum
- **File size**: < 100KB
- **Background**: Transparent preferred

### Amenities
- **Format**: JPG or WebP
- **Dimensions**: 1600x900px (16:9 aspect ratio)
- **File size**: < 800KB
- **Quality**: 90% JPEG quality

## Image Optimization

### Recommended Tools

1. **ImageOptim** (Mac): https://imageoptim.com/
2. **TinyPNG** (Web): https://tinypng.com/
3. **Squoosh** (Web): https://squoosh.app/
4. **ImageMagick** (CLI): For batch processing

### CLI Example (ImageMagick)

```bash
# Resize and optimize an event image
convert input.jpg -resize 1200x800^ -gravity center -extent 1200x800 -quality 85 output.jpg

# Resize and optimize a logo
convert logo.png -resize 400x400 -background none -gravity center -extent 400x400 optimized-logo.png

# Batch process all JPGs in a directory
for img in *.jpg; do
  convert "$img" -resize 1200x800^ -gravity center -extent 1200x800 -quality 85 "optimized-$img"
done
```

### WebP Conversion

```bash
# Convert JPG to WebP
cwebp -q 85 input.jpg -o output.webp

# Batch convert all JPGs to WebP
for img in *.jpg; do
  cwebp -q 85 "$img" -o "${img%.jpg}.webp"
done
```

## Cloudinary Integration

Sterling Life uses Cloudinary for image hosting and transformation. Here's how to integrate:

### Setup

1. Sign up for Cloudinary: https://cloudinary.com/
2. Get your Cloud Name, API Key, and API Secret
3. Upload images to appropriate folders

**⚠️ Security Warning:** Never commit your Cloudinary API Secret to version control. Use environment variables or secure credential storage. Add `.env` files containing credentials to your `.gitignore`.

### Folder Structure in Cloudinary

```
sterling-ranch/
├── events/
├── food-trucks/
├── businesses/
└── amenities/
```

### Upload Script (Node.js)

```javascript
const cloudinary = require('cloudinary').v2;

cloudinary.config({
  cloud_name: 'your-cloud-name',
  api_key: 'your-api-key',
  api_secret: 'your-api-secret'
});

// Upload an event image
cloudinary.uploader.upload('images/events/karaoke.jpg', {
  folder: 'sterling-ranch/events',
  public_id: 'karaoke',
  overwrite: true,
  resource_type: 'image'
}, (error, result) => {
  console.log(result.secure_url);
});
```

### Upload Script (Python)

```python
import cloudinary
import cloudinary.uploader

cloudinary.config(
  cloud_name = "your-cloud-name",
  api_key = "your-api-key",
  api_secret = "your-api-secret"
)

# Upload an event image
result = cloudinary.uploader.upload(
  "images/events/karaoke.jpg",
  folder="sterling-ranch/events",
  public_id="karaoke",
  overwrite=True
)

print(result['secure_url'])
```

### URL Transformations

Cloudinary allows dynamic image transformations via URL parameters:

```
# Original
https://res.cloudinary.com/your-cloud/image/upload/sterling-ranch/events/karaoke.jpg

# Resized to 400x300
https://res.cloudinary.com/your-cloud/image/upload/w_400,h_300,c_fill/sterling-ranch/events/karaoke.jpg

# Optimized WebP
https://res.cloudinary.com/your-cloud/image/upload/f_auto,q_auto/sterling-ranch/events/karaoke.jpg

# Rounded corners
https://res.cloudinary.com/your-cloud/image/upload/r_20/sterling-ranch/events/karaoke.jpg

# Apply filter
https://res.cloudinary.com/your-cloud/image/upload/e_grayscale/sterling-ranch/events/karaoke.jpg
```

### Common Transformations

```javascript
// In Swift/iOS
let baseUrl = "https://res.cloudinary.com/your-cloud/image/upload"
let transformations = "w_800,h_600,c_fill,f_auto,q_auto"
let imagePath = "sterling-ranch/events/karaoke.jpg"
let finalUrl = "\(baseUrl)/\(transformations)/\(imagePath)"

// For thumbnails
let thumbnailUrl = "\(baseUrl)/w_200,h_200,c_fill,f_auto,q_auto/\(imagePath)"

// For retina displays
let retinaUrl = "\(baseUrl)/w_1600,h_1200,c_fill,f_auto,q_auto,dpr_2.0/\(imagePath)"
```

## Image Templates

The enrichment.json file contains image template mappings for consistent image usage:

```json
{
  "imageTemplates": {
    "karaoke": {
      "template": "karaoke-night",
      "cloudinaryId": "sterling-ranch/events/karaoke",
      "fallbackColor": "#FF6B6B"
    }
  }
}
```

### Using Templates in iOS

```swift
struct ImageLoader {
    let cloudinaryBase = "https://res.cloudinary.com/your-cloud/image/upload"
    
    func getImageUrl(template: String, size: ImageSize) -> URL? {
        guard let enrichmentData = loadEnrichmentData(),
              let imageTemplate = enrichmentData.imageTemplates[template] else {
            return nil
        }
        
        let transformation = size.cloudinaryTransformation
        let path = imageTemplate.cloudinaryId
        let urlString = "\(cloudinaryBase)/\(transformation)/\(path).jpg"
        
        return URL(string: urlString)
    }
    
    func getFallbackColor(template: String) -> UIColor? {
        guard let enrichmentData = loadEnrichmentData(),
              let imageTemplate = enrichmentData.imageTemplates[template],
              let colorHex = imageTemplate.fallbackColor else {
            return nil
        }
        
        return UIColor(hex: colorHex)
    }
}

enum ImageSize {
    case thumbnail  // 200x200
    case medium     // 800x600
    case large      // 1200x800
    
    var cloudinaryTransformation: String {
        switch self {
        case .thumbnail:
            return "w_200,h_200,c_fill,f_auto,q_auto"
        case .medium:
            return "w_800,h_600,c_fill,f_auto,q_auto"
        case .large:
            return "w_1200,h_800,c_fill,f_auto,q_auto"
        }
    }
}
```

## Best Practices

1. **Always optimize images** before committing to the repository
2. **Use descriptive filenames** that match your JSON references
3. **Maintain aspect ratios** appropriate for the content type
4. **Include alt text** in your app for accessibility
5. **Use WebP format** when browser/app support allows
6. **Implement lazy loading** for better performance
7. **Cache images locally** to reduce bandwidth usage
8. **Use Cloudinary transformations** instead of storing multiple sizes
9. **Test images on different screen sizes** before deployment
10. **Keep original high-res images** in a separate backup location

## Accessibility

When implementing images in your app, always include descriptive alt text:

```swift
// Good
Image(url: imageUrl)
    .accessibilityLabel("Karaoke night at Sterling Ranch Brewery")

// Bad
Image(url: imageUrl)
    .accessibilityLabel("Image")
```

## License and Attribution

- Ensure you have rights to all images
- Include photographer attribution when required
- Follow Creative Commons licenses if applicable
- Document image sources in a separate CREDITS.md file

## Questions?

For image-related questions or issues, please open an issue in the repository.
