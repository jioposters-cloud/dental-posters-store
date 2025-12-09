# Bulk Upload Guide for Status Ring Store

## Overview
The Status Ring Store uses a **CSV file** (`_data/products.csv`) to manage all product listings. This means you can manage up to 1500+ products with a single spreadsheet - no manual coding required!

## Step 1: Prepare Your Product Data

### Required Columns in Your Spreadsheet
Create a spreadsheet with these columns:

| Column | Description | Example | Required |
|--------|-------------|---------|----------|
| `id` | Unique product ID (number) | 1, 2, 3 | ✓ Yes |
| `name` | Product name | "Dental Poster" | ✓ Yes |
| `category` | Product category | "Dental Artwork Posters" | ✓ Yes |
| `main_image` | Main product image URL | "https://example.com/image.jpg" | ✓ Yes |
| `image1` | Additional image URL | "https://example.com/image2.jpg" | Optional |
| `image2` | Additional image URL | "https://example.com/image3.jpg" | Optional |
| `image3` | Additional image URL | "https://example.com/image4.jpg" | Optional |
| `description` | Product description (0-100 chars for UI) | "Professional dental poster" | ✓ Yes |
| `price` | Price in rupees (number only) | 599, 1299, 99 | ✓ Yes |
| `stock` | Stock quantity | 50, 100, 500 | Optional |

### Sample Data Format

```csv
id,name,category,main_image,image1,image2,image3,description,price,stock
1,Tooth Anatomy Poster,Dental Artwork Posters,https://via.placeholder.com/400,https://via.placeholder.com/400,https://via.placeholder.com/400,https://via.placeholder.com/400,Professional dental anatomy poster showing tooth structure and layers,599,50
2,Oral Hygiene Steps,Dental Patient Education Posters,https://via.placeholder.com/400,https://via.placeholder.com/400,https://via.placeholder.com/400,https://via.placeholder.com/400,Step-by-step guide to proper oral hygiene for patient education,499,100
3,Skin Care Basics,Skin Posters,https://via.placeholder.com/400,https://via.placeholder.com/400,https://via.placeholder.com/400,https://via.placeholder.com/400,Comprehensive skin care routine poster,399,75
```

## Step 2: Upload CSV to GitHub

### Option A: Upload via GitHub Web Interface (Easiest)

1. Navigate to: `_data/products.csv` in your repo
2. Click the **Edit (pencil icon)** button
3. Delete all content and paste your CSV data
4. Scroll to bottom and click **Commit changes**
5. Add commit message: "Update product catalog"
6. Click **Commit changes** button
7. Wait 2-3 minutes for GitHub Pages to rebuild

### Option B: Using Git Command Line

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/dental-posters-store.git
cd dental-posters-store

# Replace the CSV file
cp ~/Downloads/products.csv _data/products.csv

# Commit and push
git add _data/products.csv
git commit -m "Update product catalog with new items"
git push origin main
```

## Step 3: Verify Your Upload

1. Go to: https://jioposters-cloud.github.io/dental-posters-store/
2. Refresh the page (press Ctrl+Shift+R for hard refresh)
3. Check if your products appear
4. Test category filters
5. Test search functionality
6. Test sorting options

## Image Management

### Where to Host Images

**Option 1: Use Placeholder (For Testing)**
```
https://via.placeholder.com/400
```

**Option 2: GitHub Repository (Free)**
1. Create `images/` folder in your repo
2. Upload images via GitHub web interface
3. Use raw URL: `https://raw.githubusercontent.com/jioposters-cloud/dental-posters-store/main/images/photo.jpg`

**Option 3: Cloudinary (Free with Limits)**
1. Sign up at https://cloudinary.com
2. Upload images to your account
3. Copy the public URL

**Option 4: Imgur (Free, No Account Needed)**
1. Visit https://imgur.com
2. Drag and drop your image
3. Copy the image URL

### Image URL Format
Must start with `http://` or `https://`

```
✓ https://example.com/product.jpg
✓ https://via.placeholder.com/400
✓ https://imgur.com/abcdef.jpg
✗ /images/product.jpg (Won't work!)
✗ product.jpg (Won't work!)
```

## Troubleshooting

### Products Not Showing
1. **Check for CSV errors**: Make sure no commas are in product names
   - Bad: `Dental Poster, 5x10 inches`
   - Good: `Dental Poster (5x10 inches)`

2. **Verify all required fields**: `id`, `name`, `category`, `main_image`, `description`, `price`

3. **Check image URLs**: Test URLs in a browser - they must be publicly accessible

4. **Hard refresh**: Press Ctrl+Shift+R (Windows/Linux) or Cmd+Shift+R (Mac)

5. **Check GitHub Pages status**: Go to Settings > Pages to see build status

### Search Not Working
- Products are searched by `name` and `description`
- Make sure these fields contain text
- Search is case-insensitive

### Categories Not Showing
- Categories are auto-generated from the `category` column
- Make sure spelling is consistent
- Avoid leading/trailing spaces

## CSV File Size Limits

- **Maximum rows**: 1000+ products (no hard limit)
- **File size**: Keep under 10 MB
- **Columns**: Add as many as you want (only listed columns are used)

## Advanced: Custom Categories

Edit `index.html` to customize category display or add featured products:

```javascript
// Around line 50, modify populateCategories function
const categories = [...new Set(allProducts.map(p => p.category))];
populateCategories(['all', ...categories]);
```

## Snipcart Integration

Products are automatically integrated with Snipcart cart:

```html
<button class="snipcart-add-item"
  data-item-id="product-1"
  data-item-name="Product Name"
  data-item-price="599"
  data-item-image="image-url"
  data-item-url="store-url">Add to Cart</button>
```

## Best Practices

1. **Use consistent categories**: Avoid typos
   - ✓ "Dental Artwork Posters"
   - ✗ "Dental artwork posters", "Dental Posters"

2. **Keep IDs unique**: Use sequential numbers (1, 2, 3...)

3. **Write good descriptions**: First 100 characters show in grid

4. **Optimize images**: 
   - Use JPG for photos (smaller file size)
   - Use PNG for graphics (transparent background)
   - Keep dimensions around 400x400px

5. **Backup your CSV**: Keep a local copy on your computer

## Example: Full Spreadsheet with 100 Products

### Using Google Sheets
1. Create new Google Sheet
2. Add headers: id, name, category, main_image, description, price
3. Add 100 rows of data
4. File > Download > CSV
5. Upload to GitHub

### Using Excel
1. Create new workbook
2. Add headers and data
3. Save As > Format: CSV UTF-8
4. Upload to GitHub

## Quick Reference

**File to edit**: `_data/products.csv`

**Store frontend**: `index.html`

**Styling**: `assets/css/style.css`

**Live store**: https://jioposters-cloud.github.io/dental-posters-store/

## Features Included

✓ Real-time search across product names and descriptions
✓ Category filtering with dynamic population
✓ Sorting (price low-to-high, price high-to-low, newest)
✓ Pagination (12 items per page)
✓ Responsive design (mobile, tablet, desktop)
✓ Snipcart cart integration
✓ Beautiful product cards with hover effects
✓ Category badges on products

## Support

For issues:
1. Check the troubleshooting section above
2. Verify your CSV format
3. Clear browser cache and hard refresh
4. Check GitHub Actions for build errors

---

**Last Updated**: December 2025
**Store Version**: 2.0 with UI/UX Improvements
