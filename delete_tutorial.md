# DELETE Method Tutorial

## Server Code (First Version)

Create your server file:

```javascript
const express = require("express");
const cors = require("cors");
const mysql = require("mysql2/promise");

const app = express();
const port = 3000;

app.use(cors());
app.use(express.json());

// Database configuration
const dbConfig = {
  host: "localhost",
  user: "root",
  password: "your_password", // replace with your password
  database: "test",
};

// DELETE method to delete a movie by its ID
app.delete("/movies/:movie_id", async (req, res) => {
  const movieId = req.params.movie_id;

  try {
    const db = await mysql.createConnection(dbConfig);
    
    const [results] = await db.execute(
      "DELETE FROM movies WHERE movie_id = ?",
      [movieId]
    );

    await db.end();

    res.send({
      message: "Movie deleted successfully",
      affectedRows: results.affectedRows,
    });
  } catch (error) {
    res.status(500).send({
      message: "Error deleting movie",
      error: error.message,
    });
  }
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## HTML Test File

Create an HTML file to test the DELETE method:

```html
<!DOCTYPE html>
<html>
<head>
    <title>Test DELETE with Fetch</title>
</head>
<body>
    <h1>Delete Movie</h1>
    
    <input type="number" id="movieId" placeholder="Enter movie ID">
    <button onclick="deleteMovie()">Delete Movie</button>
    
    <p id="result"></p>

    <script>
        function deleteMovie() {
            const movieId = document.getElementById("movieId").value;
            const resultDiv = document.getElementById("result");
            
            if (!movieId) {
                alert("Please enter a movie ID");
                return;
            }
            
            resultDiv.innerHTML = "Deleting...";
            
            // Asking the server to delete a movie with the entered ID
            fetch(`http://localhost:3000/movies/${movieId}`, {
                method: "DELETE",
            })
                .then((response) => response.json())
                .then((data) => {
                    console.log(data);
                    if (data.affectedRows > 0) {
                        resultDiv.innerHTML = "✅ Movie deleted successfully!";
                    } else {
                        resultDiv.innerHTML = "⚠️ Movie not found";
                    }
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

## Possible Foreign Key Error

When you test the DELETE method, you might get this error:

```
"Cannot delete or update a parent row: a foreign key constraint fails"
```

**What does this mean?**

This happens when the movie you're trying to delete is connected to other tables. For example, if movie ID 2 has actors in the `movie_actors` table, MySQL won't let you delete it because it would break the connection.

## Fixed Server Code

To fix this issue, we need to temporarily disable foreign key checks. Here's the updated server code:

```javascript
const express = require("express");
const cors = require("cors");
const mysql = require("mysql2/promise");

const app = express();
const port = 3000;

app.use(cors());
app.use(express.json());

// Database configuration
const dbConfig = {
  host: "localhost",
  user: "root",
  password: "your_password", // replace with your password
  database: "test",
};

// DELETE method to delete a movie by its ID
app.delete("/movies/:movie_id", async (req, res) => {
  const movieId = req.params.movie_id;

  try {
    const db = await mysql.createConnection(dbConfig);
    
    // Temporarily disable foreign key checks
    await db.execute("SET FOREIGN_KEY_CHECKS = 0");
    
    const [results] = await db.execute(
      "DELETE FROM movies WHERE movie_id = ?",
      [movieId]
    );
    
    // Re-enable foreign key checks
    await db.execute("SET FOREIGN_KEY_CHECKS = 1");
    
    await db.end();

    res.send({
      message: "Movie deleted successfully",
      affectedRows: results.affectedRows,
    });
  } catch (error) {
    res.status(500).send({
      message: "Error deleting movie",
      error: error.message,
    });
  }
});

app.listen(port, () => {
  console.log(`Server running on http://localhost:${port}`);
});
```

## What Changed?

We added **3 lines** to fix the foreign key issue:

1. `await db.execute("SET FOREIGN_KEY_CHECKS = 0");` - Turn off foreign key checks
2. `await db.execute("SET FOREIGN_KEY_CHECKS = 1");` - Turn them back on
3. These lines go before and after the DELETE query

Now you can delete any movie without getting foreign key errors!

## How to Test

1. Start your server: `node server.js`
2. Open the HTML file in your browser
3. Enter a movie ID (like 1, 2, 4, etc.)
4. Click "Delete Movie"
5. Check the result on the webpage and in your database!