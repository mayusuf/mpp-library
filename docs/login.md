# Login

| User                                               | System                                                                                                     |
|----------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| Enters a login credentials and clicks login button | Validates id and password then fetches user and based on the role shows main screen for admin or librarian |



```mermaid

sequenceDiagram
    Actor U as User
    participant LC as LoginComponent
    participant SC as SystemController
    participant Us as User
    participant DB as Database
    participant MC as MainComponent
    
    activate U
    U->>LC: submitLogin(id, password)
    
    activate LC
    LC->>SC: login(id, password)
    
    activate SC
    SC->>DB: readUserMap()
    activate DB
    deactivate DB
    SC->>SC: *checkId(id)
    activate SC
    deactivate SC
    SC->>Us: getPassword(password)
    activate Us
    deactivate Us
    SC->>Us: getUserRole(id)
    activate Us
    deactivate Us
    SC->>MC: showMainComponent(role)
    
    activate MC
    deactivate MC
    deactivate SC
    deactivate LC
    deactivate U
    
    



```