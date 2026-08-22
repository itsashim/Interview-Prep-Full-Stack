# Fat Model Thin Controller Philoshopy

It is a Design Patter,  that advocates placing business logic within the model layer while keeping controllers minimal and focused solely on handling HTTP requests and responses. 

Proponents argue this approach keeps code DRY (Don't Repeat Yourself) and makes business rules testable outside the context of a web request, as the model acts as the single source of truth for data processing and validation. 

However, this pattern is frequently criticized for leading to "God Models"—monolithic, difficult-to-maintain classes that mix persistence logic with complex business rules.  

Critics and many modern developers advocate for Thin Model, Thin Controller architectures, using Service Classes, Repositories, or Interactors to handle complex logic, thereby ensuring that models remain focused on data access while services manage application flow and business rules. 

Skinny Controllers: Responsible only for receiving input, delegating to models or services, and returning responses. 

Fat Models: Contain validations, scopes, and business methods; risks include violating the Single Responsibility Principle. 

Alternative Approach: Use Service Objects or Action Classes to encapsulate complex workflows, keeping both controllers and models slim. 