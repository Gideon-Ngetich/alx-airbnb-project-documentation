# Airbnb Clone – Backend Feature Specifications

## 📌 Objective

This document outlines the **technical** and **functional** specifications for each core backend feature of the Airbnb Clone system. It includes descriptions, API endpoints, expected inputs/outputs, validation rules, and performance requirements.

---

## 🧑‍💼 1. User Authentication

### Functional Requirements
- Allow users to register as `guest` or `host`
- Enable login using email and password
- Issue JWT tokens upon successful login
- Support secure password hashing (e.g., bcrypt)

### API Endpoints

#### Register
- `POST /api/auth/register`

```json
Request Body:
{
  "first_name": "John",
  "last_name": "Doe",
  "email": "john@example.com",
  "password": "SecurePassword123",
  "role": "guest"
}

Response:
{
  "message": "User registered successfully",
  "token": "jwt_token"
}
```

#### Login
- `POST /api/auth/login`

```json
Request Body:
{
  "email": "john@example.com",
  "password": "SecurePassword123"
}

Response:
{
  "token": "jwt_token",
  "user": {
    "id": "uuid",
    "role": "guest"
  }
}
```

### Validation Rules
- Email must be valid and unique
- Password must be at least 8 characters
- Role must be either `guest` or `host`

---

## 🏡 2. Property Management

### Functional Requirements
- Hosts can create, update, and delete property listings
- Properties must include title, description, location, price, and availability

### API Endpoints

#### Create Property
- `POST /api/properties`

```json
Request Body:
{
  "name": "Beach House",
  "description": "Oceanfront with 2 bedrooms",
  "location": "Mombasa",
  "pricepernight": 150.00
}

Response:
{
  "message": "Property created successfully",
  "property_id": "uuid"
}
```

#### Get All Properties
- `GET /api/properties`

#### Update Property
- `PUT /api/properties/:id`

#### Delete Property
- `DELETE /api/properties/:id`

### Validation Rules
- `name`, `description`, `location`, and `pricepernight` must be provided
- Price must be a positive decimal

---

## 📅 3. Booking System

### Functional Requirements
- Guests can book available properties for specific date ranges
- Prevent double bookings
- Allow booking status changes (pending, confirmed, canceled)

### API Endpoints

#### Create Booking
- `POST /api/bookings`

```json
Request Body:
{
  "property_id": "uuid",
  "start_date": "2025-07-15",
  "end_date": "2025-07-18"
}

Response:
{
  "booking_id": "uuid",
  "status": "pending",
  "total_price": 450.00
}
```

#### Cancel Booking
- `PATCH /api/bookings/:id/cancel`

#### Get Bookings for a User
- `GET /api/bookings/user/:userId`

### Validation Rules
- Start date must be before end date
- Property must be available for selected dates
- User must be authenticated

---

## 💳 4. Payment Processing

### Functional Requirements
- Guests can pay using credit card, PayPal, or Stripe
- Store payment record linked to a booking

### API Endpoints

#### Process Payment
- `POST /api/payments`

```json
Request Body:
{
  "booking_id": "uuid",
  "payment_method": "stripe",
  "amount": 450.00
}

Response:
{
  "message": "Payment successful",
  "payment_id": "uuid"
}
```

### Validation Rules
- Amount must match the booking total
- Payment method must be one of: `credit_card`, `paypal`, `stripe`

---

## 🌟 5. Reviews and Ratings

### Functional Requirements
- Guests can leave reviews after completing a stay
- Hosts can respond to reviews

### API Endpoints

#### Leave Review
- `POST /api/reviews`

```json
Request Body:
{
  "property_id": "uuid",
  "rating": 5,
  "comment": "Amazing location and service!"
}

Response:
{
  "message": "Review submitted"
}
```

#### Get Reviews for Property
- `GET /api/reviews/property/:id`

### Validation Rules
- Rating must be between 1 and 5
- Comment must be non-empty
- User must be authenticated

---

## 📬 6. Notification System

### Functional Requirements
- Email and/or in-app notifications for:
  - Booking confirmations
  - Booking cancellations
  - Payment receipts

### Implementation Notes
- Use a service like **SendGrid** or **Mailgun**
- Queue background jobs with **BullMQ**, **RabbitMQ**, or similar

---

## ⚙️ Performance Criteria

| Feature             | Performance Requirement                      |
|---------------------|-----------------------------------------------|
| User Registration   | Response in under 500ms                      |
| Search Listings     | Return first 20 results within 1s            |
| Create Booking      | Prevent race conditions; complete in 800ms   |
| Payment Processing  | Secure + < 2s gateway response               |
| API Response Format | JSON, with HTTP status codes (200, 201, etc) |

---

## ✅ Security & Validation Summary

- Passwords hashed using bcrypt
- JWT-based authentication for all protected routes
- Role-based access (Guest, Host, Admin)
- Input validation using Joi, Zod, or custom middleware
- Rate limiting on auth and payment routes