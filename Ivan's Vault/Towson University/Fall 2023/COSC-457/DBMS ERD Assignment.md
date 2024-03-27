
```mermaid
classDiagram
    class STATE {
        +State_Name: String
        Region: String
    }
    
    class CONGRESS_PERSON {
        +Congress_Person_ID: Number
        Name: String
        District: String
        Start_date: Date
        Party: String
        State_Name: String
    }
    
    class BILL {
        +Bill_ID: Number
        Bill_name: String
        Date_of_vote: Date
        Passed_or_failed: String
    }
    
    class VOTE {
        +Vote_ID: Number
        Congress_Person_ID: Number
        Bill_ID: Number
        Vote: String
    }

    class SPONSORSHIP {
        Sponsor_ID: Number
        Bill_ID: Number
    }

    STATE "1" --> "N" CONGRESS_PERSON: contains
    CONGRESS_PERSON --|> SPONSORSHIP: sponsors
    SPONSORSHIP "0..*" --|> "N" BILL: is sponsored by
    CONGRESS_PERSON "1" --> "N" VOTE: votes
    BILL "1" --> "N" VOTE: receives


```



```mermaid
classDiagram
    class STATE {
        «PK» State_Name: String
        Region: String
    }
    
    class CONGRESS_PERSON {
        «PK» Congress_Person_ID: Number
        Name: String
        District: String
        Start_Date: Date
        Party: String
        «FK» State_Name: String
    }
    
    class BILL {
        «PK» Bill_ID: Number
        Bill_name: String
        Date_of_vote: Date
        Passed_or_failed: String
    }
    
    class VOTE {
        «PK» Vote_ID: Number
        «FK» Congress_Person_ID: Number
        «FK» Bill_ID: Number
        Vote: String
    }
    
    class SPONSORSHIP {
        «FK» Sponsor_ID: Number
        «FK» Bill_ID: Number
    }

    STATE "1" --> "N" CONGRESS_PERSON: contains
    CONGRESS_PERSON "1" --> "N" VOTE: votes
    BILL "1" --> "N" VOTE: receives
    CONGRESS_PERSON "1" --> "N" SPONSORSHIP: sponsors
    BILL "1" <-- "N" SPONSORSHIP: is sponsored by

```



note right of CONGRESS_PERSON: + indicates Primary Key
note right of STATE: One STATE can be represented by multiple CONGRESS_PERSON
note right of CONGRESS_PERSON: One CONGRESS_PERSON can sponsor and vote on multiple BILLs
note right of BILL: One BILL can be sponsored by and voted on by multiple CONGRESS_PERSONs

```mermaid
classDiagram
    class STATE{
        +Name: String
        Region: String
    }
    
    class CONGRESS_PERSON{
        +Name: String
        District: String
        Start_date: Date
        Party: String
    }
    
    class BILL{
        +Bill_name: String
        Date_of_vote: Date
        Passed_or_failed: String
    }
    
    STATE --|> CONGRESS_PERSON: REPRESENTS
    CONGRESS_PERSON --|> BILL: SPONSORED_BY
    CONGRESS_PERSON -- BILL: VOTED_ON
    BILL: Vote


```

```mermaid
erDiagram
    STATE ||--o{ CONGRESS_PERSON : represents
    STATE {
        string Name
        string Region
    }
    CONGRESS_PERSON ||--o{ BILL : sponsors
    CONGRESS_PERSON ||--o{ VOTE : casts
    CONGRESS_PERSON {
        string Name
        string District
        date Start_date
        string Party
    }
    BILL ||--o{ VOTE : is_voted_on
    BILL {
        string Bill_name
        date Date_of_vote
        string Passed_or_failed
    }
    VOTE {
        string Vote
    }

```