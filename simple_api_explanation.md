# How APIs Work - Simple Explanation

## What is an API?

**API = Application Programming Interface**

Think of an API like a **waiter in a restaurant**:
- You (the website) tell the waiter what you want
- The waiter goes to the kitchen (database) 
- The waiter brings back your food (data)

## Why Not Talk to Database Directly?

**Bad idea:** Website → Database directly
**Good idea:** Website → Server → Database

### Real Life Example: ATM Machine

Imagine if you could walk directly into a bank vault and take money:
- **Problems**: Anyone could steal money, no security checks, chaos!

Instead, you use an ATM machine:
- **ATM checks your card and PIN** (like server checking permissions)
- **ATM talks to bank safely** (like server talking to database)
- **You get your money safely** (like getting your data back)

### Why use a server?
- **Security**: Database passwords stay hidden on the server (like bank vault keys stay with the bank)
- **Safety**: Server checks if requests are valid before touching database (like ATM checking your PIN)
- **Control**: Server decides who can do what (like ATM limiting how much you can withdraw)
- **Multiple users**: Many websites can use the same server safely (like many people using the same ATM)

## The Journey of Data

```
1. HTML page → 2. Fetch request → 3. Server → 4. Database
                                     ↓
8. HTML shows result ← 7. Fetch gets response ← 6. Server ← 5. Database responds
```

## HTTP Methods (CRUD)

### POST = Create New Thing
```javascript
// "Hey server, make a new movie for me!"
fetch("http://localhost:3000/movies", {
    method: "POST",
    body: JSON.stringify({ title: "New Movie" })
})
```
**What happens:** Server adds new movie to database

### PUT = Update Existing Thing  
```javascript
// "Hey server, change movie #5 for me!"
fetch("http://localhost:3000/movies/5", {
    method: "PUT", 
    body: JSON.stringify({ title: "Updated Movie" })
})
```
**What happens:** Server finds movie #5 and updates it

### DELETE = Remove Thing
```javascript
// "Hey server, delete movie #3 for me!"
fetch("http://localhost:3000/movies/3", {
    method: "DELETE"
})
```
**What happens:** Server removes movie #3 from database

### GET = Read/Fetch Thing
```javascript
// "Hey server, show me all movies!"
fetch("http://localhost:3000/movies")
```
**What happens:** Server gets all movies from database and sends them back

## Real Life Example

Imagine ordering food on an app:

1. **You tap "Order Pizza"** (HTML button click)
2. **App sends request to restaurant** (fetch to server)
3. **Restaurant checks if pizza available** (server checks database)
4. **Kitchen makes pizza** (server processes request)
5. **Restaurant confirms order** (server sends response)
6. **App shows "Order confirmed!"** (HTML shows result)

You don't call the kitchen directly - you go through the restaurant system!

## Key Points

- **HTML/JavaScript**: The face of your app (what users see)
- **Fetch**: The messenger (carries requests back and forth)  
- **Server**: The middleman (handles requests safely)
- **Database**: The storage room (keeps all the data)

**Simple rule:** 
- POST = Add new
- GET = Show me  
- PUT = Change existing
- DELETE = Remove

Each method tells the server exactly what you want to do!