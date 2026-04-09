# 寒夜録 (Kanya Roku) - Site Handbook

Welcome to your personal digital archive. This handbook provides detailed instructions on how to maintain, update, and customize your website.

## 1. Updating Content (Posts)

All site content is managed in `src/data/blogData.ts`. To add or edit a post, find the `posts` array and add a new object following these formats:

### General Post Format
```typescript
{
  id: 'unique-id',
  title: 'Post Title',
  date: 'YYYY-MM-DD',
  category: 'general',
  tags: ['tag1', 'tag2'],
  excerpt: 'Short summary for the card view.',
  content: 'Full markdown content here...',
  coverImage: 'https://url-to-image.jpg',
}
```

### Photography Post Format
```typescript
{
  id: 'unique-id',
  title: 'Collection Name',
  date: 'YYYY-MM-DD',
  category: 'photography',
  theme: 'Urban/Nature/etc',
  collection: 'Collection Name',
  tags: ['tag1'],
  excerpt: '...',
  content: '...',
  coverImage: '...',
  images: ['img1-url', 'img2-url'],
  showOnMap: true, // Optional
  location: { lat: 0, lng: 0, name: 'Location Name' } // Optional
}
```

### Travel Post Format
```typescript
{
  id: 'unique-id',
  title: 'Trip Name',
  date: 'YYYY-MM-DD',
  category: 'travel',
  duration: '5 days',
  tags: ['tag1'],
  excerpt: '...',
  content: '...',
  coverImage: '...',
  showOnMap: true,
  location: { lat: 0, lng: 0, name: 'City, Country' }
}
```

### Food Post Format (Recipe or Review)
```typescript
{
  id: 'unique-id',
  title: 'Dish Name',
  date: 'YYYY-MM-DD',
  category: 'food',
  foodType: 'recipe', // or 'review'
  cuisine: 'Japanese/French/etc',
  price: '$$', // For reviews
  rating: 4.5, // For reviews
  ingredients: ['item1', 'item2'], // For recipes
  tags: ['tag1'],
  excerpt: '...',
  content: '...',
  coverImage: '...',
  showOnMap: true, // Recommended for reviews
  location: { lat: 0, lng: 0, name: 'Restaurant Name' }
}
```

## 2. Customizing Site Identity

To change the site title, description, or intro, edit the top-level fields in `src/data/blogData.ts`:

- `siteTitle`: Appears in the navigation and welcome page.
- `siteDescription`: Appears under the title on the welcome page.
- `siteIntro`: Appears in the footer.
- `about`: Update your bio, avatar, and social links here.

## 3. Editing Styles & Artistic Expressions

### Floating Illustrations
To add or edit floating illustrations (like the emojis on the welcome page), edit `src/components/WelcomePage.tsx`. Look for the "Collage Elements" section. You can add more `<span>` elements with different emojis and CSS animations.

To make them move, you can use Tailwind's `animate-bounce` or create custom keyframes in `src/index.css`.

### Avant-Garde Styling
The "collage" look is achieved using the `.collage-card` and `.collage-border` classes in `src/index.css`. You can modify these to change the shadow offsets, border styles, or rotation angles.

To add more "personal" touches, consider adding `rotate-[xdeg]` classes to images or cards to give them a "scattered on a desk" feel.

### Quick Filters
Quick filters for Food and Posts are defined in their respective page files (`src/pages/FoodRecipes.tsx`, `src/pages/FoodReviews.tsx`, `src/pages/Posts.tsx`). 

To edit these:
1. Open the page file (e.g., `src/pages/FoodRecipes.tsx`).
2. Find the `Quick Filters` section in the JSX.
3. Update the array of strings (e.g., `['Matcha', 'Dessert', 'Baking']`).
4. The filtering logic uses `setSearch(tag)`, which automatically updates the search input and filters the list.

## 4. Advanced Map Integration

The current map uses `react-simple-maps` for a lightweight, SVG-based interactive experience. If you want to switch to a more detailed map like Google Maps:

### Option A: Google Maps (via `google-map-react`)
1. **Install the library**: `npm install google-map-react`
2. **Get an API Key**: Obtain a key from the Google Cloud Console.
3. **Replace MapFeature**: Create a new component that uses `GoogleMapReact`.
4. **Markers**: Use custom React components as markers on the map.

### Option B: Leaflet (Open Source)
1. **Install**: `npm install react-leaflet leaflet`
2. **Setup**: Leaflet is great for detailed street maps without an API key (using OpenStreetMap tiles).

### Option C: Mapbox
1. **Install**: `npm install react-map-gl mapbox-gl`
2. **Setup**: Offers highly customizable, beautiful vector maps (requires a Mapbox token).

*Note: For most personal blogs, the current SVG map is preferred as it requires no API keys and loads instantly.*

## 5. Local Development

To run the site locally on your computer:

1. **Install Node.js**: Ensure you have Node.js installed.
2. **Open in VS Code**: Open the project folder.
3. **Install Dependencies**: Open the terminal in VS Code and run:
   ```bash
   npm install
   ```
4. **Run Dev Server**: Run the following command to start the local preview:
   ```bash
   npm run dev
   ```
5. **View Results**: Open `http://localhost:3000` in your browser. Any changes you save in VS Code will automatically refresh the page.

## 5. Deployment (GitHub Pages)

To make your website public via GitHub Pages:

1. **Create a GitHub Repository**: Create a new repository on GitHub.
2. **Push Code**: Push your local code to the repository.
3. **Install gh-pages**:
   ```bash
   npm install gh-pages --save-dev
   ```
4. **Update package.json**:
   - Add `"homepage": "https://yourusername.github.io/repository-name"`
   - Add these scripts:
     ```json
     "predeploy": "npm run build",
     "deploy": "gh-pages -d dist"
     ```
5. **Deploy**:
   ```bash
   npm run deploy
   ```
6. **Settings**: In your GitHub repository settings, go to "Pages" and ensure the source is set to the `gh-pages` branch.

---
*Created with stardust.*
