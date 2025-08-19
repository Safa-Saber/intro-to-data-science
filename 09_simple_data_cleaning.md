# Simple Data Cleaning Example

## Installation
```bash
pip install requests beautifulsoup4
```

## Complete Code

```python
import requests
from bs4 import BeautifulSoup
import re

def getParsedWebpage(url):
    headers = {"User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36"}
    response = requests.get(url, headers=headers)
    if response.status_code == 200:
        return BeautifulSoup(response.content, 'html.parser')
    return 'error'

# Scrape quotes (they need cleaning!)
url = 'http://quotes.toscrape.com/'
soup = getParsedWebpage(url)

if soup != 'error':
    quotes = soup.find_all('div', class_='quote')
    
    print("BEFORE CLEANING:")
    print("-" * 40)
    
    for i, quote in enumerate(quotes[:3], 1):
        raw_text = quote.find('span', class_='text').text
        raw_author = quote.find('small', class_='author').text
        print(f"{i}. {raw_text} by {raw_author}")
    
    print("\nAFTER CLEANING:")
    print("-" * 40)
    
    # START DATA CLEANING HERE
    for i, quote in enumerate(quotes[:3], 1):
        # Clean the text - make it uppercase and add stars
        raw_text = quote.find('span', class_='text').text
        clean_text = raw_text.upper()  # Make text UPPERCASE
        clean_text = f"⭐ {clean_text} ⭐"  # Add stars around the quote
        
        # Clean the author - remove extra spaces and make lowercase
        raw_author = quote.find('small', class_='author').text
        clean_author = raw_author.strip().lower()  # Remove spaces and make lowercase
        
        print(f"{i}. {clean_text} - {clean_author}")
else:
    print("Failed to scrape website")
```

## Explanation of Data Cleaning

**What is Data Cleaning?**
- Removing unwanted characters like quotes `"` and `"`
- Removing extra spaces with `.strip()`
- Fixing capitalization with `.title()`
- Making data consistent and neat

**Line-by-line cleaning explanation:**

```python
raw_text = quote.find('span', class_='text').text
```
- **Line 1**: Get the original messy text from the website

```python
clean_text = raw_text.replace('"', '').replace('"', '')
```
- **Line 2**: Remove opening `"` and closing `"` quote marks

```python
clean_text = clean_text.strip()
```
- **Line 3**: Remove extra spaces at beginning and end

```python
raw_author = quote.find('small', class_='author').text
clean_author = raw_author.strip().title()
```
- **Line 4-5**: Clean author name - remove spaces and make proper capitalization

**Common Cleaning Methods:**
- `.strip()` - removes spaces
- `.replace('old', 'new')` - replaces unwanted text
- `.title()` - makes proper capitalization
- `.lower()` - makes everything lowercase
- `.upper()` - makes everything uppercase

**Expected Output:**
```
BEFORE CLEANING:
----------------------------------------
1. "The world as we have created it..." by albert einstein
2. "It is our choices, Harry..." by j.k. rowling  
3. "There are only two ways..." by albert einstein

AFTER CLEANING:
----------------------------------------
1. The world as we have created it... - Albert Einstein
2. It is our choices, Harry... - J.K. Rowling
3. There are only two ways... - Albert Einstein
```


```
const express = require("express");
const cors = require("cors");
const app = express();
const port = 3000;

app.use(cors());
app.listen(port, () => {
  console.log(`Server app listening at http://localhost:${port}`);
});

/*
 *   ↑↑↑ DO NOT change the code above this comment
 *   =============================================
 *   ↓↓↓ ADD your code below this comment
 */

// Get Homepage movie data
app.get("/", (req, res) => {
  let data = [];
  for (let i = 0; i < genres.length; i++) {
    let moviesByGenre = [];
    for (let j = 0; j < movies.length; j++) {
      if (movies[j].genre == genres[i]) {
        moviesByGenre.push(movies[j]);
        if (moviesByGenre.length >= 2) {
          break;
        }
      }
    }
    data.push({
      genre: genres[i],
      movies: moviesByGenre,
    });
  }
  res.json(data);
});

