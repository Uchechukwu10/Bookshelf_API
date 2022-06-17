# API DOCUMENTATION
## Getting Started

Base URL: At present, this API does not have a base URL. It can only be run locally at the default address `https://localhost:5000`

Authentication: This version does not require any form of authentication at this level.

## Error Handling
Errors are returned as JSON objects in this format:

```

{
    'Success': 'False',
    'error': 404,
    'message': 'resource not found'
}

```
You will receive errors of three types which include:
404: Resource not found
400: Bad request
422: Unproccesable
405: Method not allowed

## Endpoint Library
### GET /books
- General
  - Returns a list of all books from the database alongside a success value of 'True' and the total number of books in the database.
  - The response is paginated and displays 8 books per page. The desired page must be included in your request argument.

- Sample Request
    Here is an example request:
    `curl http://localhost:5000/books?page=2`

The above request will give the following response:


```
    {
  "books": [
    {
      "author": "Stephen King",       
      "id": 1, 
      "rating": 5, 
      "title": "The Outsider: A Novel"
    }, 
    {
      "author": "Lisa Halliday",      
      "id": 2, 
      "rating": 4, 
      "title": "Asymmetry: A Novel"
    }, 
    {
      "author": "Kristin Hannah", 
      "id": 3, 
      "rating": 4, 
      "title": "The Great Alone"
    }, 
    {
      "author": "Tara Westover", 
      "id": 4, 
      "rating": 5, 
      "title": "Educated: A Memoir"
    }, 
    {
      "author": "Jojo Moyes", 
      "id": 5, 
      "rating": 5, 
      "title": "Still Me: A Novel"
    }, 
    {
      "author": "Leila Slimani", 
      "id": 6, 
      "rating": 2, 
      "title": "Lullaby"
    }, 
    {
      "author": "Amitava Kumar", 
      "id": 7, 
      "rating": 5, 
      "title": "Immigrant, Montana"
    },
    {
      "author": "Madeline Miller",
      "id": 8,
      "rating": 5,
      "title": "CIRCE"
    }
  ],
  "success": true,
  "total_books": 16
    }


```


### POST /books

- General
  - Creates a book using the values of title, author and rating from the passed json. It returns a success message, the created book id, a list of all the books in the database after the creation and the total number of books.
  - The list of books returned is still paginated and a page argument can be added to the request indicating the page to be displayed.

- Sample request
  Here is an example request:

  `curl -X POST -H "Content-Type: application/json" -d '{"title": "The Mad Men of Lagos", "author": "Uche Nwankwo", "rating": "4"}' http://localhost:5000/books?page=2`

The above request will give the following response:


```
        {
       "books": [
        {
          "author": "Gina Apostol",
          "id": 9,
          "rating": 5,
          "title": "Insurrecto: A Novel"
        },
        {
          "author": "Tayari Jones",
          "id": 10,
          "rating": 5,
          "title": "An American Marriage"
        },
        {
          "author": "Jordan B. Peterson",
          "id": 11,
          "rating": 5,
          "title": "12 Rules for Life: An Antidote to Chaos"
        },
        {
          "author": "Kiese Laymon",
          "id": 12,
          "rating": 1,
          "title": "Heavy: An American Memoir"
        },
        {
          "author": "Emily Giffin",
          "id": 13,
          "rating": 4,
          "title": "All We Ever Wanted"
        },
        {
          "author": "Jose Andres",
          "id": 14,
          "rating": 4,
          "title": "We Fed an Island"
        },
        {
          "author": "Gregory Blake Smith",
          "id": 16,
          "rating": 2,
          "title": "The Maze at Windermere"
        },
        {
          "author": "Uche Nwankwo",
          "id": 24,
          "rating": 4,
          "title": "The Mad Men of Lagos"
        }
      ],
      "created": 24,
      "success": true,
      "total_books": 16
    }

```

### PATCH /books/{book_id}

- General
  - Updates the rating of an already existing book. This request must include a json object that contains a 'rating' key and the new rating as the value.
  - It returns a json with a success message and the id of the book updated

- Sample request
    Here is an example request:
    `curl -X PATCH -H "Content-Type: application/json" -d '{"rating": "1"}' http://localhost:5000/books/15`

The above request will give the following response:

```
      {
      "id": 15,
      "success": true
      }
      
 ```

### DELETE /books/{book_id}

  - General
      - Deletes a single book from the list of books in our database and returns a list of all the books left. It also returns a json containing a success message, the deleted book id and the number of books left in our database.
      - The response will still be paginated and each page contains 8 books.

  - Sample Request
      Here is an example request:
      `curl -X DELETE http://localhost:5000/books/15`

  The above request will give the following response:

```
      {
    "books": [
      {
        "author": "Stephen King",       
        "id": 1,
        "rating": 5,
        "title": "The Outsider: A Novel"
      },
      {
        "author": "Lisa Halliday",      
        "id": 2,
        "rating": 4,
        "title": "Asymmetry: A Novel"
      },
      {
        "author": "Kristin Hannah",
        "id": 3,
        "rating": 4,
        "title": "The Great Alone"
      },
      {
        "author": "Tara Westover",
        "id": 4,
        "rating": 5,
        "title": "Educated: A Memoir"
      },
      {
        "author": "Jojo Moyes",
        "id": 5,
        "rating": 5,
        "title": "Still Me: A Novel"
      },
      {
        "author": "Leila Slimani",
        "id": 6,
        "rating": 2,
        "title": "Lullaby"
      },
      {
        "author": "Amitava Kumar",
        "id": 7,
        "rating": 5,
        "title": "Immigrant, Montana"
      },
      {
        "author": "Madeline Miller",
        "id": 8,
        "rating": 5,
        "title": "CIRCE"
      }
    ],
    "deleted": 15,
    "success": true,
    "total_books": 15
    }

```






