# crispy-fiesta

<html lang="en" dir="ltr">
   
<head>
    <meta charset="utf-8">
    <title>
        How to take array input using JavaScript 
    </title>
</head>
 <style>
   
  @font-face {
    font-family: Montserrat;
    src: url(fonts/Montserrat-Regular.ttf);
}

.body style {
    box-sizing: border-box;
    font-family: Montserrat;
}

body {
    background-color: lightsteelblue;
    background-image: url("bg.jpg");
    height: 600px;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
}

.header {
    background-color: teal;
    padding: 30px 30px;
    color: white;
    text-align: center;
}

.header:after {
    content: "";
    display: table;
    clear: both;
}

* {
    box-sizing: border-box;
}

body {
    background-color: #00ff00;
    font-family: "Poppins", sans-serif;
    margin: 0;
}

header {
    background-color: #373b69;
    display: flex;
    justify-content: flex-end;
    padding: 1rem;
}

.search {
    background-color: transparent;
    border: 2px solid #22254b;
    border-radius: 50px;
    color: #fff;
    font-family: inherit;
    font-size: 1rem;
    padding: 0.5rem 1rem;
}

.search::placeholder {
    color: #7378c5;
}

.search:focus {
    background-color: #22254b;
    outline: none;
}

main {
    display: flex;
    flex-wrap: wrap;
}

.movie {
    background-color: #000099;
    border-radius: 3px;
    box-shadow: 0 4px 5px rgba(0, 0, 0, 0.2);
    overflow: hidden;
    position: relative;
    margin: 1rem;
    width: 300px;
}

.movie img {
    width: 100%;
}

.movie-info {
    color: #eee;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0.5rem 1rem 1rem;
    letter-spacing: 0.5px;
}

.movie-info h3 {
    margin: 0;
}

.movie-info span {
    background-color: #00ff00;
    border-radius: 3px;
    font-weight: bold;
    padding: 0.25rem 0.5rem;
}

.movie-info span.green {
    color: rgb(39, 189, 39);
}

.movie-info span.orange {
    color: orange;
}

.movie-info span.red {
    color: rgb(189, 42, 42);
}

.overview {
    background-color: #00ff00;
    padding: 2rem;
    position: absolute;
    max-height: 100%;
    overflow: auto;
    left: 0;
    bottom: 0;
    right: 0;
    transform: translateY(101%);
    transition: transform 0.3s ease-in;
}

.overview h3 {
    margin-top: 0;
}

.movie:hover .overview {
    transform: translateY(0);
}
  </style>
  
  
<body style="text-align: center;">
<form>
   <h1>Please Enter Your Favorite Movies</h1>
   <br>
      <label for="movie">Movie Name:</label> 
       <input id="movie" type="text">
     <br> 
    
   <br>
     <label for="year">Year Released:</label>
   <input id="year" type="text">
   <br>
   <br>   
    <label for="reason">Why You Like it?</label>
   <input id="reason" type="text">
   <br>
    
   <br>
  <input type="button" value="Add Movie" onclick="addData()">
   <input type="button" value="Display Movie" onclick="displayData()">
  
  <input type="button" value="Reset Movie List" onclick="resetData()">
   <br>
   <br>
</form>
<div id="display"></div>
  
 
     <body>
        <header>
            <form id="form">
                <input
                    type="text"
                    id="search"
                    placeholder="Search"
                    class="search"
                />
            </form>
        </header>
        <main id="main"></main>
    </body>
  <script>
  const APIURL =
    "https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=04c35731a5ee918f014970082a0088b1&page=1";
const IMGPATH = "https://image.tmdb.org/t/p/w1280";
const SEARCHAPI =
    "https://api.themoviedb.org/3/search/movie?&api_key=04c35731a5ee918f014970082a0088b1&query=";

const main = document.getElementById("main");
const form = document.getElementById("form");
const search = document.getElementById("search");

// initially get fav movies
getMovies(APIURL);

async function getMovies(url) {
    const resp = await fetch(url);
    const respData = await resp.json();

    console.log(respData);

    showMovies(respData.results);
}

function showMovies(movies) {
    // clear main
    main.innerHTML = "";

    movies.forEach((movie) => {
        const { poster_path, title, vote_average, overview } = movie;

        const movieEl = document.createElement("div");
        movieEl.classList.add("movie");

        movieEl.innerHTML = `
            <img
                src="${IMGPATH + poster_path}"
                alt="${title}"
            />
            <div class="movie-info">
                <h3>${title}</h3>
                <span class="${getClassByRate(
                    vote_average
                )}">${vote_average}</span>
            </div>
            <div class="overview">
                <h3>Overview:</h3>
                ${overview}
            </div>
        `;

        main.appendChild(movieEl);
    });
}

function getClassByRate(vote) {
    if (vote >= 8) {
        return "green";
    } else if (vote >= 5) {
        return "orange";
    } else {
        return "red";
    }
}

form.addEventListener("submit", (e) => {
    e.preventDefault();

    const searchTerm = search.value;

    if (searchTerm) {
        getMovies(SEARCHAPI + searchTerm);

        search.value = "";
    }
});




var arrMovie=new Array();
var arrYear=new Array();
var arrReason=new Array();
 
function addData(){
    var movie = document.getElementById('movie').value;
    var reason= document.getElementById('reason').value;
    var year = document.getElementById('year').value;
    arrReason[arrReason.lengths]=reason;    
  arrMovie[arrMovie.length]=movie;
  arrYear[arrYear.length]=year;
  
  document.getElementById('year').value='';
  document.getElementById('movie').value='';
  document.getElementById('reason').value='';
  }
   
 
function displayData() 
{
  var content="<b>Data Entered by User :</b><br>";
  content+= [...arrMovie]+"</br>";
  content+=[...arrYear]+"</br>";
  content+=[...arrReason]+"</br>";
 
  document.getElementById('display').innerHTML = content;
}
 
 function resetData() 
{
 arrMovie=new Array();
arrYear=new Array();
arrReason=new Array();
  
  var content="<b>Reset Movie Entered by User</b><br>";
  document.getElementById('display').innerHTML = content;
}
 
</script>

 
