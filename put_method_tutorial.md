# PUT Method Tutorial

## Server Code

Add this PUT endpoint to your server file:

```javascript
const express = require("express");
const cors = require("cors");
const mysql = require("mysql2/promise");

const app = express();
const port = 3000;

app.use(cors());
app.use(express.json()); // Middleware to parse JSON request bodies

// Database configuration
const dbConfig = {
  host: "localhost",
  user: "root",
  password: "your_password", // replace with your password
  database: "test",
};

// PUT method to update an existing movie
app.put("/movies/:id", async (req, res) => {
  const movieId = req.params.id; // Get the movie ID from the URL
  const data = req.body;
  
  try {
    const db = await mysql.createConnection(dbConfig);
    
    const results = await db.query(`
      UPDATE movies SET
        title = '${data.title}',
        release_year = ${data.release_year},
        duration_minutes = ${data.duration_minutes},
        description = '${data.description}',
        director_id = ${data.director_id}
      WHERE id = ${movieId}
    `);

    await db.end();

    res.send({ 
      message: "Movie updated", 
      movieId: movieId
    });
  } catch (error) {
    res.status(500).send({
      message: "Error updating movie",
      error: error.message,
    });
  }
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## HTML Test File

Create an HTML file to test the PUT method:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Test PUT with Fetch</title>
</head>
<body>
    <h1>Update Movie</h1>
    
    <input type="number" id="movieId" placeholder="Movie ID">
    <input type="text" id="title" placeholder="Movie Title">
    <input type="number" id="release_year" placeholder="Release Year">
    
    <button onclick="updateMovie()">Update Movie</button>
    
    <p id="result"></p>

    <script>
        function updateMovie() {
            const movieId = document.getElementById("movieId").value;
            const title = document.getElementById("title").value;
            const release_year = document.getElementById("release_year").value;
            const resultDiv = document.getElementById("result");
            
            if (!movieId || !title || !release_year) {
                alert("Please fill in all fields");
                return;
            }
            
            resultDiv.innerHTML = "Updating movie...";
            
            // Asking the server to update an existing movie
            fetch(`http://localhost:3000/movies/${movieId}`, {
                method: "PUT", // Specifying the PUT method
                headers: {
                    "Content-Type": "application/json", // Specifying the content type
                },
                body: JSON.stringify({
                    title: title,
                    release_year: parseInt(release_year),
                    duration_minutes: 120, // hardcoded for simplicity
                    description: "An updated movie", // hardcoded for simplicity
                    director_id: 1 // hardcoded for simplicity
                }), // Sending the data as JSON
            })
                .then((response) => response.json())
                .then((data) => {
                    console.log(data);
                    resultDiv.innerHTML = `✅ Movie updated successfully! Movie ID: ${data.movieId}`;
                })
                .catch((error) => {
                    console.error(error);
                    resultDiv.innerHTML = "❌ Error: " + error.message;
                });
        }
    </script>
</body>
</html>
```

## How to Test

1. Make sure you have existing movies in your database first (use POST to create some)
2. Start your server: `node server.js`
3. Open the HTML file in your browser
4. Fill in the fields:
   - Movie ID: 1 (use an existing movie ID from your database)
   - Title: "Updated Movie Title"
   - Release Year: 2025
5. Click "Update Movie"
6. Check the result on the webpage and in your database!

## Key Points

- **PUT** is used to update existing resources
- The movie ID goes in the **URL** (`/movies/:id`), not in the body
- We still send data in the **body** using `JSON.stringify()`
- We need to set the **Content-Type** header to "application/json"

## PUT vs POST

- **POST**: Creates new movies → `POST /movies`
- **PUT**: Updates existing movies → `PUT /movies/1`