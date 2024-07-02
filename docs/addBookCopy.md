# Add a Book Copy

| Administrator            | System                                            |
|--------------------------|---------------------------------------------------|
| Enters a ISBN            | Searches book by ISBN then displays a book window |
| Clicks add a copy button | Adds a book copy                                  |


```mermaid

sequenceDiagram
    Actor L as Librarian
    participant AB as AllBookComponent
    participant SC as SystemController
    participant BC as BookComponent
    participant B as Book
    participant DB as Database
    
    activate L
    L ->> AB: searchByISBN(isbn)
    activate SC
    AB ->> SC: searchByISNB(isbn)
    SC ->> DB: getAllBook()
    activate DB
    deactivate DB
    SC ->> B: *checkISBN(isbn)
    activate B
    deactivate B
    SC ->> BC: setVisible(book)
    activate BC
    deactivate BC
    deactivate SC
    deactivate L
    
    activate L
    L ->> BC: addBookCopy(book)
    activate BC
    BC ->> SC: addBookCopy(book)
    deactivate BC
    activate SC
    SC ->> B: saveBookCopy(book)
    activate B
    deactivate B
    SC ->> DB: saveBookCopy(book)
    activate DB
    deactivate DB
    deactivate SC
    deactivate L
    
    

```
