# spring-rest-introduction-course

## About project:
This project presents a CRUD system with Entities relations using Spring Boot Rest API. It is able to Create, List, Search, Update and Delete entity Client and entity Service Orders. The idea is to present an early development of a service-marketplace, which people can order many kinds of services such as Computer Repair, Personal Trainer, Haircutting and more.

## Things I learned from this course and Important Notes:

#### MVC Pattern (Model-View-Controller)

- The Model contains pure application data. It contains no logic on how to present the data to a user. It's job is to manage the data rules and logic.
It receives any user input from Controller

- The View takes data from Model and presents to the User in a friendly interface

- The Controller receives inputs from user and use these inputs to manipulate the data based on Model logics and rules.
It mapps and directs requests from users to Services. Those Services will handle these requests based on their business rules, manipulate the data and finally return some response so the controller can take back this response to the View Layer

#### Used Features

- Flyway: execute SQL queries and migrations

- RequestMapping: used on Controllers to handle requests from users. Most used Mappings are @GetMapping, @PostMapping, @PutMapping and @DeleteMapping

- Bean Validation: Create validations for the data (such as @NotBlank, @Email, @Size(max=20)). It's also necessary to insert @Valid on called Controller Method.

@Valid: Marks a property, method parameter or method return type for validation cascading. What goes with @Valid will check further validations from Entities.
Example:

```	
// OrdemServico Controller
public OrdemServico criar(@Valid @RequestBody OrdemServico ordemServico) {
		return gestaoOrdemServico.criar(ordemServico);
	}
  
// OrdemServico Model
@NotBlank
private String descricao;
	
@NotNull
private BigDecimal preco;

```

@ConvertGroup(from = Default.class, to = ValidationGroup.GroupClass.class): Ensure that the validation are made only inside the group

```
// Model Ordem Servico
@Valid
@ConvertGroup(from = Default.class, to = ValidationGroups.ClienteId.class)
@ManyToOne
private Cliente cliente;

// Group Interface - domain.ValidationGroups.java

public interface ValidationGroups {
	public interface ClienteId { }
}

// Model Cliente Id

@NotNull(groups = ValidationGroups.class)
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;

```

- @JsonInclude: Annotation used to indicate when value of the annotated property is to be serialized. Without JsonInclude, property values are always included. By using JsonInclude is possible to specify simples exclusion rules to reduce amount of properties shown

- JpaRepository: Extends repository to support some query instructions pre-defined such as save, findAll, findById, delete and more.
Example:

```
public interface ExampleRepository extends JpaRepository<Example, Long>{

}
```
where Example is the Model.

- ModelMapper: Maps objects transforming these objects from on type to another.

