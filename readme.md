### Important Notes

#### MVC Pattern (Model-View-Controller)

- The Model contains pure application data. It contains no logic on how to present the data to a user. It's job is to manage the data rules and logic.
It receives any user input from Controller

- The View takes data from Model and presents to the User in a friendly interface

- The Controller receives inputs from user and use these inputs to manipulate the data based on Model logics and rules.
It mapps and directs requests from users to Services. Those Services will handle these requests based on their business rules, manipulate the data and finally return some response so the controller can take back this response to the View Layer

#### Some Spring Tools

- Flyway: execute SQL queries and migrations

- RequestMapping: used on Controllers to handle requests from users. Most used Mappings are @GetMapping, @PostMapping, @PutMapping and @DeleteMapping

- Bean Validation: Create validations for the data (such as @NotBlank, @Email, @Size(max=20))
