# Introduction

There are several popular reference applications that web developers often use as "canonical" or "holotype" examples when learning or comparing JavaScript frameworks and libraries. These range from examples that optimize for simplicity (e.g. TodoMVC) to those that attempt to better model real-world complexity better, relying on third-party APIs. 

These include:

1. [TodoMVC](todomvc.com): This is a simple to-do list application that is implemented using various JavaScript frameworks. It often used as a starting point for learning a new framework. It is also used in the Speedometer browser benchmark.
1. [Hacker News Clone](hnpwa.com): This is a clone of the popular news website, Hacker News and is more complex than TodoMVC as it contains multiple views, comment threads and does rely on a real data source.
1. [Movies](https://tastejs.com/movies/): This is a real-world movie listing and discovery web application that allows users to browse and search for movies, view movie details, read reviews, and create lists of their favorite movies. It is intended to demonstrate how to build a web application that integrates with a third-party API such as TMDB and can include authentication making it more "complete"
1. E-Commerce: This is a simple e-commerce web application that allows users to browse, search and purchase products. It can be implemented using third-party services and Vercel's [ACME Storefront](https://demo.vercel.store/) is a good example.

This doc covers an outline for a Movies application built using TMDB.

## What is TMDB (The Movie Database)?

[TMDB](https://www.themoviedb.org/?language=en-US), also known as The Movie Database, is a community-driven website that provides a database of information about movies, TV shows, and actors. It includes information such as title, release date, overview, cast, crew, and more. The website also has a user-friendly interface that allows users to search, filter, and browse through the database of movies and TV shows.  

[The TMDB API](https://developers.themoviedb.org/3) is a way for developers to access and retrieve information from the TMDB database. It is a RESTful API that allows developers to make HTTP requests to retrieve information in a variety of formats such as JSON or XML. The API requires an API key, which can be obtained by registering as a developer on the TMDB website.  
To use the API, developers can make various types of requests to different endpoints such as:

-  Retrieving information about a specific movie or TV show by its ID
-  Retrieving a list of popular movies or TV shows
-  Searching for movies or TV shows by title or keywords
-  Retrieving information about a specific actor or cast member
-  Retrieving a list of reviews for a movie or TV show

For example, here is how to fetch popular movies from the TMDB API:  

```js
// Replace YOUR_API_KEY with your TMDB API key  
const API_KEY = "YOUR_API_KEY";

async function fetchPopularMovies() {  
    // Make a request to the TMDB API to fetch a list of popular movies  
    const response = await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${API_KEY}`);

    // Parse the response as JSON  
    const data = await response.json();

    // Log the list of popular movies  
    console.log(data.results);  
}

// Call the function to fetch popular movies  
fetchPopularMovies();  
```  

The API also has a number of parameters and options that can be used to filter and sort the data that is returned. For example, developers can use parameters to specify the language of the data, the number of results per page, and the sort order of the results.  

Overall, the TMDB API allows developers to easily access and retrieve information from the TMDB database and use it to build a variety of applications such as movie and TV show listing, recommendation, and searching apps.

## What does the TMDB website do that a client could?

The TMDB (The Movie Database) website offers a variety of features for users to explore and discover movies and TV shows.   
Some of the main features include:

1. Search and Browse: Users can easily search and browse through the database by title, keywords, or genres. There's also an option to filter and sort the results.
1. Movie and TV show pages: Each movie and TV show in the database has its own page that includes detailed information and images. Users can also view trailers, reviews and ratings from other users.
1. People pages: The website also includes detailed information about actors, directors, writers, and other crew members. Each person has their own page that includes a list of their credits, biography and other information.
1. Lists: Users can create and manage their own lists of movies and TV shows. They can also discover lists created by other users, and see how their lists compare with the community.
1. Reviews and ratings: Users can write reviews and rate movies and TV shows they've watched. They can also view other users reviews and ratings to help them decide what to watch next.
1. News and articles: The website also includes news, interviews and articles about movies and TV shows.
1. Community: The website also has a community aspect where users can join groups, create discussions, and share their thoughts on movies and TV shows with other users.
1. Discover: Users can discover new movies and TV shows based on their preferences and watch history.

A TMDB web client might focus on the first 5 of these features, leaving features 6-8 to the official site. To an extent, clients are also limited by what the API provides.

## Movies app primary features

### Views

**Popular Movies View:**

-  Allows users to browse a list of popular movies from TMDB.
-  The view should support pagination (preferred) or infinite scroll to allow users to easily browse through a large number of movies.
-  Each movie in the list should display the movie's title, poster and rating (stars).
-  Users should be able to click on a movie to view more details.

**Individual Movie View:**

-  Allows users to view detailed information about a specific movie.
-  The view should display the movie's title, poster, release date, overview, runtime, and genre.
-  Users should be able to view the cast and crew of the movie.
-  Users should be able to view recommendations for similar movies.

**Cast Member/Actor View:**

-  Allows users to view the details of a specific cast member or actor.
-  The view should display the cast member's/actor's name, profile picture, and a brief overview of their career.
-  Users should be able to view a list of movies in which the cast member/actor has appeared.

**Genres View:**

-  Allows users to browse movies by genre. 
-  The view should have options for popular movies, TV shows, and more.
-  Users should be able to filter movies by genre.

**Search View:**

-  Allows users to search for movies by title, cast, or keywords.
-  The search results should be paginated to allow users to easily browse through a large number of movies.
-  Users should be able to filter and sort the search results.

**Authentication:**

-  Allows users to log in and authenticate their account with TMDB.
-  When logged in, users will be able to use the list management feature(s).
-  Users should be able to log out of their account.

**Lists:**

-  Allows users to create new lists of their favorite movies.
-  Users should be able to view all of their saved lists.
-  Users should be able to add, remove, and edit movies in their lists.
-  Users should be able to share a link to any of their saved lists.

Note: This is a general guideline, additional features and design can be added as per the requirement.

### Responsive Design

[Responsive design](https://web.dev/responsive-web-design-basics/) is a web development approach that involves using CSS media queries, flexible grid-based layout and flexible images to adapt the layout and appearance of a website to different screen sizes and resolutions. By using responsive design, the Movies application built using TMDB can ensure that it looks good and is easy to use on both mobile and desktop devices, providing a seamless user experience for users regardless of the device they are using.  

Here are a few ways a Movies application built using TMDB might use responsive design to look good on both mobile and desktop devices:

1. Flexible grid-based layout: The application would use a flexible grid-based layout that adjusts the number and width of columns based on the screen size. This would ensure that the layout of the movie listings and other elements adapts to the size of the screen and is easy to navigate on both mobile and desktop devices.
1. Flexible images: The application would use flexible images that adjust their size and resolution based on the screen size and resolution. This would ensure that images look good and load quickly on both mobile and desktop devices.
1. CSS media queries: The application would use CSS media queries to apply different styles based on the screen size and resolution. For example, it could use different font sizes and spacing for text, different button sizes and layouts, and different image sizes based on the screen size.
1. Mobile-first design: The application would be designed with a mobile-first approach, which means that it would prioritize the mobile experience first, and then adapt the layout and functionality for larger screens. This will ensure that the application is easy to use and navigate on mobile devices.
1. Touch-friendly interface: The application would have a touch-friendly interface with large buttons and touch targets, making it easy to use on mobile devices

Where possible, it is encouraged to follow the approach taken in the [Next.js movies application](https://next-movies-zeta.vercel.app/?category=Popular&page=1) for a perspective on the numbers. For example, the total movie poster columns for desktop could be 4 for most 15" desktop screens, switching to 2 for mobile devices.   

The specification does not prescribe whether to use CSS Grid or Flexbox, but rather to use the best tool for the job which may include both.  

### Navigation

A navigation drawer for a Movies application using TMDB would likely be a slide-out menu that can be accessed from a button or icon in the app's user interface. It would have two sections of links: "Discover" and "Genres". 

The "Discover" section would have links to popular movies, top rated movies, and upcoming movies. 

The "Genres" section would have links to different movie genres, such as action, adventure, comedy, etc. Clicking on any of these links would take the user to the specific view for that category, such as a list of popular movies or a list of movies in a specific genre.

### Light/Dark Mode

Dark mode is becoming a popular feature in applications as it provides a more comfortable reading experience for users and also is more energy efficient for devices with AMOLED displays.

A light/dark mode feature for a movie application would allow users to switch between a light and a dark color scheme for the application's interface.  
In light mode, the background color of the application would be a light color such as white or off-white, and text and other interface elements would be in darker colors such as black or dark gray. This mode is intended to be used during the day and in well-lit environments.  

In dark mode, the background color of the application would be a dark color such as black or dark gray, and text and other interface elements would be in lighter colors such as white or light gray. This mode is intended to be used at night or in low-light environments, as it reduces the amount of glare and reduces the strain on the eyes.  

Users can switch between the two modes by clicking on a switch button or through settings page. It's also possible to set the application to automatically switch between modes based on the time of day or the device's system settings.  
While not perfect, the color scheme used in [this Next.js example](https://next-movies-zeta.vercel.app/?category=Popular&page=1) is a good baseline to build on.


### URL Structure

Ideally, all Movie applications follow a very similar URL schema.

The URL structure for the TMDB (The Movie Database) website uses the following format:

-  [https://www.themoviedb.org/](https://www.themoviedb.org/) - This is the base URL for the website.
-  [https://www.themoviedb.org/movie/[movie_id]](https://www.themoviedb.org/movie/%5Bmovie_id%5D) - This is the URL structure for accessing a specific movie's page, where [movie_id] is replaced with the ID of the movie.
-  [https://www.themoviedb.org/person/[person_id]](https://www.themoviedb.org/person/%5Bperson_id%5D) - This is the URL structure for accessing a specific person's page, where [person_id] is replaced with the ID of the person.
-  [https://www.themoviedb.org/tv/[tv_id]](https://www.themoviedb.org/tv/%5Btv_id%5D) - This is the URL structure for accessing a specific TV show's page, where [tv_id] is replaced with the ID of the TV show.
-  [https://www.themoviedb.org/discover](https://www.themoviedb.org/discover) - This is the URL for the discover page where you can browse through the database based on various filter and sorting options.

While existing applications loosely follow a schema such as the below, aligning on a very similar schema to the original site may be preferable.

* https://angular-movies-a12d3.web.app/list/category/popular
* https://angular-movies-a12d3.web.app/list/category/top_rated
* https://angular-movies-a12d3.web.app/list/category/upcoming
* https://angular-movies-a12d3.web.app/list/genre/18
* https://angular-movies-a12d3.web.app/detail/movie/536554
* https://angular-movies-a12d3.web.app/detail/person/3131



### Performance optimizations

Here are some performance optimizations that can be made to a web application built using the TMDB API:

1. Lazy-loading offscreen movie posters: This can be achieved by using an Image component, the `loading` attribute or a lazy-loading library such as LazySizes.js, which loads images only when they are about to enter the viewport. This reduces the initial load time of the page and improves the user experience.
1. Lazy-loading or loading-on-demand certain pieces of UI: This can be achieved by using a technique such as code splitting, where certain parts of the application are loaded only when they are needed (e.g. on demand, on scrolling into the viewport, on-interaction etc).
1. Lazy-loading offscreen carousel elements: This can be achieved by using a technique such as lazy-loading (for images) or virtualization, where only a certain number of carousel items are rendered at a time, and new items are loaded as the user navigates through the carousel.
1. Route-based code-splitting so that the code for a specific route is loaded only when the user navigates to that route.
1. Component-based code-splitting to split your code based on components, so that the code for a specific component is loaded only when that component is rendered.

These are just some examples of performance optimization techniques, and the specific implementation will depend on the application's architecture and requirements.