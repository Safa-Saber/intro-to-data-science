# Webshop Development Guide
*Following Your Teacher's Approach*

## Table of Contents
1. [Development Order](#development-order)
2. [Database Structure](#database-structure)
3. [Server Components](#server-components)
4. [Frontend Components](#frontend-components)
5. [Data Flow Explanation](#data-flow-explanation)
6. [File Connections](#file-connections)
7. [Adapting to Books Domain](#adapting-to-books-domain)

---

## Development Order

### Phase 1: Database First
**Why first?** Everything depends on data structure - server needs tables to query, frontend needs data to display.

1. **Create database schema** (`database/setup.sql`)
2. **Design table relationships**
3. **Insert sample data**
4. **Test in TablePlus/MySQL**

### Phase 2: Server Development
**Why second?** Frontend needs API endpoints to fetch data from database.

1. **Setup Node.js project** (`server/package.json`)
2. **Create main server file** (`server/index.js`)
3. **Test API endpoints** (Postman or browser)
4. **Verify database connections**

### Phase 3: Frontend Development
**Why last?** Can now fetch real data from working server.

1. **Create HTML structure** (all .html files)
2. **Add JavaScript functionality** (`website/js/app.js`)
3. **Style with CSS** (`website/css/styles.css`)
4. **Test complete user flow**

---

## Database Structure

### Core Tables

#### Primary Tables (No Dependencies)
```sql
categories (category_id, name, description)
manufacturers (manufacturer_id, name)  
customers (customer_id, name, email, address, city, postal_code, country, phone)
```

#### Secondary Tables (Have Foreign Keys)
```sql
products (product_id, manufacturer_id, name, description, price, image_url, stock_quantity, isFeatured, isDeleted)
cart (cart_id, customer_id)
orders (order_id, customer_id, order_date, total_amount)
```

#### Junction Tables (Many-to-Many Relationships)
```sql
product_categories (product_id, category_id)
cart_items (cart_item_id, cart_id, product_id, quantity)
order_items (order_item_id, order_id, product_id, quantity, price)
```

### Key Relationships
- **Products ↔ Categories**: Many-to-many (one product can be in multiple categories)
- **Products → Manufacturers**: Many-to-one (many products from one manufacturer)
- **Customers → Orders**: One-to-many (one customer can have many orders)
- **Orders → Products**: Many-to-many through order_items
- **Customers → Cart**: One-to-one (each customer has one cart)

---

## Server Components

### File: `server/package.json`
**Purpose**: Defines project dependencies and scripts
```json
{
  "dependencies": {
    "express": "Web server framework",
    "mysql2": "Database connection",
    "cors": "Cross-origin requests"
  }
}
```

### File: `server/index.js`
**Purpose**: Main server application following your teacher's patterns

#### Database Connection (Top of file)
```javascript
const mysql = require("mysql2/promise");
const db = mysql.createPool({
  // Connection details - MUST match your MySQL setup
});
```

#### API Endpoints (Following teacher's REST pattern)

**Homepage Route** - `GET /`
- Fetches featured products grouped by categories
- Similar to your movie project's "2 movies per genre" approach
- Returns JSON data for homepage display

**Product Routes**
- `GET /api/products` - All products
- `GET /api/products/:id` - Single product details
- Uses SQL JOINs to get manufacturer info and categories

**Category Routes**  
- `GET /api/categories` - All categories (for navigation)
- `GET /api/categories/:id/products` - Products by category

**Cart Routes** (New compared to movie project)
- `POST /api/cart` - Add product to cart
- `GET /api/cart` - View cart contents  
- `PUT /api/cart` - Update quantities
- `DELETE /api/cart/:productId` - Remove items

**Order Routes**
- `POST /api/checkout` - Create order from cart
- `GET /api/orders/:id` - View order details

---

## Frontend Components

### HTML Files Structure

#### `website/index.html` - Homepage
**Purpose**: Main landing page showing featured products by category
**Key Elements**:
- Navigation with category links
- Hero section with welcome message
- Container for dynamic product sections
- Calls `getFeaturedProductsPerCategoryAndDisplay()`

#### `website/category.html` - Category Page
**Purpose**: Shows all products in selected category
**Key Elements**:
- Same navigation structure
- Container for product grid
- Gets category_id from URL parameters
- Calls `fetchAndDisplayProductsByCategory()`

#### `website/product.html` - Product Details
**Purpose**: Detailed view of single product
**Key Elements**:
- Product image, description, price
- Add to cart functionality
- Stock availability check
- Gets product_id from URL parameters
- Calls `fetchAndDisplayProductDetails()`

#### `website/cart.html` - Shopping Cart
**Purpose**: View and manage cart contents
**Key Elements**:
- Email input to load customer's cart
- Cart items with quantity controls
- Total calculation
- Checkout button
- Calls `loadCartForEmail()`

#### `website/checkout.html` - Checkout Form
**Purpose**: Collect shipping info and create order
**Key Elements**:
- Customer information form
- Order summary
- Form validation
- Calls `processCheckout()`

#### `website/thankyou.html` - Order Confirmation
**Purpose**: Show completed order details
**Key Elements**:
- Thank you message
- Order summary
- Order ID for reference
- Gets order_id from URL parameters
- Calls `fetchAndDisplayOrderDetails()`

### JavaScript File: `website/js/app.js`

#### Core Functions (Following Teacher's Patterns)

**Data Fetching Functions** (using fetch with .then chains)
```javascript
function getFeaturedProductsPerCategoryAndDisplay() {
  // Fetches from server root "/"
  // Builds HTML with template literals
  // Updates DOM with innerHTML
}

function fetchAndDisplayProductsByCategory() {
  // Gets category_id from URL
  // Fetches from "/api/categories/{id}/products"
  // Creates product cards dynamically
}
```

**Cart Management Functions** (New functionality)
```javascript
function addToCart(productId) {
  // POST request to add items
  // Manages customer email
  // Updates cart count
}

function updateCartItemQuantity(productId, newQuantity) {
  // PUT request to modify quantities
  // Handles stock limits
}
```

**Navigation Functions** (Run on every page)
```javascript
function fetchAndDisplayCategories() {
  // Loads category menu
  // Runs automatically when app.js loads
  // Similar to your movie project's genre loading
}
```

### CSS File: `website/css/styles.css`

#### Key Styling Concepts
- **Grid Layout**: For product cards (like your movie cards)
- **Flexbox Navigation**: Horizontal menu layout
- **Responsive Design**: Mobile-friendly breakpoints
- **Card Components**: Consistent product/cart item styling
- **Form Styling**: Professional checkout forms

---

## Data Flow Explanation

### Homepage Flow
1. **Page loads** → `index.html`
2. **Script runs** → `getFeaturedProductsPerCategoryAndDisplay()`
3. **Server request** → `GET /` 
4. **Database query** → Featured products per category
5. **Response** → JSON data with products grouped by categories
6. **DOM update** → Template literals create HTML cards
7. **Display** → Products appear on page

### Product Detail Flow
1. **User clicks** → "View Details" link with `?product_id=123`
2. **Page loads** → `product.html`
3. **Script runs** → `fetchAndDisplayProductDetails()`
4. **URL parsing** → Extract product_id parameter
5. **Server request** → `GET /api/products/123`
6. **Database query** → JOIN products, manufacturers, categories
7. **Response** → Single product with full details
8. **DOM update** → Create detailed product display

### Cart Flow
1. **Add to cart** → User clicks "Add to Cart" button
2. **Email check** → Prompt for email if not provided
3. **Server request** → `POST /api/cart` with email, product_id, quantity
4. **Database operations** → Find/create customer, cart, add item
5. **Response** → Success message
6. **UI update** → Cart count increases

### Checkout Flow
1. **Form submission** → Customer fills shipping info
2. **Data validation** → Check required fields
3. **Server request** → `POST /api/checkout` with form data
4. **Database transactions** → Create order, order items, clear cart, update stock
5. **Response** → Order ID
6. **Redirect** → Thank you page with order details

---

## File Connections

### How Files Work Together

```
DATABASE (MySQL)
    ↑
    | SQL queries
    ↓
SERVER (index.js)
    ↑
    | HTTP requests (fetch)
    ↓
JAVASCRIPT (app.js)
    ↑
    | DOM manipulation
    ↓
HTML FILES (index.html, etc.)
    ↑
    | CSS classes
    ↓
STYLES (styles.css)
```

### Key Connection Points

**Server ↔ Database**
- Connection pool established at server startup
- Each API endpoint makes specific SQL queries
- Results returned as JSON

**Frontend ↔ Server**  
- JavaScript makes fetch() requests to API endpoints
- Server responds with JSON data
- No direct database access from frontend

**HTML ↔ JavaScript**
- HTML provides containers with specific IDs
- JavaScript finds elements with getElementById()
- Content added using innerHTML and template literals

**JavaScript ↔ CSS**
- JavaScript adds CSS classes dynamically
- CSS provides styling for all visual elements
- Responsive design handles different screen sizes

---

## Adapting to Books Domain

### Database Changes
Replace electronics tables with book-focused ones:

```sql
-- Instead of manufacturers → publishers
publishers (publisher_id, name, founded_year, country)

-- Instead of products → books  
books (book_id, publisher_id, title, author, isbn, description, price, cover_image_url, stock_quantity, isFeatured, isDeleted, publication_year, page_count)

-- Instead of categories → genres
genres (genre_id, name, description)

-- Junction table
book_genres (book_id, genre_id)
```

### Sample Data Changes
```sql
-- Publishers
INSERT INTO publishers (name) VALUES ('Penguin Random House'), ('HarperCollins'), ('Macmillan');

-- Genres  
INSERT INTO genres (name, description) VALUES 
('Fiction', 'Novels and short stories'),
('Non-Fiction', 'Biography, history, science'),
('Mystery', 'Crime and detective stories');

-- Books
INSERT INTO books (publisher_id, title, author, price, description) VALUES
(1, 'The Great Gatsby', 'F. Scott Fitzgerald', 12.99, 'Classic American novel'),
(2, 'To Kill a Mockingbird', 'Harper Lee', 14.99, 'Coming-of-age story');
```

### Frontend Text Changes
- "Electronics" → "Books"
- "Manufacturer" → "Publisher"  
- "Products" → "Books"
- "Categories" → "Genres"
- "TechZone" → "BookHaven"

### Server Code Changes
Minimal - just update column names in SQL queries:
```javascript
// Change
p.manufacturer_id, m.name AS manufacturer_name
// To  
p.publisher_id, pub.name AS publisher_name
```

---

## Key Teaching Concepts Used

### Your Teacher's Patterns
1. **Separation of Concerns**: Database, Server, Frontend in separate files
2. **Template Literals**: Building HTML strings with `${variable}` 
3. **Fetch with .then()**: No async/await, stick to promise chains
4. **innerHTML Updates**: Direct DOM manipulation, no frameworks
5. **URL Parameters**: Navigation using query strings
6. **Express REST API**: Standard HTTP methods for different operations
7. **MySQL with Promises**: mysql2/promise for database operations

### Development Approach
- **Start with data structure** (database first)
- **Build API endpoints** (server second)  
- **Create user interface** (frontend last)
- **Test each component** before moving to next
- **Keep code readable** with meaningful function names

This guide provides the complete understanding you need for your video demonstration and project adaptation.
