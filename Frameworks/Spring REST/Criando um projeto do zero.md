[vídeo aula](https://youtu.be/wlYvA2b1BWI?si=FqgGWu10S6EWe6ke)
https://start.spring.io/
1. Dependências:
	* Spring Web
	* Spring Data JPA
	* PostgreSQL Driver
	* Validation
	* Lombok

2. Conexão com banco de dados:
	dentro do projeto em src.main.resources. ==application.properties==
```
spring.datasource.url= jdbc:postgresql://localhost:5432/products-api
spring.datasource.username=postgres
spring.datasource.password=banco123
spring.jpa.hibernate.ddl-auto=update

spring.jpa.properties.hibernate.jdbc.lob.non_contextual_creation=true
```

3. src.main.java.com.example.springboot.models.==ProductModel==
```java
@Entity
@Table(name = "TB_PRODUCTS")
public class ProductModel implements Serializable {
	private static final long serialVersionUID = 1L; // controle de versão das classes serializadas

@Id
@GeneratedValue(strategy=GenerationType.AUTO)
@Getters
@Setters
private UUID idProduct;
private String name;
private BigDecimal value;
}
```

4. src.main.java.com.example.springboot.repositories.==ProductRepository==
```java
@Repository
public interface ProductRepository extends JpaRepository<ProductModel, UUID> {}
```

5. src.main.java.com.example.springboot.controllers.==ProductController==
```java
@RestController
public class ProductController {
	@Autowired
	ProductRepository productRepository;
}
```

6. src.main.java.com.example.springboot.dtos.==ProductRecordDto==
```java
public record ProductRecordDto(@NotBlank String name, @NotNull BigDecimal value) {
	
}
```

7. Criando o método POST
```java title:ProductController
@RestController
public class ProductController {
	@Autowired
	ProductRepository productRepository;

	@PostMapping("/products") // uri
	public ResponseEntity<ProductModel> saveProduct(@RequestBody @Valid ProductRecordDto productRecordDto) { 
	/* iniciando o método; "ResponseEntity<ProductModel>"é o retorno do método "saveProduct" que recebe como corpo da solicitação Http via POST("@ResquestBody") o "ProductRecordDto" que recebe o nome e valor(@NotBlank String name, @NotNull BigDecimal value) e entra em vigor com o "@Valid"(validação dos dados) */
		var productModel = new ProductModel(); // iniciando o "productModel" já tendo recebido o "productRecordDto" do cliente
		BeanUtils.copyProperties(productRecordDto, productModel); // conversão do dto para Model
		return ResponseEntity.status(HttpStatus.CREATED).body(productRepository.save(productModel)); // construção do retorno, com o status Created, e o corpo com o nome, valor e UUID
	}
}
```

8. Utilizar o [Postman](https://web.postman.co/workspace/f6ee18f0-9749-4c84-896f-798c2414aaf8/request/39177871-7e906c92-588f-4dbb-a72a-13cf1a1203dd?tab=body) para testar o método POST
	![[Pasted image 20241021170445.png|600]]
	retorno
	![[Pasted image 20241021170907.png|600]]
	testando o  @NotBlank
	![[Pasted image 20241021171020.png|500]]
	testando o @NotNull
	![[Pasted image 20241021171201.png|500]]

9.  Criando o método getAll
```java title:ProductController
...
@GetMapping("/products") // uri
public ResponseEntity<List<ProductMode1>> getAllProducts() { // retorna "ResponseEntity" com o corpo "<List<ProductModel>>" com o método "getAllProducts()" sem entrada;
	return ResponseEntity.status(HttpStatus.OK).body(productRepository.findAll()); // tem como retorno o "ResponseEntity" com o status OK e o corpo com a lista de todos os recursos salvos na base de daods
}
```
 10. Testando o método getAll no Postman
	 retorna os produtos salvos anteriormente com o método POST
	 ![[Pasted image 20241021172605.png|500]]

11. Criando o método getOne
```java title:ProductController
...
@GetMapping("/products/{id}")
public ResponseEntity<Object> getOneProduct(@PathVariable(value="id") UUID id) {
	Optional<ProductModel> productO = productRepository.findById(id);
	if (productO.isEmpty()) {
		return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Product not found.");
	}
	return ResponseEntity.status(HttpStatus.OK) .body(productO.get());
}
```

12.  Testando o método getOne
![[Pasted image 20241021181308.png|500]]

13.  Criando o método PUT
```java title:ProductController
...
@PutMapping("/products/{id}")
public ResponseEntitY<Object> updateProduct(@PathVariable(value="id")) UUID id, @RequestBody @Valid ProductRecordDto productRecordDto) {
	Optional<ProductModel> productO = productRepository.findById(id);
	if (productO.isEmpty()) {
		return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Product not found.");
	}
	var productModel = productO.get();
	BeanUtils.copyProperties(productRecordDto, productModel);
	return ResponseEntity.status(HttpStatus.OK).body(productRepository.save(productModel));
}
```

14. Testando o método PUT
![[Pasted image 20241022081135.png|500]]

15. Criando o método DELETE
```java title:ProductController
...
@DeleteMapping("/products/{id}")
public ResponseEntity<Object> deleteProduct(@PathVariable(value="id")) UUID id) {
	Optional<ProductModel> productO = productRepository.findById(id);
	if (productO.isEmpty()) {
		return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Product not found.");
	}
	productRepository.delete(productO.get());
	return ResponseEntity.status(HttpStatus.OK).body("Product deleted successfully.");
}
```

16. Testando o método DELETE
![[Pasted image 20241022082314.png|500]]
	tentando deletar o mesmo deletado anteriormente
![[Pasted image 20241022082354.png|500]]

17. Adicionar a dependência Hateoas
```xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-hateoas</artifactId>
</dependency>
```

18. Inserindo o Hateoas e refatorando o código getAll
```java title:ProductModel
@Entity
@Table(name = "TB_PRODUCTS")
public class ProductModel extends RepresentationModel<ProductModel> implements Serializable {
	private static final long serialVersionUID = 1L; // controle de versão das classes serializadas

@Id
@GeneratedValue(strategy= GenerationType.AUTO)
@Getters
@Setters
private UUID idProduct;
private String name;
private BigDecimal value;
}
```

refatorando
```java title:ProductController
...
@GetMapping("/products")
public ResponseEntity<List<ProductMode1>> getAllProducts() {
	List<ProductModel> productsList = productRepository.findAll();
	if(!productsList.isEmpty()) {
		for(ProductModel product : productsList) {
			UUID id = product.getIdProduct();
			product.add(linkTo(methodOn(ProductController.class).getOneProduct(id)).withSelfRel());
		}
	}
	return ResponseEntity.status(HttpStatus.OK).body(productsList);
}
...
```

19. Testando a implementação
![[Pasted image 20241022085238.png|500]]

20. Refatorando getOne
 ```java title:ProductController
...
@GetMapping("/products/{id}")
public ResponseEntity<Object> getOneProduct(@PathVariable(value="id") UUID id) {
	Optional<ProductModel> productO = productRepository.findById(id);
	if(productO.isEmpty()) {
		return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Product not found.");
	}
	productO.get().add(linkTo(methodOn(ProductController.class).getAllProducts()).withRel("Products List"));
	return ResponseEntity.status(HttpStatus.OK) .body(productO.get());
}
...
```

21. Testando getOne
![[Pasted image 20241022085921.png|500]]
