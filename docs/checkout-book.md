# Checkout book usecase

| User: logged in librarian | System |
| --- | --- |
| clicks checkout button | shows checkout form |
| enters book details, clicks (check) button | validate, shows correct message |
|   | creates checkout record |

```mermaid
sequenceDiagram
    Actor A as Librarian
    Participant MC as MainComponent
    Participant CC as CheckoutComponent
    Participant V as ValidatorComponent
    Participant B as Book
    Participant M as Member
    Participant DF as DataFacade

    activate A
    A->>MC: checkoutBook()
    activate MC
    MC->>CC: setVisible()
    activate CC
    A->>CC: enterDetails(isbn, memberId)
    A->>CC: createCheckout()
    
    CC->>V: validate()
    activate V
    V-->CC: return
    deactivate V
    
    CC->>DF: getMembers()
    activate DF
    deactivate DF
    
    CC->>DF: getBooks()
    activate DF
    deactivate DF
    
    CC->>M: checkMember(memberId)
    activate M
    deactivate M
    
    CC->>B: checkBookAvailability(isbn)
    activate B
    deactivate B
    
    CC->>DF: updateBookDetails(book)
    activate DF
    deactivate DF
    
    CC->>DF: updateMemberDetails(checkOutRecord)
    activate DF
    deactivate DF
    
    CC->>CC: showResult()
    activate CC
    deactivate CC
    
    CC-->MC: 
    deactivate CC
    deactivate MC
    deactivate A
```