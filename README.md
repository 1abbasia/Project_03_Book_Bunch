*** Team ALA - Ahsan, Lisa, Aliaksei / 5.23.17 ***

# Book Bunch

![img](./assets/millenials_read.png)

## What is Book Bunch?

Contrary to popular belief, Millennials read more than older generations do—and more than the last generation did at the same age! An [article](https://www.theatlantic.com/technology/archive/2014/09/millennials-are-out-reading-older-generations/379934/) about the 2014 Pew Research Center report said that "Deeper connections with [books] are also often associated with key life moments such as having a child, seeking a job, being a student, and going through a situation in which research and data can help inform a decision." Soooo...basically all of your 20's! Everything on the internet is interconnected. What better place to have a list of the books you've found on forbes, ESPN, instagram, in a youtube video, amazon etc. that can help you tackle those life event than Book Bunch? 

Book Bunch is a virtual bookshelf CRUD app where users can: 
- View books on a user profile archived in the database
- Add books to the database(by searching the google books api)
- Edit books in the database, update the status of the book (read, reading, to-read), and add a review of the book
- And delete books from the database

## Technologies To Be Used
- Express (backend)
- Postgres/Pg-Promise (working with database)
- React (frontend)
- Bcrypt/sessions (for user authentication)
- Git/Github.com ()
- CSS3 (styling)
- Heroku (web hosting)

## Installation of dependencies

In the command line from the root folder run -npm install

1. Run `npm install` in the root folder and the client folder
2. in the root folder, create `.env` file and add `SECRET_KEY`. Set the secret key to anything you want
3. run `psql -f migrations_05232017.sql` in the migrations folder in db of the root folder
4. run `npm run dev` in the root folder
5. in another terminal tab run `npm start` in the client folder


## Wireframes

#### Landing on home page

![img](./assets/bookbunch_1.1.png)

#### Registration Form

![img](./assets/bookbunch_2.png)

#### Add Book/Search Page

![img](./assets/bookbunch_3.1.png)

#### User Collection Page

![img](./assets/bookbunch_4.1.png)

#### Individual Book Page

![img](./assets/bookbunch_5.1.png)


## Initial thoughts on database structure

Users.

| id | Username   | Email   | Password    | 
|--- |:----------:|:-------:| -----------:|
| 1  | 'username' | 'email' | 'password'  | 
| 2  | 'username' | 'email' | 'password'  | 
| 3  | 'username' | 'email' | 'password'  | 

Books.

| id | Title   | Author   | Genre  |   ISBN  |Description   | Rating | Image Url |  
|--- |:-------:|:--------:|:------:|:-------:|:------------:|:------:| ---------:| 
| 1  | 'title' | 'author' | 'genre'|  num    |'description' | num    | 'url'     |
| 2  | 'title' | 'author' | 'genre'|  num    |'description' | num    | 'url'     |
| 3  | 'title' | 'author' | 'genre'|  num    |'description' | num    | 'url'     |

Users_Books table.

| id | user_ref_id | book_ref_id | status   | review      | date_started  | date_finished | 
|--- |-------------:|:-----------:| :-------:|:----------:|:-------------:| -------------:|
| 1  |     1        |     1       |'Reading' | 'Loved it' | 'YYYY-MM-DD'  | 'YYYY-MM-DD'  |
| 2  |     2        |     1       | 'Read'   | 'Hated it' | 'YYYY-MM-DD'  | 'YYYY-MM-DD'  |
| 3  |     1        |     2       | 'To-Read'| 'Loved it' | 'YYYY-MM-DD'  | 'YYYY-MM-DD'  |

## Advanced Features
- notes section on individual book page
- embedded/popup book preview
- Link to amazon to purchase books
- Ability to scan isbn barcode on mobile
- Google Chrome extension for easy access to our app from anywhere the user may be surfing in the internet.

## Coding Wins
```
INSERT INTO books (title, author, genre, isbn, description, rating, image_url) 
        SELECT $1, $2, $3, $4, $5, $6, $7 
        FROM dual
        WHERE NOT EXISTS (
            SELECT * FROM books WHERE books.isbn = $4
        )
        RETURNING *
```

```
userController.destroy = (req, res) => {
  console.log('in controller to destroy');
  User.findBookEntryId(req.params.id, req.params.isbn)
    .then(entryId => {
        User.destroy(entryId[0].id, req.params.isbn)
        .then(() => {
            res.json({message: 'book entry deleted'});
        })
        .catch(err => {
            console.log(err);
            res.status(400).json(err);
        });
    })
};
```
```
date_started: book.date_started.slice(0,10)
```

## Links and Resources

- https://developers.google.com/books/
- https://developers.google.com/books/docs/v1/using#PerformingSearch
- http://developer.nytimes.com/books_api.json#/Documentation/GET/lists.%7Bformat%7D
- https://developers.google.com/books/docs/preview-wizard
- https://react-bootstrap.github.io/
- https://www.nytimes.com/books/best-sellers/?mcubz=0
- https://www.forbes.com/sites/neilhowe/2017/01/16/millennials-a-generation-of-page-turners/#255cd1fa1978
- http://www.androidauthority.com/best-ebook-ereader-apps-for-android-170696/

- https://git.generalassemb.ly/nyc-wdi-ada/ada-with-jointables


