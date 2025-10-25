# Ìròrùn Technical Documentation

**Version:** 1.0  
**Last Updated:** October 25, 2025  
**Platform:** Web Application (Single Page Application)

---

## Table of Contents

1. [Overview](#overview)
2. [Architecture](#architecture)
3. [Technology Stack](#technology-stack)
4. [Features & Components](#features--components)
5. [Data Structures](#data-structures)
6. [User Flows](#user-flows)
7. [Styling System](#styling-system)
8. [State Management](#state-management)
9. [Deployment](#deployment)
10. [Future Enhancements](#future-enhancements)

---

## Overview

**Ìròrùn** (meaning "Ease" in Yoruba) is a local business discovery platform designed specifically for Ogbomoso, connecting customers with trusted local businesses and products. The platform serves two primary user types: **customers** seeking local products/services and **businesses** wanting to increase their visibility.

### Project Goals

- Enable easy discovery of local businesses in Ogbomoso
- Provide businesses with a simple platform to showcase products
- Build trust through reviews and ratings
- Facilitate seamless product browsing and checkout experiences

### Target Audience

- **Customers:** Local residents seeking products and services
- **Business Owners:** Small to medium-sized businesses in Ogbomoso

---

## Architecture

### Application Type

**Single Page Application (SPA)** built with React (via CDN) in a single HTML file.

### Architecture Pattern

- **Component-Based Architecture:** Modular React components for each view
- **Client-Side Routing:** View management through state (`currentView`)
- **Stateful Management:** React hooks (`useState`) for state management
- **Mock Data Layer:** In-memory data structures simulating backend

### File Structure

```
index.html (Single file containing):
├── HTML Structure
├── CSS Styles (embedded <style>)
├── JavaScript/React Code (embedded <script type="text/babel">)
│   ├── Mock Data
│   ├── Components
│   ├── Pages
│   └── Main App Component
```

---

## Technology Stack

### Frontend Framework

- **React 18** (via CDN)
  - `react.production.min.js` - Core React library
  - `react-dom.production.min.js` - React DOM rendering
  
### Transpiler

- **Babel Standalone** - JSX transformation in browser

### Styling

- **Tailwind CSS** (via CDN) - Utility-first CSS framework
- **Custom CSS** - Additional styling for animations, gradients, and custom components
- **Google Fonts** - Inter font family

### Browser APIs

- JavaScript ES6+ features
- Window print API (for invoice printing)

---

## Features & Components

### Core Features

1. **Business Discovery**
   - Browse local businesses by category
   - Search functionality
   - Distance-based sorting
   - Rating and review system

2. **User Management**
   - User signup/login
   - User profiles
   - Business registration
   - Guest browsing

3. **Product Management**
   - Product listings per business
   - Product detail pages
   - Favorites/Wishlist system
   - Product images and pricing

4. **E-commerce Flow**
   - Favorites cart
   - Checkout system
   - Multiple payment methods (Card/Bank Transfer)
   - Invoice generation

5. **Business Dashboard**
   - Product management
   - Review management
   - Business profile editing
   - Analytics overview

### Component Breakdown

#### Navigation Component
```javascript
Navigation({ currentView, setCurrentView, userType, setUserType, favorites })
```
- Responsive navigation bar
- Dynamic menu based on user type (guest/user/business)
- Favorites badge counter
- Mobile hamburger menu

#### Landing Page
```javascript
LandingPage({ setCurrentView, setSelectedBusiness })
```
- Hero section with CTAs
- Featured businesses grid
- "How It Works" section
- Footer with links

#### User Dashboard
```javascript
UserDashboard({ setCurrentView, setSelectedBusiness })
```
- Welcome banner
- Search bar
- Category filters
- Business cards grid

#### Business Detail Page
```javascript
BusinessDetailPage({ business, setCurrentView, setSelectedProduct })
```
- Business hero banner
- Tabbed interface (About, Products, Reviews)
- Product showcase
- Review display and submission

#### Product Detail Page
```javascript
ProductDetailPage({ product, setCurrentView, addToFavorites })
```
- Product image and details
- Pricing information
- Add to Favorites button
- Contact seller CTA

#### Favorites Page
```javascript
FavoritesPage({ favorites, removeFromFavorites, setCurrentView })
```
- Favorites list with product cards
- Order summary sidebar
- Remove from favorites functionality
- Checkout button

#### Checkout Page
```javascript
CheckoutPage({ favorites, setCurrentView })
```
- Contact information form
- Delivery address input
- Payment method selection (Card/Bank Transfer)
- Card payment form
- Bank transfer details with timer warning
- Order summary

#### Invoice Page
```javascript
InvoicePage({ favorites, setCurrentView })
```
- Success confirmation
- Invoice number and date
- Itemized order details
- Payment breakdown (Subtotal, Delivery, Total)
- Print invoice button
- Continue shopping CTA

#### Business Dashboard
```javascript
BusinessDashboard({ setCurrentView })
```
- Sidebar navigation
- Overview statistics
- Product management
- Review management
- Profile editing

#### User Profile
```javascript
UserProfilePage({ setCurrentView })
```
- Profile photo
- Personal information form
- Review history
- Favorite businesses

#### Authentication Pages
```javascript
SignUpPage({ setCurrentView, setUserType })
LoginPage({ setCurrentView, setUserType })
BusinessRegisterPage({ setCurrentView, setUserType })
```
- Form validation
- User type switching
- Quick guest access

---

## Data Structures

### Business Object

```javascript
{
  id: Number,
  name: String,
  category: String,
  rating: Number (0-5),
  reviews: Number,
  distance: String,
  image: String (URL),
  description: String,
  address: String,
  products: Array<Product>
}
```

### Product Object

```javascript
{
  id: Number,
  name: String,
  price: String (formatted with ₦),
  image: String (URL)
}
```

### Review Object

```javascript
{
  id: Number,
  user: String,
  avatar: String (initials),
  rating: Number (0-5),
  comment: String,
  date: String
}
```

### Mock Data

**4 Businesses:**
1. Mama Risi's Kitchen (Restaurant)
2. TechHub Electronics (Electronics)
3. Fashion Forward Boutique (Fashion)
4. Fresh Farms Grocery (Grocery)

**8 Products** (2 per business)

**3 Reviews** (sample reviews)

---

## User Flows

### Customer Journey

```
Landing Page
    ↓
Sign Up / Login (or continue as guest)
    ↓
User Dashboard (Browse & Search)
    ↓
Business Detail Page
    ↓
Product Detail Page
    ↓
Add to Favorites
    ↓
Favorites Page
    ↓
Checkout (Enter details, Select payment)
    ↓
Invoice Page (Success)
```

### Business Journey

```
Landing Page
    ↓
Register Business
    ↓
Business Dashboard
    ↓
Manage Products / Reviews / Profile
```

### View States

The application uses a state-based routing system with the following views:

- `landing` - Landing page
- `signup` - User signup
- `login` - User login
- `user-dashboard` - Main user dashboard
- `business-detail` - Individual business page
- `product-detail` - Individual product page
- `favorites` - Favorites/cart page
- `checkout` - Checkout form
- `invoice` - Payment confirmation and invoice
- `user-profile` - User profile page
- `business-register` - Business registration
- `business-dashboard` - Business management dashboard
- `explore` - Browse businesses (same as user-dashboard)
- `about` - About Ìròrùn page

---

## Styling System

### Color Palette

**Primary Colors:**
- Orange: `#fb923c` to `#f97316` (gradients)
- Blue: `#3b82f6` to `#2563eb` (gradients)
- Green: `#10b981` (accents)

**Neutral Colors:**
- White: `#ffffff`
- Gray shades: `#f8f9fa`, `#f3f4f6`, `#6b7280`, `#1f2937`

### Gradient Backgrounds

```css
.gradient-bg {
  background: linear-gradient(135deg, #f8f9fa 0%, #fff5f0 100%);
}

.btn-primary {
  background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
}

.btn-secondary {
  background: linear-gradient(135deg, #fb923c 0%, #f97316 100%);
}
```

### Typography

- **Font Family:** Inter (Google Fonts)
- **Font Weights:** 300, 400, 500, 600, 700
- **Hero Text:** Responsive clamp sizing `clamp(2rem, 5vw, 3.5rem)`

### Animations

- **Card Hover:** `translateY(-4px)` with shadow enhancement
- **Button Hover:** `scale(1.02)` with shadow glow
- **Transitions:** `0.3s ease-in-out` for smooth interactions

### Responsive Design

- **Mobile First:** Grid layouts adapt to screen size
- **Breakpoints:**
  - Mobile: Default
  - Tablet: `md:` (768px+)
  - Desktop: `lg:` (1024px+)

---

## State Management

### Global State (App Component)

```javascript
const [currentView, setCurrentView] = useState('landing');
const [userType, setUserType] = useState('guest'); // 'guest' | 'user' | 'business'
const [selectedBusiness, setSelectedBusiness] = useState(mockBusinesses[0]);
const [selectedProduct, setSelectedProduct] = useState(null);
const [favorites, setFavorites] = useState([...]); // Pre-populated for testing
```

### State Flow

- **View Navigation:** `setCurrentView(viewName)` changes the active page
- **User Authentication:** `setUserType(type)` switches user role
- **Data Selection:** `setSelectedBusiness` and `setSelectedProduct` pass data between views
- **Favorites Management:** `addToFavorites` and `removeFromFavorites` modify cart

### Local State (Component Level)

Each component maintains its own local state:
- Form inputs (`formData`)
- UI toggles (`isMenuOpen`, `activeTab`, `sidebarOpen`)
- Filters (`selectedCategory`, `searchQuery`)

---

## Deployment

### Single File Deployment

The entire application is contained in one `index.html` file, making deployment simple:

1. **Static Hosting:**
   - Upload `index.html` to any static host
   - Compatible with: Netlify, Vercel, GitHub Pages, AWS S3, etc.

2. **CDN Dependencies:**
   - React 18 (unpkg.com)
   - Tailwind CSS (cdn.tailwindcss.com)
   - Babel Standalone (unpkg.com)
   - Google Fonts

### Production Considerations

**Current Limitations (Development Mode):**
- All CDN libraries loaded from external sources
- No build optimization
- No code splitting
- Mock data only (no backend)

**Recommended Production Setup:**
- Bundle React and dependencies locally
- Implement backend API
- Add database for persistence
- Use production build of React
- Implement proper authentication
- Add error boundaries
- Implement analytics

---

## Future Enhancements

### Short-term (Phase 2)

1. **Backend Integration**
   - REST API or GraphQL backend
   - Database (PostgreSQL/MongoDB)
   - User authentication (JWT)
   - File upload for images

2. **Payment Integration**
   - Paystack API integration
   - Flutterwave API integration
   - Real payment processing

3. **Real-time Features**
   - Order tracking
   - Push notifications
   - Live chat with businesses

4. **Enhanced Search**
   - Advanced filtering
   - Map integration
   - Geolocation services

### Medium-term (Phase 3)

1. **Mobile App**
   - React Native version
   - iOS and Android apps
   - Push notifications

2. **Advanced Analytics**
   - Business insights dashboard
   - Customer behavior tracking
   - Sales reports

3. **Marketing Features**
   - Email marketing integration
   - SMS notifications
   - Promotional campaigns

### Long-term (Phase 4)

1. **Platform Expansion**
   - Multi-city support
   - Franchise management
   - White-label solution

2. **AI/ML Features**
   - Personalized recommendations
   - Fraud detection
   - Chatbot support

3. **Ecosystem Development**
   - Delivery partner integration
   - Loyalty programs
   - Referral system

---

## API Endpoints (Future Backend)

### Authentication
```
POST /api/auth/signup
POST /api/auth/login
POST /api/auth/logout
GET  /api/auth/me
```

### Businesses
```
GET    /api/businesses
GET    /api/businesses/:id
POST   /api/businesses (auth required)
PUT    /api/businesses/:id (auth required)
DELETE /api/businesses/:id (auth required)
```

### Products
```
GET    /api/products
GET    /api/products/:id
POST   /api/products (auth required)
PUT    /api/products/:id (auth required)
DELETE /api/products/:id (auth required)
```

### Reviews
```
GET    /api/reviews/:businessId
POST   /api/reviews/:businessId (auth required)
PUT    /api/reviews/:id (auth required)
DELETE /api/reviews/:id (auth required)
```

### Orders
```
GET    /api/orders (auth required)
GET    /api/orders/:id (auth required)
POST   /api/orders (auth required)
PUT    /api/orders/:id (auth required)
```

### Payments
```
POST   /api/payments/initiate (auth required)
POST   /api/payments/verify (auth required)
GET    /api/payments/:orderId (auth required)
```

### Favorites
```
GET    /api/favorites (auth required)
POST   /api/favorites (auth required)
DELETE /api/favorites/:productId (auth required)
```

---

## Development Setup

### Prerequisites

- Modern web browser (Chrome, Firefox, Safari, Edge)
- Text editor (VS Code, Sublime Text, etc.)
- Basic knowledge of HTML, CSS, JavaScript, and React

### Running Locally

1. Save the `index.html` file
2. Open in a web browser
3. All dependencies load from CDN automatically

### Testing

**Manual Testing Checklist:**

- [ ] Navigation between all views
- [ ] User signup/login flow
- [ ] Business registration flow
- [ ] Product browsing and filtering
- [ ] Add/remove favorites
- [ ] Checkout process (both payment methods)
- [ ] Invoice generation
- [ ] Business dashboard features
- [ ] Mobile responsiveness
- [ ] Cross-browser compatibility

---

## Known Issues & Limitations

1. **No Persistence:** Data resets on page reload
2. **Mock Authentication:** No real user validation
3. **No Backend:** All data is static/mock
4. **No Real Payments:** Payment flows are simulated
5. **Limited Error Handling:** Basic validation only
6. **Single File:** Can become difficult to maintain as it grows
7. **CDN Dependencies:** Requires internet connection
8. **No SEO:** Single page app without SSR

---

## Security Considerations (Future Implementation)

1. **Authentication:** Implement JWT or session-based auth
2. **Data Validation:** Server-side validation for all inputs
3. **SQL Injection:** Use parameterized queries
4. **XSS Protection:** Sanitize user inputs
5. **CSRF Protection:** Implement CSRF tokens
6. **Rate Limiting:** Prevent API abuse
7. **HTTPS:** Enforce secure connections
8. **Payment Security:** PCI DSS compliance

---

## Performance Optimization (Future)

1. **Code Splitting:** Break into smaller chunks
2. **Lazy Loading:** Load images on scroll
3. **Caching:** Implement service workers
4. **Minification:** Minify CSS/JS
5. **CDN:** Serve static assets from CDN
6. **Database Indexing:** Optimize queries
7. **Image Optimization:** Compress and resize images

---

## Contributing Guidelines (Future)

1. Fork the repository
2. Create a feature branch
3. Write clean, documented code
4. Test thoroughly
5. Submit pull request with description

---

## License

**Proprietary** - All rights reserved to Ìròrùn platform owners.

---

## Contact & Support

- **Email:** info@irorun.com
- **Location:** Ogbomoso, Oyo State, Nigeria
- **Website:** (To be deployed)

---

## Changelog

### Version 1.0 (October 25, 2025)
- Initial release
- Core business discovery features
- User and business dashboards
- Favorites and checkout system
- Invoice generation
- Responsive design
- Mock data implementation

---

**End of Documentation**
