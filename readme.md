# E-Commerce Project

## Description

This is a full-stack e-commerce application built using the MERN stack (MongoDB, Express.js, React, Node.js) with additional integration of MySQL for relational data management. The application allows users to browse products, manage their cart, place orders, and make payments via Stripe. It includes an admin panel for managing products, categories, and orders. The backend uses MongoDB for product-related data and MySQL for user accounts, orders, and addresses.

## Tech Stack

### Frontend
- **React**: JavaScript library for building user interfaces
- **Vite**: Fast build tool and development server
- **Redux Toolkit**: State management
- **Tailwind CSS**: Utility-first CSS framework
- **Axios**: HTTP client for API requests
- **React Router DOM**: Routing for React applications
- **Stripe.js**: Payment processing
- **React Hot Toast**: Notification library
- **React Infinite Scroll Component**: Infinite scrolling for lists
- **React Icons**: Icon library

### Backend
- **Node.js**: JavaScript runtime
- **Express.js**: Web application framework
- **MongoDB**: NoSQL database for products, categories, and subcategories
- **MySQL**: Relational database for users, orders, carts, and addresses
- **Mongoose**: ODM for MongoDB
- **Sequelize**: ORM for MySQL
- **JWT**: JSON Web Tokens for authentication
- **bcryptjs**: Password hashing
- **Multer**: File upload handling
- **Cloudinary**: Image hosting and management
- **Resend**: Email service
- **Stripe**: Payment gateway
- **Morgan**: HTTP request logger
- **Helmet**: Security middleware
- **CORS**: Cross-origin resource sharing

## Features

### User Features
- User registration and login with email verification
- Password reset via OTP
- Profile management (update details, upload avatar)
- Product browsing with search and filtering
- Shopping cart management
- Address management for delivery
- Order placement and tracking
- Secure payment processing with Stripe
- Responsive design for mobile and desktop

### Admin Features
- Product management (add, edit, delete products)
- Category and subcategory management
- Order management and status updates
- User management
- Dashboard for analytics

### General Features
- Image upload and hosting via Cloudinary
- Email notifications for verification and password reset
- JWT-based authentication with refresh tokens
- Role-based access control (Admin/User)
- Text search on products (name and description)
- Pagination and infinite scrolling

## Prerequisites

Before running this application, make sure you have the following installed:

- Node.js (version 16 or higher)
- npm or yarn
- MySQL server
- MongoDB server
- Git

You will also need accounts for:
- Cloudinary (for image uploads)
- Resend (for email sending)
- Stripe (for payment processing)

## Installation

### Clone the Repository

```bash
git clone <repository-url>
cd E_commerce_Project
```

### Backend Setup

1. Navigate to the server directory:
   ```bash
   cd server
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the server directory with the following variables:
   ```
   PORT=8082
   FRONTEND_URL=http://localhost:5173
   MONGODB_URI=mongodb://localhost:27017/ecommerce
   MYSQL_HOST=localhost
   MYSQL_USER=your_mysql_username
   MYSQL_PASSWORD=your_mysql_password
   MYSQL_DATABASE=ecommerce
   SECRET_KEY_ACCESS_TOKEN=your_access_token_secret
   SECRET_KEY_REFRESH_TOKEN=your_refresh_token_secret
   CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
   CLOUDINARY_API_KEY=your_cloudinary_api_key
   CLOUDINARY_API_SECRET=your_cloudinary_api_secret
   RESEND_API_KEY=your_resend_api_key
   STRIPE_SECRET_KEY=your_stripe_secret_key
   ```

4. Ensure MySQL and MongoDB servers are running.

5. Start the server:
   ```bash
   npm run dev
   ```

### Frontend Setup

1. Navigate to the client directory:
   ```bash
   cd ../client
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file in the client directory with the following variables:
   ```
   VITE_API_URL=http://localhost:8082/api
   VITE_STRIPE_PUBLISHABLE_KEY=your_stripe_publishable_key
   ```

4. Start the development server:
   ```bash
   npm run dev
   ```

The application will be available at `http://localhost:5173`.

## Usage

1. Register a new user account or login with existing credentials.
2. Browse products by category or use the search functionality.
3. Add products to your cart.
4. Proceed to checkout, add delivery address, and complete payment.
5. View your orders in the profile section.
6. For admin access, login with an admin account and access the dashboard.

## API Documentation

### Authentication
- `POST /api/user/register` - Register a new user
- `POST /api/user/login` - Login user
- `POST /api/user/logout` - Logout user
- `POST /api/user/verify-email` - Verify email
- `POST /api/user/forgot-password` - Request password reset
- `POST /api/user/verify-forgot-password-otp` - Verify OTP for password reset
- `POST /api/user/reset-password` - Reset password
- `GET /api/user/details` - Get user details
- `PUT /api/user/update-details` - Update user details
- `POST /api/user/upload-avatar` - Upload user avatar

### Products
- `GET /api/product` - Get all products (with pagination and search)
- `GET /api/product/:id` - Get product by ID
- `POST /api/product` - Create new product (Admin only)
- `PUT /api/product/:id` - Update product (Admin only)
- `DELETE /api/product/:id` - Delete product (Admin only)

### Categories
- `GET /api/category` - Get all categories
- `POST /api/category` - Create new category (Admin only)
- `PUT /api/category/:id` - Update category (Admin only)
- `DELETE /api/category/:id` - Delete category (Admin only)

### Cart
- `GET /api/cart` - Get user's cart
- `POST /api/cart` - Add item to cart
- `PUT /api/cart/:id` - Update cart item
- `DELETE /api/cart/:id` - Remove item from cart

### Orders
- `GET /api/order` - Get user's orders
- `POST /api/order` - Create new order
- `PUT /api/order/:id` - Update order status (Admin only)

### Addresses
- `GET /api/address` - Get user's addresses
- `POST /api/address` - Add new address
- `PUT /api/address/:id` - Update address
- `DELETE /api/address/:id` - Delete address

### File Upload
- `POST /api/file/upload` - Upload image file

## Database Schema

### MySQL Tables

#### User
- id (Primary Key)
- name
- email (Unique)
- password (Hashed)
- avatar
- mobile
- refresh_token
- verify_email
- last_login_date
- status (Active/Inactive/Suspended)
- forgot_password_otp
- forgot_password_expiry
- role (ADMIN/USER)
- createdAt, updatedAt

#### CartProduct
- id (Primary Key)
- userId (Foreign Key to User)
- productId
- quantity
- createdAt, updatedAt

#### Order
- id (Primary Key)
- userId (Foreign Key to User)
- products (JSON)
- totalAmount
- status
- paymentStatus
- paymentIntentId
- deliveryAddress (JSON)
- createdAt, updatedAt

#### Address
- id (Primary Key)
- userId (Foreign Key to User)
- address_line
- city
- state
- pincode
- country
- mobile
- status (Active/Inactive)
- createdAt, updatedAt

### MongoDB Collections

#### Product
- _id (ObjectId)
- name
- image (Array)
- category (Array of ObjectIds referencing Category)
- subCategory (Array of ObjectIds referencing SubCategory)
- unit
- stock
- price
- discount
- description
- more_details (Object)
- publish (Boolean)
- createdAt, updatedAt

#### Category
- _id (ObjectId)
- name
- image
- createdAt, updatedAt

#### SubCategory
- _id (ObjectId)
- name
- image
- category (Array of ObjectIds referencing Category)
- createdAt, updatedAt

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the ISC License.
