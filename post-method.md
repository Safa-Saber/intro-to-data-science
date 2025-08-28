# POST Method Tutorial

## Server Code

Create your server file:

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

// POST method to create a new movie
app.post("/movies", async (req, res) => {
  const data = req.body;

  try {
    const db = await mysql.createConnection(dbConfig);

    const results = await db.query(`
      INSERT INTO movies (
        title,
        release_year,
        duration_minutes,
        description,
        director_id
      )
      VALUES (
        '${data.title}',
        ${data.release_year},
        ${data.duration_minutes},
        '${data.description}',
        ${data.director_id}
      )
    `);

    await db.end();

    res.send({
      message: "Movie created",
      movieId: results[0].insertId,
    });
  } catch (error) {
    res.status(500).send({
      message: "Error creating movie",
      error: error.message,
    });
  }
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});

```

## HTML Test File

Create an HTML file to test the POST method:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Test POST with Fetch</title>
</head>
<body>
    <h1>Create New Movie</h1>
    
    <input type="text" id="title" placeholder="Movie Title">
    <input type="number" id="release_year" placeholder="Release Year">
    
    <button onclick="createMovie()">Create Movie</button>
    
    <p id="result"></p>

    <script>
        function createMovie() {
            const title = document.getElementById("title").value;
            const release_year = document.getElementById("release_year").value;
            const resultDiv = document.getElementById("result");
            
            if (!title || !release_year) {
                alert("Please fill in all fields");
                return;
            }
            
            resultDiv.innerHTML = "Creating movie...";
            
            // Asking the server to create a new movie
            fetch("http://localhost:3000/movies", {
                method: "POST", // Specifying the method
                headers: {
                    "Content-Type": "application/json", // Specifying the content type
                },
                body: JSON.stringify({
                    title: title,
                    release_year: parseInt(release_year),
                    duration_minutes: 120, // hardcoded for simplicity
                    description: "A great movie", // hardcoded for simplicity
                    director_id: 1 // hardcoded for simplicity
                }), // Sending the data as JSON
            })
                .then((response) => response.json())
                .then((data) => {
                    console.log(data);
                    resultDiv.innerHTML = ` Movie created successfully! Movie ID: ${data.movieId}`;
                })
                .catch((error) => {
                    console.error(error);
                    resultDiv.innerHTML = "Error: " + error.message;
                });
        }
    </script>
</body>
</html>
```

## How to Test

1. Start your server: `node server.js`
2. Open the HTML file in your browser
3. Fill in all the fields:
   - Title: "Test Movie"
   - Release Year: 2024
   - Duration: 120
   - Description: "A test movie"
   - Director ID: 1 (use an existing director ID from your database)
4. Click "Create Movie"
5. Check the result on the webpage and in your database!


**Without JSON.stringify():** The server won't understand the data
**With JSON.stringify():** The server can read and process the data properly

Think of it like putting your data in an envelope before mailing it!
