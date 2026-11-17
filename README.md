# QueueLess – Online Queue Booking System

**Course:** Electronic Business Development (BINF 503) · Winter 2026
**Instructor:** Dr. Nourhan Hamdi
**Teaching Assistants:** Mr. Nour Gaser, Mr. Omar Alaa, Ms. Mariam Khalid, Mr. Younes Zied, Mr. Mahmoud Hani

## 1. Team


| Name | Student ID | Tutorial group | GitHub username |
|---|---|---|---|
| YARA Mohamed | 16001381 | T9 | yaraelmansoury444-cmyk |
| Mohamed Waleed | 16003272 | T6 | mkhairyprivate-bot |
| Maya Ismail | 16002499 | T9 | mayaismail349-blip |
| Mohamed Amr | 16005398 | T2 | mohamedamrr519 |
| Hazem Ahmed | 16001349 | T4 | hazemfadel12123-droid |

## 2. The idea
QueueLess is an online queue booking system that allows customers to reserve their place in a queue at businesses such as clinics, barber shops, restaurants, and service centers. Customers can book a queue position online, view their queue number, and track their booking status without waiting physically. Business owners can manage their business profiles, organize customer bookings, and update the queue as customers are served. The application aims to reduce waiting time and make queue management easier for both customers and businesses.

## 3. Features

### 3.1 The full product

- User registration and login with customer and business owner roles.
- Business owners can create, view, update, and delete their business profiles.
- Customers can browse and search for available businesses.
- Customers can book a queue position at a selected business.
- Customers can view their queue number and current booking status.
- Customers can update or cancel their bookings.
- Business owners can view and manage customer bookings.
- Business owners can update queue statuses and call the next customer.
- Customers can view estimated waiting times.
- Businesses can manage their opening hours and services.
- Users can view their booking history.

### 3.2 The use cases we will build

| # | Use case | What the user does | What they see | What is stored |
|---|---|---|---|---|
| 1 | Registration and login | Registers with name, email and password; logs in with email and password | Their home page, with their name in the header | A User, with the password hashed |
| 2 | Business management | Creates, views, updates or deletes their business profile | Their business profile and confirmation of saved changes | Business details and the owner's user ID |
| 3 | Queue booking | Selects a business and books a queue position | Booking confirmation, queue number and booking status | Customer ID, business ID, queue number and booking status |
| 4 | Booking management | Views, updates or cancels their bookings | Their booking details and updated booking status | Updated booking information or cancelled status |
| 5 | Queue management | Views the queue, updates booking statuses and calls the next customer | Current queue and updated customer statuses | Updated booking statuses and queue information |


## 4. Who owns what

| Member | Use case |
|---|---|
| Hazem Ahmed | 1. Registration and login |
| Yara Mohamed | 2. Business Management |
| Mohamed Waleed | 3. Queue booking |
| Mohamed Amr | 4. Booking management |
| Maya Ismail | 5. Queue management |

## 5. Data model

### User

```js
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true }, // stored hashed, never as plain text
  role: {
  type: String,
  enum: ["customer", "businessOwner"],
  default: "customer"
}
});
```
### Business

```js
const businessSchema = new mongoose.Schema({
  name: { type: String, required: true },
  category: { type: String, required: true },
  description: { type: String },
  location: { type: String, required: true },
  openingHours: { type: String },
  owner: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "User",
    required: true
  }
}, { timestamps: true });
```
### Booking
```js
const bookingSchema = new mongoose.Schema({
  customer: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "User",
    required: true
  },
  business: {
    type: mongoose.Schema.Types.ObjectId,
    ref: "Business",
    required: true
  },
  queueNumber: { type: Number, required: true },
  bookingDate: { type: Date, default: Date.now },
  status: {
    type: String,
    enum: ["waiting", "serving", "completed", "cancelled"],
    default: "waiting"
  },
  estimatedWaitingTime: { type: Number, default: 0 }
}, { timestamps: true });
```
## 6. Run it locally

> Leave this section as it is until Submission 2 (Thursday 10 December 2026,
> 23:59). Then fill it in: we follow these steps to run your project.

### Back end

```bash
cd backend
npm install
# create backend/.env from backend/.env.example (see the table below)
npm start
```

The API runs on http://localhost:3000.

| Variable in `.env` | What it is |
|---|---|
| `MONGODB_URI` | The connection string of your MongoDB Atlas database |
| `JWT_SECRET` | Any long random text, used to sign login tokens |
| [Any other variable] | [What it is] |

### Front end

```bash
cd frontend
npm install
npm run dev
```

The app runs on [the address `npm run dev` prints, e.g. http://localhost:5173].
