# Airbnb Clone – Use Case Diagram

## Objective

This document outlines and visualizes the interactions between users and the Airbnb Clone backend system using a **Use Case Diagram**. The goal is to clarify system functionality from the user's perspective and define the key actors and their actions.

---

## Actors

### 1. Guest
A user who signs up to search and book properties for rent.

### 2. Host
A user who lists their properties and manages bookings.

### 3. Admin
A system administrator who manages users, listings, and monitors overall platform activity.

---

## Use Cases

| Use Case | Description |
|----------|-------------|
| **Register Account** | User signs up as a guest or host |
| **Login / Authenticate** | Login with email/password or OAuth |
| **Edit Profile** | Update personal info and upload profile picture |
| **Search Properties** | Guests search for listings by filters |
| **Book Property** | Guests reserve available properties |
| **Cancel Booking** | Guests or hosts cancel confirmed bookings |
| **Make Payment** | Guests pay upfront via Stripe/PayPal |
| **Leave Review** | Guests review completed bookings |
| **Receive Notifications** | Users receive booking/payment notifications |
| **List Property** | Hosts create new listings |
| **Edit/Delete Property** | Hosts manage their own listings |
| **View Bookings (Host)** | Hosts track reservations on their listings |
| **Respond to Reviews** | Hosts can reply to guest reviews |
| **Payout to Host** | Hosts receive payouts after guest stays |
| **Manage Users** | Admin can ban/approve user accounts |
| **Manage Listings** | Admin can moderate properties |
| **Monitor Bookings & Payments** | Admin dashboard for platform metrics |

---