/* 
    Get all movies of a certain genre:

    - /genres/Action
    - /genres/Comedy
    - /genres/Drama
    - /genres/Horror
    - /genres/Sci-Fi
*/
app.get("/genres/:genre", (req, res) => {
  const genre = req.params.genre;
  const moviesByGenre = [];
  for (let i = 0; i < movies.length; i++) {
    if (movies[i].genre == genre) {
      movies[i].reviewCount = getMovieReviewCount(movies[i].id);
      moviesByGenre.push(movies[i]);
    }
  }
  res.json(moviesByGenre);
});

app.get("/movies/:id", (req, res) => {
  const id = req.params.id;
  for (let i = 0; i < movies.length; i++) {
    if (movies[i].id == id) {
      res.json(movies[i]);
    }
  }
  res.json("Movie not found");
});

function getMovieReviewCount(movieId) {
  let count = 0;
  for (let i = 0; i < reviews.length; i++) {
    if (reviews[i].movieId == movieId) {
      count += 1;
    }
  }
  return count;
}

const genres = ["Action", "Drama", "Comedy", "Horror", "Sci-Fi"];
// ovie data
const movies = [
  {
    id: 1,
    title: "Mad Max: Fury Road",
    year: 2015,
    director: "George Miller",
    rating: 8.6,
    genre: "Action",
    description:
      "In a desert wasteland, Max and Furiosa flee a tyrant in a roaring convoy chase.",
    actors: ["Tom Hardy", "Charlize Theron", "Nicholas Hoult"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/6/6e/Mad_Max_Fury_Road.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4",
  },
  {
    id: 2,
    title: "John Wick",
    year: 2014,
    director: "Chad Stahelski",
    rating: 8.0,
    genre: "Action",
    description: "A retired hitman returns to the underworld to exact revenge.",
    actors: ["Keanu Reeves", "Michael Nyqvist", "Alfie Allen"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/9/98/John_Wick_TeaserPoster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4",
  },
  {
    id: 3,
    title: "Mission: Impossible – Fallout",
    year: 2018,
    director: "Christopher McQuarrie",
    rating: 8.2,
    genre: "Action",
    description:
      "Ethan Hunt races to stop a global catastrophe after a mission goes wrong.",
    actors: ["Tom Cruise", "Henry Cavill", "Rebecca Ferguson"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/f/ff/MI_%E2%80%93_Fallout.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/Sintel.mp4",
  },
  {
    id: 4,
    title: "Die Hard",
    year: 1988,
    director: "John McTiernan",
    rating: 8.2,
    genre: "Action",
    description:
      "An NYPD cop battles terrorists in a Los Angeles skyscraper on Christmas Eve.",
    actors: ["Bruce Willis", "Alan Rickman", "Bonnie Bedelia"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/thumb/c/ca/Die_Hard_%281988_film%29_poster.jpg/250px-Die_Hard_%281988_film%29_poster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerEscapes.mp4",
  },
  {
    id: 5,
    title: "The Dark Knight",
    year: 2008,
    director: "Christopher Nolan",
    rating: 9.0,
    genre: "Action",
    description:
      "Batman faces the Joker, whose chaos tests Gotham and the hero’s limits.",
    actors: ["Christian Bale", "Heath Ledger", "Aaron Eckhart"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/1/1c/The_Dark_Knight_%282008_film%29.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerFun.mp4",
  },
  {
    id: 6,
    title: "Superbad",
    year: 2007,
    director: "Greg Mottola",
    rating: 7.7,
    genre: "Comedy",
    description:
      "Two best friends scramble to make their last week of high school legendary.",
    actors: ["Jonah Hill", "Michael Cera", "Christopher Mintz-Plasse"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/8/8b/Superbad_Poster.png",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerJoyrides.mp4",
  },
  {
    id: 7,
    title: "The Hangover",
    year: 2009,
    director: "Todd Phillips",
    rating: 7.7,
    genre: "Comedy",
    description:
      "After a wild night in Vegas, three friends retrace their steps to find the groom.",
    actors: ["Bradley Cooper", "Ed Helms", "Zach Galifianakis"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/b/b9/Hangoverposter09.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerMeltdowns.mp4",
  },
  {
    id: 8,
    title: "Groundhog Day",
    year: 1993,
    director: "Harold Ramis",
    rating: 8.0,
    genre: "Comedy",
    description:
      "A cynical weatherman relives the same day until he gets life right.",
    actors: ["Bill Murray", "Andie MacDowell", "Chris Elliott"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/thumb/b/b1/Groundhog_Day_%28movie_poster%29.jpg/250px-Groundhog_Day_%28movie_poster%29.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4",
  },
  {
    id: 9,
    title: "Bridesmaids",
    year: 2011,
    director: "Paul Feig",
    rating: 7.5,
    genre: "Comedy",
    description:
      "A down-on-her-luck maid of honor spirals as a wedding approaches.",
    actors: ["Kristen Wiig", "Maya Rudolph", "Rose Byrne"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/thumb/d/df/BridesmaidsPoster.jpg/250px-BridesmaidsPoster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/SubaruOutbackOnStreetAndDirt.mp4",
  },
  {
    id: 10,
    title: "Mean Girls",
    year: 2004,
    director: "Mark Waters",
    rating: 7.1,
    genre: "Comedy",
    description:
      "A teen navigates high school cliques after moving from Africa to the suburbs.",
    actors: ["Lindsay Lohan", "Rachel McAdams", "Tina Fey"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/thumb/a/ac/Mean_Girls_film_poster.png/250px-Mean_Girls_film_poster.png",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/WeAreGoingOnBullrun.mp4",
  },
  {
    id: 11,
    title: "The Shawshank Redemption",
    year: 1994,
    director: "Frank Darabont",
    rating: 9.3,
    genre: "Drama",
    description:
      "Two imprisoned men bond over years, finding solace and redemption.",
    actors: ["Tim Robbins", "Morgan Freeman", "Bob Gunton"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/8/81/ShawshankRedemptionMoviePoster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/WhatCarCanYouGetForAGrand.mp4",
  },
  {
    id: 12,
    title: "Forrest Gump",
    year: 1994,
    director: "Robert Zemeckis",
    rating: 8.8,
    genre: "Drama",
    description:
      "A simple man unwittingly influences decades of American history.",
    actors: ["Tom Hanks", "Robin Wright", "Gary Sinise"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/6/67/Forrest_Gump_poster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/TearsOfSteel.mp4",
  },
  {
    id: 13,
    title: "The Godfather",
    year: 1972,
    director: "Francis Ford Coppola",
    rating: 9.2,
    genre: "Drama",
    description:
      "The aging patriarch of a crime dynasty transfers control to his reluctant son.",
    actors: ["Marlon Brando", "Al Pacino", "James Caan"],
    poster: "https://upload.wikimedia.org/wikipedia/en/1/1c/Godfather_ver1.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/VolkswagenGTIReview.mp4",
  },
  {
    id: 14,
    title: "Moonlight",
    year: 2016,
    director: "Barry Jenkins",
    rating: 8.2,
    genre: "Drama",
    description:
      "A young Black man grapples with identity and love across three chapters of his life.",
    actors: ["Trevante Rhodes", "André Holland", "Janelle Monáe"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/8/84/Moonlight_%282016_film%29.png",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerJoyrides.mp4",
  },
  {
    id: 15,
    title: "Whiplash",
    year: 2014,
    director: "Damien Chazelle",
    rating: 8.5,
    genre: "Drama",
    description:
      "An ambitious drummer clashes with a ruthless jazz instructor.",
    actors: ["Miles Teller", "J. K. Simmons", "Melissa Benoist"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/0/01/Whiplash_poster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4",
  },
  {
    id: 16,
    title: "The Exorcist",
    year: 1973,
    director: "William Friedkin",
    rating: 8.1,
    genre: "Horror",
    description:
      "When a girl is possessed, a priest confronts a demonic force.",
    actors: ["Ellen Burstyn", "Max von Sydow", "Linda Blair"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/thumb/7/7b/Exorcist_ver2.jpg/250px-Exorcist_ver2.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerEscapes.mp4",
  },
  {
    id: 17,
    title: "A Nightmare on Elm Street",
    year: 1984,
    director: "Wes Craven",
    rating: 7.4,
    genre: "Horror",
    description:
      "Teens are stalked in their dreams by a burned killer with a bladed glove.",
    actors: ["Heather Langenkamp", "Robert Englund", "Johnny Depp"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/thumb/f/fa/A_Nightmare_on_Elm_Street_%281984%29_theatrical_poster.jpg/250px-A_Nightmare_on_Elm_Street_%281984%29_theatrical_poster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerFun.mp4",
  },
  {
    id: 18,
    title: "The Conjuring",
    year: 2013,
    director: "James Wan",
    rating: 7.5,
    genre: "Horror",
    description:
      "Paranormal investigators help a family terrorized by a dark presence.",
    actors: ["Vera Farmiga", "Patrick Wilson", "Lili Taylor"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/8/8c/The_Conjuring_poster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerMeltdowns.mp4",
  },
  {
    id: 19,
    title: "Hereditary",
    year: 2018,
    director: "Ari Aster",
    rating: 7.8,
    genre: "Horror",
    description: "A family’s grief uncovers a chilling, inherited fate.",
    actors: ["Toni Collette", "Alex Wolff", "Milly Shapiro"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/thumb/d/d9/Hereditary.png/250px-Hereditary.png",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ForBiggerBlazes.mp4",
  },
  {
    id: 20,
    title: "Get Out",
    year: 2017,
    director: "Jordan Peele",
    rating: 8.0,
    genre: "Horror",
    description:
      "A Black man uncovers a sinister secret while visiting his white girlfriend’s family.",
    actors: ["Daniel Kaluuya", "Allison Williams", "Bradley Whitford"],
    poster: "https://upload.wikimedia.org/wikipedia/en/a/a3/Get_Out_poster.png",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/SubaruOutbackOnStreetAndDirt.mp4",
  },
  {
    id: 21,
    title: "Interstellar",
    year: 2014,
    director: "Christopher Nolan",
    rating: 8.6,
    genre: "Sci-Fi",
    description:
      "Explorers travel through a wormhole to save humanity from a dying Earth.",
    actors: ["Matthew McConaughey", "Anne Hathaway", "Jessica Chastain"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/b/bc/Interstellar_film_poster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/TearsOfSteel.mp4",
  },
  {
    id: 22,
    title: "Blade Runner 2049",
    year: 2017,
    director: "Denis Villeneuve",
    rating: 8.0,
    genre: "Sci-Fi",
    description:
      "A young blade runner unearths a secret that could plunge society into chaos.",
    actors: ["Ryan Gosling", "Harrison Ford", "Ana de Armas"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/9/9b/Blade_Runner_2049_poster.png",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/Sintel.mp4",
  },
  {
    id: 23,
    title: "The Matrix",
    year: 1999,
    director: "The Wachowskis",
    rating: 8.7,
    genre: "Sci-Fi",
    description:
      "A hacker learns reality is a simulation and joins the fight to free humanity.",
    actors: ["Keanu Reeves", "Laurence Fishburne", "Carrie-Anne Moss"],
    poster: "https://upload.wikimedia.org/wikipedia/en/9/94/The_Matrix.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4",
  },
  {
    id: 24,
    title: "Inception",
    year: 2010,
    director: "Christopher Nolan",
    rating: 8.8,
    genre: "Sci-Fi",
    description: "A thief enters dreams to plant an idea in a target’s mind.",
    actors: ["Leonardo DiCaprio", "Joseph Gordon-Levitt", "Elliot Page"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/2/2e/Inception_%282010%29_theatrical_poster.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/ElephantsDream.mp4",
  },
  {
    id: 25,
    title: "Star Wars: Episode IV – A New Hope",
    year: 1977,
    director: "George Lucas",
    rating: 8.6,
    genre: "Sci-Fi",
    description:
      "A farm boy joins a rebellion to destroy a planet-killing battle station.",
    actors: ["Mark Hamill", "Harrison Ford", "Carrie Fisher"],
    poster:
      "https://upload.wikimedia.org/wikipedia/en/8/87/StarWarsMoviePoster1977.jpg",
    video:
      "https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/Sintel.mp4",
  },
];

const reviews = [
  // Mad Max: Fury Road
  {
    id: 1,
    movieId: 1,
    createdAt: "2023-06-12",
    title: "Explosive action!",
    description: "The stunts and visuals are insane. Non-stop adrenaline.",
    rating: 9,
  },
  {
    id: 2,
    movieId: 1,
    createdAt: "2023-07-01",
    title: "Charlize steals the show",
    description: "Furiosa was the heart of the movie. Loved every minute.",
    rating: 10,
  },
  {
    id: 3,
    movieId: 1,
    createdAt: "2023-07-15",
    title: "Pure cinema",
    description: "One of the best action films ever made.",
    rating: 9,
  },

  // John Wick
  {
    id: 4,
    movieId: 2,
    createdAt: "2022-12-10",
    title: "Stylish revenge",
    description: "Keanu is perfect. Fight choreography is unmatched.",
    rating: 8,
  },
  {
    id: 5,
    movieId: 2,
    createdAt: "2023-01-03",
    title: "Best gun-fu ever",
    description: "The nightclub scene alone is worth the ticket.",
    rating: 9,
  },
  {
    id: 6,
    movieId: 2,
    createdAt: "2023-01-20",
    title: "Simple but effective",
    description: "Straightforward story, executed brilliantly.",
    rating: 7,
  },

  // Mission: Impossible – Fallout
  {
    id: 7,
    movieId: 3,
    createdAt: "2023-03-22",
    title: "Best MI yet",
    description: "Tom Cruise hanging from helicopters? Insane commitment.",
    rating: 9,
  },
  {
    id: 8,
    movieId: 3,
    createdAt: "2023-03-30",
    title: "Henry Cavill!",
    description: "His bathroom fight scene was jaw-dropping.",
    rating: 8,
  },
  {
    id: 9,
    movieId: 3,
    createdAt: "2023-04-10",
    title: "Great pacing",
    description: "Tense, well-structured, and thrilling all the way.",
    rating: 8,
  },

  // Die Hard
  {
    id: 10,
    movieId: 4,
    createdAt: "2022-12-24",
    title: "The best Christmas movie",
    description: "It’s not Christmas until John McClane saves Nakatomi Plaza.",
    rating: 10,
  },
  {
    id: 11,
    movieId: 4,
    createdAt: "2023-01-15",
    title: "Alan Rickman forever",
    description: "Hans Gruber is one of the greatest villains ever.",
    rating: 9,
  },

  // The Dark Knight
  {
    id: 12,
    movieId: 5,
    createdAt: "2023-05-10",
    title: "Masterpiece",
    description: "Heath Ledger’s Joker changed comic book movies forever.",
    rating: 10,
  },
  {
    id: 13,
    movieId: 5,
    createdAt: "2023-05-12",
    title: "Dark and brilliant",
    description: "Nolan nailed the atmosphere and storytelling.",
    rating: 9,
  },
  {
    id: 14,
    movieId: 5,
    createdAt: "2023-06-01",
    title: "Still holds up",
    description: "Even after many rewatches, it feels fresh.",
    rating: 9,
  },

  // Superbad
  {
    id: 15,
    movieId: 6,
    createdAt: "2023-02-14",
    title: "So funny!",
    description: "Never gets old. McLovin is iconic.",
    rating: 8,
  },
  {
    id: 16,
    movieId: 6,
    createdAt: "2023-03-01",
    title: "Teen comedy gold",
    description: "Captures awkward high school vibes perfectly.",
    rating: 7,
  },

  // The Hangover
  {
    id: 17,
    movieId: 7,
    createdAt: "2023-01-05",
    title: "Vegas chaos",
    description: "Every rewatch is hilarious. Great chemistry.",
    rating: 8,
  },
  {
    id: 18,
    movieId: 7,
    createdAt: "2023-01-18",
    title: "Classic comedy",
    description: "Absurd but endlessly entertaining.",
    rating: 7,
  },

  // Groundhog Day
  {
    id: 19,
    movieId: 8,
    createdAt: "2023-04-01",
    title: "Bill Murray magic",
    description: "Funny and surprisingly deep.",
    rating: 8,
  },
  {
    id: 20,
    movieId: 8,
    createdAt: "2023-04-12",
    title: "Timeless",
    description: "The loop concept still feels fresh today.",
    rating: 9,
  },

  // Bridesmaids
  {
    id: 21,
    movieId: 9,
    createdAt: "2023-02-07",
    title: "Laugh out loud",
    description: "The airplane scene kills me every time.",
    rating: 8,
  },
  {
    id: 22,
    movieId: 9,
    createdAt: "2023-02-20",
    title: "Great cast",
    description: "Wiig and McCarthy are unforgettable.",
    rating: 8,
  },

  // Mean Girls
  {
    id: 23,
    movieId: 10,
    createdAt: "2022-11-12",
    title: "So fetch",
    description: "One of the most quotable movies ever.",
    rating: 9,
  },
  {
    id: 24,
    movieId: 10,
    createdAt: "2022-11-25",
    title: "High school classic",
    description: "Sharp and witty. Tina Fey nailed it.",
    rating: 8,
  },

  // Shawshank Redemption
  {
    id: 25,
    movieId: 11,
    createdAt: "2023-05-20",
    title: "Best film ever?",
    description: "Emotional, inspiring, unforgettable.",
    rating: 10,
  },
  {
    id: 26,
    movieId: 11,
    createdAt: "2023-06-02",
    title: "Powerful",
    description: "The ending never fails to move me.",
    rating: 10,
  },

  // Forrest Gump
  {
    id: 27,
    movieId: 12,
    createdAt: "2023-03-15",
    title: "Life is like a box of chocolates",
    description: "Tom Hanks at his best.",
    rating: 9,
  },
  {
    id: 28,
    movieId: 12,
    createdAt: "2023-04-01",
    title: "Emotional journey",
    description: "Funny, sad, and beautiful.",
    rating: 9,
  },

  // The Godfather
  {
    id: 29,
    movieId: 13,
    createdAt: "2022-12-10",
    title: "Epic masterpiece",
    description: "Coppola’s direction is flawless.",
    rating: 10,
  },
  {
    id: 30,
    movieId: 13,
    createdAt: "2023-01-08",
    title: "Marlon Brando!",
    description: "One of the greatest performances ever.",
    rating: 10,
  },

  // Moonlight
  {
    id: 31,
    movieId: 14,
    createdAt: "2023-06-05",
    title: "Beautiful film",
    description: "Delicate storytelling, stunning visuals.",
    rating: 9,
  },
  {
    id: 32,
    movieId: 14,
    createdAt: "2023-06-15",
    title: "Heartbreaking",
    description: "Touches on identity and love in a raw way.",
    rating: 8,
  },

  // Whiplash
  {
    id: 33,
    movieId: 15,
    createdAt: "2023-02-01",
    title: "Intense!",
    description: "Simmons is terrifying, the tension is insane.",
    rating: 9,
  },
  {
    id: 34,
    movieId: 15,
    createdAt: "2023-02-14",
    title: "Inspiring",
    description: "Pushes you to chase perfection.",
    rating: 8,
  },

  // The Exorcist
  {
    id: 35,
    movieId: 16,
    createdAt: "2022-10-31",
    title: "Terrifying",
    description: "Still the scariest movie ever.",
    rating: 9,
  },
  {
    id: 36,
    movieId: 16,
    createdAt: "2022-11-01",
    title: "Classic horror",
    description: "The atmosphere is unmatched.",
    rating: 8,
  },

  // Nightmare on Elm Street
  {
    id: 37,
    movieId: 17,
    createdAt: "2022-12-05",
    title: "Freddy rules",
    description: "Such a creative horror concept.",
    rating: 8,
  },
  {
    id: 38,
    movieId: 17,
    createdAt: "2022-12-12",
    title: "Creepy",
    description: "The dream scenes are haunting.",
    rating: 7,
  },

  // The Conjuring
  {
    id: 39,
    movieId: 18,
    createdAt: "2023-01-25",
    title: "Scary!",
    description: "Jump scares done right.",
    rating: 8,
  },
  {
    id: 40,
    movieId: 18,
    createdAt: "2023-02-05",
    title: "Well crafted",
    description: "Wan knows how to build suspense.",
    rating: 8,
  },

  // Hereditary
  {
    id: 41,
    movieId: 19,
    createdAt: "2023-03-18",
    title: "Disturbing",
    description: "The dinner table scene shook me.",
    rating: 9,
  },
  {
    id: 42,
    movieId: 19,
    createdAt: "2023-03-25",
    title: "Ari Aster brilliance",
    description: "Unsettling and unforgettable.",
    rating: 9,
  },

  // Get Out
  {
    id: 43,
    movieId: 20,
    createdAt: "2023-04-01",
    title: "Social horror",
    description: "Smart, scary, and relevant.",
    rating: 9,
  },
  {
    id: 44,
    movieId: 20,
    createdAt: "2023-04-10",
    title: "Jordan Peele delivers",
    description: "A genre-bending masterpiece.",
    rating: 9,
  },

  // Interstellar
  {
    id: 45,
    movieId: 21,
    createdAt: "2023-05-05",
    title: "Mind-blowing visuals",
    description: "The black hole scene was stunning.",
    rating: 10,
  },
  {
    id: 46,
    movieId: 21,
    createdAt: "2023-05-15",
    title: "Emotional sci-fi",
    description: "The father-daughter story hit hard.",
    rating: 9,
  },

  // Blade Runner 2049
  {
    id: 47,
    movieId: 22,
    createdAt: "2023-06-02",
    title: "Visual masterpiece",
    description: "Every frame is art.",
    rating: 9,
  },
  {
    id: 48,
    movieId: 22,
    createdAt: "2023-06-12",
    title: "Slow but brilliant",
    description: "Requires patience, but worth it.",
    rating: 8,
  },

  // The Matrix
  {
    id: 49,
    movieId: 23,
    createdAt: "2022-11-20",
    title: "Game changer",
    description: "Red pill, blue pill—iconic cinema.",
    rating: 10,
  },
  {
    id: 50,
    movieId: 23,
    createdAt: "2022-11-28",
    title: "Still cool",
    description: "Action scenes hold up even today.",
    rating: 9,
  },

  // Inception
  {
    id: 51,
    movieId: 24,
    createdAt: "2023-01-10",
    title: "Dream within a dream",
    description: "Nolan’s imagination on full display.",
    rating: 9,
  },
  {
    id: 52,
    movieId: 24,
    createdAt: "2023-01-22",
    title: "Amazing score",
    description: "Hans Zimmer’s music elevates everything.",
    rating: 10,
  },

  // Star Wars IV
  {
    id: 53,
    movieId: 25,
    createdAt: "2022-12-05",
    title: "The beginning of it all",
    description: "Changed sci-fi forever.",
    rating: 10,
  },
  {
    id: 54,
    movieId: 25,
    createdAt: "2022-12-18",
    title: "Classic adventure",
    description: "Simple story, perfectly executed.",
    rating: 9,
  },
];
```
