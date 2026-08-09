# MVC architecture
=> big goals of MVC is to seperate business logic and application logic

- Model
 concerned with business logic and application data

- Controller
handle application req interact with model and send back res to users, application logic

- View
if we build SSR, templates to generate a view , presentation logic


- easy to maintain and scale

```mermaid
\


flowchart LR
    A[Client Request] --> B[Router]

    subgraph Application_Logic
        B --> C[Controller]
    end

    subgraph Business_Logic
        D[Model]
    end

    subgraph Presentation_Logic
        E[View]
    end

    C -->|Read / Write Data| D
    D -->|Return Data| C

    C -->|Render View| E
    E -->|Rendered HTML| C

    C --> F[HTTP Response]
```



# Application Logic
    - managing req and res, doesn't think about business logic
    - bridge between model and view layers

# Business Logic
   - codes that is directly related to business logic
   - examples: in context with tours app
      - create new tours in the db
      - checking if users password is correct
      - validating users input
      - ensuring who bought a tour and review it

it is almost impossible to seperate app and business logic but we should do our best efforts to seperate them