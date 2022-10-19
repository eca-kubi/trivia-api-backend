# Backend - Trivia API

## Setting up the Backend

### Install Dependencies

1. **Python 3.8** 

2. **PIP Dependencies**  install the required dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

#### Key Pip Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in `app.py`and can reference `models.py`.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross-origin requests from our frontend server.

### Set up the Database

With Postgres running, create a `trivia` database:

```bash
createdb -U postgres trivia
```

Populate the database using the `trivia.psql` file provided. From the `backend` folder in terminal run:

```bash
psql -U postgres trivia < trivia.psql
```

### Run the Server

To run the server, execute:

```bash
flask --app flaskr --debug run --reload 
```

## Documentation

>_**Tip 1**_: Objects returned by endpoints will have a `success` boolean property with a value of `true` or `false` to indicate whether the operation was successful or failed respectively.
#####
> _**Tip 2**_: Text in angle brackets `<>` are placeholders. You will need to replace them with real values

`GET '/questions?page=<page_number>'`

- For returning a paginated list of questions. The page number is passed as url parameter.
- Request Parameters: `page: int` argument for specifying the page number
- Returns: List of questions, total number of questions, current category, and categories

```json
{
  "categories": [
    {
      "id": 1,
      "type": "Science"
    },
    {
      "id": 2,
      "type": "Art"
    },
    {
      "id": 3,
      "type": "Geography"
    },
    {
      "id": 4,
      "type": "History"
    },
    {
      "id": 5,
      "type": "Entertainment"
    },
    {
      "id": 6,
      "type": "Sports"
    }
  ],
  "current_category": null,
  "questions": [
    {
      "answer": "Maya Angelou",
      "category": 4,
      "difficulty": 2,
      "id": 5,
      "question": "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
    },
    {
      "answer": "Muhammad Ali",
      "category": 4,
      "difficulty": 1,
      "id": 9,
      "question": "What boxer's original name is Cassius Clay?"
    },
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },
    {
      "answer": "Tom Cruise",
      "category": 5,
      "difficulty": 4,
      "id": 4,
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    },
    {
      "answer": "Brazil",
      "category": 6,
      "difficulty": 3,
      "id": 10,
      "question": "Which is the only team to play in every soccer World Cup tournament?"
    },
    {
      "answer": "George Washington Carver",
      "category": 4,
      "difficulty": 2,
      "id": 12,
      "question": "Who invented Peanut Butter?"
    },
    {
      "answer": "Lake Victoria",
      "category": 3,
      "difficulty": 2,
      "id": 13,
      "question": "What is the largest lake in Africa?"
    },
    {
      "answer": "The Palace of Versailles",
      "category": 3,
      "difficulty": 3,
      "id": 14,
      "question": "In which royal palace would you find the Hall of Mirrors?"
    },
    {
      "answer": "Agra",
      "category": 3,
      "difficulty": 2,
      "id": 15,
      "question": "The Taj Mahal is located in which Indian city?"
    },
    {
      "answer": "Escher",
      "category": 2,
      "difficulty": 1,
      "id": 16,
      "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
    }
  ],
  "success": true,
  "total_questions": 16
}
```

`GET '/categories'`

- Fetches categories as array of objects.
- Request Parameters: None
- Returns: An object with `categories` as an array of category objects. Each category object has two keys: `id` and `type`, representing the category's unique id and name respectively.

```json
{
  "categories": [
    {
      "id": 1,
      "type": "Science"
    },
    {
      "id": 2,
      "type": "Art"
    },
    {
      "id": 3,
      "type": "Geography"
    },
    {
      "id": 4,
      "type": "History"
    },
    {
      "id": 5,
      "type": "Entertainment"
    },
    {
      "id": 6,
      "type": "Sports"
    }
  ],
  "success": true
}
```

`DELETE '/questions/<question_id>'`

- Deletes a question whose id is `question_id`.
- Request Argument: `question_id: int`
- Returns: An object with the id of the deleted question on success.

```json
{
  "deleted": 5,
  "success": true
}
```

`POST '/questions`

- Posts a new question
- Request Payload: an object with the question, answer, category, and difficulty
```json
{
    "question":"What is the tallest mountain on earth?",
    "answer":"Mt Everest",
    "category": 2,
    "difficulty": 1
}
```
- Returns: An object with the new question on success
```json
{
  "question": {
    "answer": "Mt Everest",
    "category": 2,
    "difficulty": 1,
    "id": 25,
    "question": "What is the tallest mountain on earth?"
  },
  "success": true
}

```

`GET '/categories/<category_id>/questions?page=<page_number>`

- Fetch questions based on category specified by `category_id`. Page number may optionally be specified via `page` url parameter.
- Request Parameters: `category_id: int`: to specify category id and optional `page: int` parameter for page number
- Returns all questions from category specified by `category_id`, current category and the total number of questions
```json
{
  "current_category": 1,
  "questions": [
    {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    {
      "answer": "Alexander Fleming",
      "category": 1,
      "difficulty": 3,
      "id": 21,
      "question": "Who discovered penicillin?"
    },
    {
      "answer": "Blood",
      "category": 1,
      "difficulty": 4,
      "id": 22,
      "question": "Hematology is a branch of medicine involving the study of what?"
    }
  ],
  "success": true,
  "total_questions": 3
}

```

`POST '/questions`

- Endpoint to get questions based on a search term. It returns any questions for whom the search term is a substring.
- Request Payload: An object with property `search_term` to specify the search keyword.
```json
{
  "search_term": "<searchTerm>"
}
```
- Returns: An object with an array of the matched questions, current category, and total number of questions on success
```json
{
  "current_category": null,
  "questions": [],
  "success": true,
  "total_questions": 0
}

```

`POST '/quizzes'`

- This endpoint takes a category and ids of previous questions and returns random questions within the given category. Question returned will be different from previous questions. 
- Request Payload: An object with the current category id, and an array of ids of previous questions.
```json
{
  "previous_questions": ["<question_id1>", "<question_id2>"],
  "quiz_category": "<category_id>"
}
```
- Returns a question
```json
{
  "question": {
    "answer": "The Liver",
    "category": 1,
    "difficulty": 4,
    "id": 20,
    "question": "What is the heaviest organ in the human body?"
  },
  "success": true
}
```
