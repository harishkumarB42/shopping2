# Sri Vogue — Full-stack JavaScript Storefront

A responsive React + Vite frontend and Express REST API for Sri Vogue. This version uses an editorial cream/burgundy visual system, dedicated Home / Shop / Orders / My Profile pages, product details, image placeholders, wishlist, shopping bag, and backend login/register.

## Requirements
- Node.js 20+ recommended
- npm

## Start locally
```bash
npm install
npm run dev
```
Open `http://localhost:5173`. The API runs at `http://localhost:4000`.

If the default ports are already in use, choose a free API port and point the Vite proxy to it (PowerShell):
```powershell
$env:PORT='4003'; $env:API_PORT='4003'; npm run dev
```
Vite automatically selects the next available frontend port.

## Separate page components
- `src/pages/HomePage.jsx` — homepage and collection tiles
- `src/pages/ShopPage.jsx` — product grid, search, audience/category filters and sorting
- `src/pages/ProductDetail.jsx` — individual product view, size and quantity selection, wishlist and add-to-bag
- `src/pages/OrdersPage.jsx` — order history and refresh
- `src/pages/ProfilePage.jsx` — profile, account information, orders and wishlist shortcuts
- `src/pages/AuthPage.jsx` — login and registration
- `src/App.jsx` — navigation, shared state, API requests and cart drawer
- `src/styles.css` — responsive styling
- `server/index.js` — Express backend and API routes
- `src/products.js` — editable product catalogue

## Add your own product images
The catalogue deliberately has blank image fields so you can add your own real product photos rather than seeing repeated demo images.
1. Copy each image into `public/images/products/`.
2. Open `src/products.js` and set the matching product's `image` field, e.g. `"image": "/images/products/kanjivaram-silk-saree.jpg"`.
3. For collection artwork, add files under `public/images/collections/`; for the homepage campaign, use `public/images/hero.jpg`; for editorial use `public/images/editorial/brand-story.jpg`.
4. The frontend automatically displays the image when the product `image` field is set; otherwise, it shows a designed placeholder. No component changes are required when you add the image path.

## Categories
The Unisex category and Unisex catalogue records have been removed. The available audience filters are All, Women, Men and Accessories.

## API endpoints
- `GET /api/health`
- `GET /api/products`
- `GET /api/products/:id`
- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/me`
- `GET /api/cart`, `PUT /api/cart` (authenticated)
- `POST /api/orders`, `GET /api/orders` (authenticated)
- Admin endpoints are available in `server/index.js` for catalogue analytics and management.

## Important
This is a development starter. Orders are recorded without payment collection. For a public launch, configure a strong `JWT_SECRET`, create an administrator using `/api/admin/bootstrap` with environment variables, add production-grade database storage, HTTPS, rate limiting and a real payment provider. Local JSON files are not appropriate for a high-traffic production store.

## AI Stylist (demo feature)
- Open **AI Stylist** from the main navigation.
- Upload a style inspiration photo (JPG/PNG/WEBP, up to 8 MB), choose an occasion and style mood, then select **Find My Look**.
- The photo preview and basic colour cue are processed locally in the browser; the photo is not uploaded to the API.
- Recommendations are generated from catalogue metadata and the selected occasion/mood/colour. This is a frontend demo, not a connected generative-AI vision service.

## Order storage
Orders are saved by the Express API in `server/data/orders.json` and are associated with the signed-in account. A customer must register/sign in before checkout. Checkout is a project demo and does not collect payment. The included JSON-file storage is suitable for a local academic demo, not production deployment.

## Run the project
```bash
npm install
npm run dev
```
Open `http://localhost:5173`. Keep the server terminal running; it serves the API on port `4000`.
