# Add a new member usecase

| User: logged in administrator    | System |
|----------------------------------| --- |
| clicks add new member button     | displays the form for the member detail fields |
| fills out the details and submit | validates the details, saves them to database, shows results |

```mermaid
sequenceDiagram
    Actor A as Admin
    Participant MC as MainComponent
    Participant AC as NewMemberComponent
    Participant V as Validator
    PARTICIPANT SC as SystemController
    Participant DB as DataFacade

    activate A
    A->>MC: addNew()
    activate MC
    MC->>AC: setVisible()
    activate AC
    A->>AC: enter details
    A->>AC: submit()
    
    AC->>V: *validate()
    activate V
    deactivate V
    
    AC->>SC: saveMember(member)
    activate SC
    SC->>DB: saveMember(member)
    activate DB
    deactivate DB
    deactivate SC
    
    AC->>AC: refresh()
    activate AC
    deactivate AC
    
    AC-->AC: message
    deactivate AC
    deactivate MC
    deactivate A
```