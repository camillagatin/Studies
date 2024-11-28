## Introdução ao Tratamento e Modelagem de Erros

**O que são exceções e por que são importantes?**

Em programação, exceções são eventos que interrompem o fluxo normal de execução de um programa. Elas podem ocorrer por diversos motivos, como erros de entrada, falhas em operações de I/O, problemas de conexão com banco de dados, etc. O tratamento adequado de exceções é crucial para garantir a robustez e a estabilidade de uma aplicação.

**Por que modelar erros?**

Modelar erros significa criar uma estrutura para representar diferentes tipos de erros que podem ocorrer em sua aplicação. Isso permite que você:

* **Identifique o erro:** Ao modelar um erro, você define uma classe específica para representá-lo, facilitando a identificação da causa raiz do problema.
* **Comunique o erro:** Você pode criar mensagens de erro personalizadas e informativas para o usuário ou para outros sistemas.
* **Tome ações específicas:** Ao capturar uma exceção específica, você pode executar ações de recuperação ou notificar outros sistemas.

**Tratamento de exceções em Java**

Java possui um mecanismo robusto para lidar com exceções, baseado em blocos `try`, `catch` e `finally`.

* **try:** Envolve o código que pode gerar uma exceção.
* **catch:** Captura exceções específicas e executa o código de tratamento.
* **finally:** Executa um bloco de código independentemente de ocorrer uma exceção ou não.

**Tratamento de exceções em Spring Boot**

O Spring Boot oferece diversas ferramentas para facilitar o tratamento de exceções em suas aplicações:

* **@ControllerAdvice:** Anotação que marca uma classe como um manipulador global de exceções.
* **@ExceptionHandler:** Anotação que marca um método para tratar um tipo específico de exceção.
* **ResponseEntityExceptionHandler:** Classe base para criar manipuladores de exceções personalizados.
* **ResponseStatusException:** Exceção que permite definir um status HTTP específico para uma exceção.

**Criando exceções personalizadas**

É altamente recomendável criar suas próprias exceções para representar os erros específicos da sua aplicação. Isso torna o código mais legível e facilita a depuração.

**Exemplo:**

```java
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

**Exemplo de tratamento de exceção em um controlador Spring MVC:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        User user = userService.getUserById(id);
        if (user == null) {
            throw new ResourceNotFoundException("User not found");
        }
        return user;
    }
}
```

**Exemplo de manipulador global de exceções:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleResourceNotFoundException(ResourceNotFoundException ex) {
        return ResponseEntity.notFound().body(ex.getMessage());
    }
}
```

**Melhores práticas**

* **Seja específico:** Crie exceções personalizadas para representar diferentes tipos de erros.
* **Use exceções para condições excepcionais:** Não use exceções para controlar o fluxo normal do programa.
* **Trate exceções o mais próximo possível da fonte:** Isso facilita a depuração e evita propagação de exceções não tratadas.
* **Logue as exceções:** Isso ajuda a identificar e corrigir problemas em produção.
* **Evite exceções verificadas:** Use exceções não verificadas (RuntimeExceptions) para erros que não podem ser recuperados.
---
## Lançando Exceções Customizadas Anotadas com @ResponseStatus
**O que é @ResponseStatus?**

A anotação `@ResponseStatus` do Spring permite que você defina o status HTTP que será retornado quando uma exceção específica é lançada. Isso é especialmente útil em APIs REST, onde o status HTTP é crucial para comunicar o resultado de uma requisição ao cliente.

**Por que usar exceções customizadas com @ResponseStatus?**

* **Mensagens de erro personalizadas:** Você pode fornecer mensagens de erro mais informativas e específicas para cada tipo de exceção.
* **Códigos de status HTTP precisos:** Ao associar um status HTTP específico a cada exceção, você garante que o cliente receba a resposta correta.
* **Tratamento centralizado de exceções:** Com `@ControllerAdvice`, você pode criar um tratamento centralizado para todas as exceções, simplificando a lógica de tratamento de erros.

**Como criar e usar exceções customizadas com @ResponseStatus:**

1. **Crie uma exceção personalizada:**

   ```java
   @ResponseStatus(HttpStatus.NOT_FOUND)
   public class ResourceNotFoundException extends RuntimeException {
       public ResourceNotFoundException(String message) {
           super(message);
       }
   }
   ```

2. **Lance a exceção em seu código:**

   ```java
   @Service
   public class UserService {
       public User getUserById(Long id) {
           Optional<User> user = userRepository.findById(id);
           return user.orElseThrow(() -> new ResourceNotFoundException("User not found"));
       }
   }
   ```

3. **Crie um `@ControllerAdvice` para tratar a exceção:**

   ```java
   @ControllerAdvice
   public class GlobalExceptionHandler {
       @ExceptionHandler(ResourceNotFoundException.class)
       public ResponseEntity<String> handleResourceNotFoundException(ResourceNotFoundException ex) {
           return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
       }
   }
   ```

**Exemplo completo:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        return userService.getUserById(id);
    }
}

@Service
public class UserService {
    public User getUserById(Long id) {
        Optional<User> user = userRepository.findById(id);
        return user.orElseThrow(() -> new ResourceNotFoundException("User not found"));
    }
}

@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}

@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleResourceNotFoundException(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

**Explicação:**

* A anotação `@ResponseStatus(HttpStatus.NOT_FOUND)` na classe `ResourceNotFoundException` indica que, quando essa exceção for lançada, o status HTTP 404 (Not Found) será retornado.
* O `@ControllerAdvice` define um manipulador global de exceções. O método `handleResourceNotFoundException` é chamado quando ocorre uma `ResourceNotFoundException`.
* O `ResponseEntity` retornado contém o status HTTP 404 e a mensagem da exceção.

**Vantagens:**

* **Claridade:** Facilita a compreensão de como a aplicação deve responder a diferentes tipos de erros.
* **Personalização:** Permite criar mensagens de erro personalizadas para cada tipo de exceção.
* **Reutilização:** O `@ControllerAdvice` centraliza o tratamento de exceções, evitando a duplicação de código.
* **Integração com APIs REST:** Garante que a API retorne os códigos de status HTTP corretos.

**Considerações adicionais:**

* **Hierarquia de exceções:** Você pode criar uma hierarquia de exceções para agrupar exceções relacionadas.
* **Exceções personalizadas com parâmetros:** Adicione construtores com parâmetros para passar informações adicionais para a exceção.
* **Tratamento de exceções específicas:** Crie `@ExceptionHandler` para tratar diferentes tipos de exceções.
* **Logging:** Use um framework de logging para registrar as exceções e facilitar a depuração.
---
## Lançando Exceções do Tipo ResponseStatusException no Spring Boot

**O que é ResponseStatusException?**

A `ResponseStatusException` é uma classe especial de exceção no Spring que permite associar diretamente um status HTTP a uma exceção. Isso facilita a criação de respostas HTTP personalizadas para diferentes tipos de erros em sua aplicação. Ao lançar uma `ResponseStatusException`, você define explicitamente o código de status HTTP que será retornado ao cliente, juntamente com uma mensagem de erro opcional.

**Por que usar ResponseStatusException?**

* **Clareza:** Torna o código mais conciso e claro, pois o status HTTP está diretamente ligado à exceção.
* **Flexibilidade:** Permite definir diferentes códigos de status e mensagens de erro para cada tipo de exceção.
* **Integração com Spring MVC:** Se integra perfeitamente com o mecanismo de tratamento de exceções do Spring MVC, simplificando a criação de APIs REST.

**Como usar ResponseStatusException:**

1. **Importar a classe:**

   ```java
   import org.springframework.http.HttpStatus;
   import org.springframework.web.server.ResponseStatusException;
   ```

2. **Lançar a exceção:**

   ```java
   @GetMapping("/users/{id}")
   public User getUserById(@PathVariable Long id) {
       Optional<User> user = userRepository.findById(id);
       return user.orElseThrow(() -> new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found"));
   }
   ```

   Neste exemplo, se o usuário não for encontrado, uma `ResponseStatusException` com status 404 (Not Found) será lançada.

**Exemplo completo com tratamento de exceções:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        Optional<User> user = userRepository.findById(id);
        return user.orElseThrow(() -> new ResponseStatusException(HttpStatus.NOT_FOUND, "User not found"));
    }
}

@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResponseStatusException.class)
    public ResponseEntity<String> handleResponseStatusException(ResponseStatusException ex) {
        return ResponseEntity.status(ex.getStatus()).body(ex.getMessage());
    }
}
```

**Vantagens:**

* **Simplifica o tratamento de exceções:** Ao centralizar o tratamento de `ResponseStatusException` em um `@ControllerAdvice`, você evita a repetição de código.
* **Personalização:** Permite criar respostas HTTP personalizadas para diferentes cenários de erro.
* **Integração com outras ferramentas:** Funciona bem com ferramentas de documentação de APIs como Swagger, que podem gerar automaticamente a documentação das respostas de erro.

**Comparação com exceções customizadas:**

| Característica | ResponseStatusException | Exceção customizada com @ResponseStatus |
|---|---|---|
| Simplicidade | Mais simples de usar | Requer mais código |
| Flexibilidade | Menos flexível para personalizar a resposta | Mais flexível para personalizar a resposta |
| Integração com Spring | Integração nativa | Requer um `@ExceptionHandler` personalizado |

**Quando usar cada uma:**

* **ResponseStatusException:** Ideal para exceções simples que mapeiam diretamente para um status HTTP.
* **Exceção customizada com @ResponseStatus:** Ideal quando você precisa de mais controle sobre a resposta, como incluir informações adicionais na mensagem de erro ou personalizar a estrutura da resposta.

**Considerações adicionais:**

* **Hierarquia de exceções:** Você pode criar uma hierarquia de exceções customizadas que estendam `ResponseStatusException` para organizar melhor suas exceções.
* **Mensagens de erro personalizadas:** Inclua mensagens de erro detalhadas para ajudar na depuração.
* **Tratamento de exceções específicas:** Crie `@ExceptionHandler` específicos para tratar diferentes tipos de `ResponseStatusException`.
* **Logging:** Use um framework de logging para registrar as exceções e facilitar a análise de problemas.
---
## Estendendo a ResponseStatusException no Spring Boot

**Por que estender a ResponseStatusException?**

Ao estender a classe `ResponseStatusException`, você pode criar exceções personalizadas que encapsulam informações específicas sobre o erro, permitindo um tratamento mais granular e informativo. Isso é especialmente útil quando você precisa:

* **Criar uma hierarquia de exceções:** Organizar suas exceções em uma estrutura hierárquica, facilitando a manutenção e o tratamento.
* **Adicionar campos personalizados:** Incluir informações adicionais na exceção, como códigos de erro personalizados, detalhes técnicos ou informações de contexto.
* **Personalizar a mensagem de erro:** Criar mensagens de erro mais específicas e informativas para o usuário final.

**Como estender a ResponseStatusException:**

```java
import org.springframework.http.HttpStatus;
import org.springframework.web.server.ResponseStatusException;

public class CustomNotFoundException extends ResponseStatusException {

    private final String errorCode;

    public CustomNotFoundException(String errorCode, String reason) {
        super(HttpStatus.NOT_FOUND, reason);
        this.errorCode = errorCode;
    }

    public String getErrorCode() {
        return errorCode;
    }
}
```

Neste exemplo, criamos uma exceção personalizada `CustomNotFoundException` que herda de `ResponseStatusException`. Adicionamos um campo `errorCode` para armazenar um código de erro personalizado.

**Utilizando a exceção personalizada:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        Optional<User> user = userRepository.findById(id);
        return user.orElseThrow(() -> new CustomNotFoundException("USER_NOT_FOUND", "User not found"));
    }
}
```

**Tratamento da exceção:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(CustomNotFoundException.class)
    public ResponseEntity<ErrorDto> handleCustomNotFoundException(CustomNotFoundException ex) {
        ErrorDto errorDto = new ErrorDto(ex.getErrorCode(), ex.getMessage());
        return ResponseEntity.status(ex.getStatus()).body(errorDto);
    }
}
```

**Vantagens de estender a ResponseStatusException:**

* **Reutilização:** Crie uma base de exceções personalizadas que podem ser reutilizadas em diferentes partes da aplicação.
* **Informação adicional:** Inclua informações específicas sobre o erro para facilitar a depuração e a criação de logs detalhados.
* **Personalização:** Adapte a mensagem de erro e o código de status HTTP para cada tipo de exceção.
* **Hierarquia:** Organize as exceções em uma hierarquia para um melhor gerenciamento.

**Considerações:**

* **Evite criar muitas subclasses:** Uma hierarquia de exceções muito profunda pode dificultar a manutenção.
* **Use exceções personalizadas para erros específicos:** Não crie exceções personalizadas para cada pequena variação de um erro.
* **Documente suas exceções:** Inclua uma documentação clara sobre o significado de cada exceção personalizada.
* **Considere usar bibliotecas de validação:** Para validação de dados de entrada, considere usar bibliotecas como o Hibernate Validator, que podem gerar automaticamente exceções com mensagens de erro personalizadas.

**Exemplo de hierarquia de exceções:**

```
ResponseStatusException
├── CustomNotFoundException
├── CustomBadRequestException
└── CustomUnauthorizedException
```
---
## Simplificando o código com o uso de @ResponseStatus em exceptions

O uso da anotação `@ResponseStatus` nas suas exceções customizadas pode simplificar significativamente o tratamento de erros em suas aplicações Spring Boot. Ao associar diretamente um status HTTP a uma exceção, você elimina a necessidade de criar `@ExceptionHandler` personalizados para cada tipo de erro, tornando o código mais conciso e fácil de manter.

**Como funciona:**

* **Anotação @ResponseStatus:** Ao adicionar essa anotação a uma exceção, você especifica o status HTTP que será retornado quando essa exceção for lançada.
* **Tratamento centralizado:** O Spring MVC possui um mecanismo de tratamento de exceções global que reconhece a anotação `@ResponseStatus` e automaticamente configura a resposta HTTP com o status especificado.

**Exemplo prático:**

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

Com essa configuração, sempre que uma `ResourceNotFoundException` for lançada, o Spring retornará automaticamente um status HTTP 404 (Not Found).

**Vantagens:**

* **Código mais conciso:** Elimina a necessidade de criar `@ExceptionHandler` personalizados para cada tipo de exceção.
* **Melhor legibilidade:** Torna o código mais fácil de entender, pois o status HTTP está diretamente ligado à exceção.
* **Maior reutilização:** As exceções customizadas podem ser reutilizadas em diferentes partes da aplicação.
* **Integração com APIs REST:** Garante que a API retorne os códigos de status HTTP corretos, facilitando a integração com outros sistemas.

**Exemplo completo de uma API REST com tratamento de exceções usando @ResponseStatus:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        Optional<User> user = userRepository.findById(id);
        return user.orElseThrow(() -> new ResourceNotFoundException("User not found"));
    }
}

@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```
---
## Analisando os Impactos da Refatoração

**Refatoração:** um processo de melhoria contínua no desenvolvimento de software, que visa aprimorar a estrutura interna do código sem alterar seu comportamento externo. Mas quais são os impactos reais dessa prática? Vamos explorar os principais benefícios e desafios da refatoração:

### Benefícios da Refatoração

* **Melhora na legibilidade do código:** Um código refatorado é mais fácil de entender, o que facilita a manutenção e o desenvolvimento de novas funcionalidades.
* **Redução de bugs:** Ao simplificar a estrutura do código, a refatoração ajuda a identificar e corrigir bugs mais facilmente.
* **Aumento da manutenibilidade:** Um código bem estruturado é mais fácil de modificar e adaptar a novas necessidades.
* **Maior flexibilidade:** Um código refatorado é mais flexível e adaptável a mudanças, permitindo que o software evolua com menos esforço.
* **Melhora na performance:** Em alguns casos, a refatoração pode levar a melhorias na performance do sistema, especialmente quando se trata de otimizar algoritmos ou estruturas de dados.

### Desafios da Refatoração

* **Custo:** A refatoração exige tempo e esforço, o que pode impactar o cronograma do projeto.
* **Risco de introduzir novos bugs:** Se não for feita com cuidado, a refatoração pode introduzir novos bugs no código.
* **Necessidade de testes:** Para garantir que a refatoração não altere o comportamento do sistema, é fundamental ter uma boa cobertura de testes.
* **Resistência à mudança:** Alguns desenvolvedores podem resistir à refatoração, especialmente se o código existente funciona.

### Quando Refatorar?

A refatoração deve ser feita de forma contínua e incremental. Alguns sinais indicam que o código precisa ser refatorado:

* **Código duplicado:** Blocos de código idênticos ou muito semelhantes.
* **Funções ou classes muito grandes:** Funções ou classes com muitas responsabilidades.
* **Nomes de variáveis ou funções pouco claros:** Nomes que não refletem a função do código.
* **Código difícil de entender:** Código que exige muito esforço para ser compreendido.
* **Código rígido:** Código que é difícil de modificar sem quebrar outras partes do sistema.

### Boas Práticas para Refatorar

* **Faça pequenas mudanças:** Refatore em pequenos passos, testando cada mudança para garantir que o código continue funcionando.
* **Tenha testes automatizados:** Os testes automatizados garantem que a refatoração não introduza novos bugs.
* **Revise o código regularmente:** Faça revisões de código para identificar oportunidades de melhoria.
* **Use ferramentas de refatoração:** As IDEs modernas oferecem ferramentas que automatizam muitas tarefas de refatoração.
* **Comunique a equipe:** Mantenha a equipe informada sobre as mudanças e o motivo da refatoração.
---
## Criando a Exceção NegocioException: Uma Abordagem Personalizada para Erros de Negócio

**Por que criar uma `NegocioException` personalizada?**

Ao desenvolver aplicações, é comum encontrarmos situações em que um erro não é necessariamente um erro técnico, mas sim uma violação de alguma regra de negócio. Por exemplo, um usuário tentando sacar um valor superior ao saldo em uma conta bancária. Nesses casos, uma exceção genérica como `Exception` não é suficiente para expressar a natureza específica do problema.

A criação de uma exceção personalizada, como `NegocioException`, permite:

* **Clareza:** Indica claramente que o erro está relacionado a uma regra de negócio.
* **Tratamento específico:** Permite implementar tratamentos específicos para erros de negócio, como mensagens de erro mais detalhadas ou logs personalizados.
* **Hierarquia:** Permite criar uma hierarquia de exceções, agrupando erros de negócio por categorias.

**Como criar a `NegocioException`:**

```java
public class NegocioException extends RuntimeException {
    public NegocioException(String message) {
        super(message);
    }

    public NegocioException(String message, Throwable cause) {
        super(message, cause);
    }
}
```

* **Herança:** A `NegocioException` estende a classe `RuntimeException`, o que significa que não é obrigatório declará-la no método que a lança.
* **Construtores:** Os construtores permitem criar a exceção com uma mensagem personalizada ou com uma causa raiz.

**Exemplo de uso:**

```java
public class ContaBancaria {
    public void sacar(double valor) {
        if (saldo < valor) {
            throw new NegocioException("Saldo insuficiente para saque.");
        }
        // ...
    }
}
```

**Extendendo a `NegocioException`:**

Para representar diferentes tipos de erros de negócio, podemos criar subclasses de `NegocioException`:

```java
public class SaldoInsuficienteException extends NegocioException {
    public SaldoInsuficienteException() {
        super("Saldo insuficiente.");
    }
}
```

**Tratando a `NegocioException`:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(NegocioException.class)
    public ResponseEntity<String> handleNegocioException(NegocioException ex) {
        return ResponseEntity.status(HttpStatus.BAD_REQUEST).body(ex.getMessage());
    }
}
```

**Vantagens de usar `NegocioException`:**

* **Melhora a legibilidade do código:** Torna mais claro o motivo do erro.
* **Facilita a depuração:** Ajuda a identificar rapidamente a causa de um problema.
* **Permite um tratamento mais preciso:** Permite implementar tratamentos específicos para diferentes tipos de erros de negócio.
* **Promove a modularidade:** Ajuda a organizar o código em camadas e responsabilidades.

**Considerações adicionais:**

* **Mensagens de erro:** As mensagens de erro devem ser claras e concisas, informando o usuário sobre a causa do problema.
* **Hierarquia de exceções:** Crie uma hierarquia de exceções que reflita a estrutura do seu domínio.
* **Logging:** Utilize um framework de logging para registrar as exceções e facilitar a análise de problemas.
* **Customização:** Você pode adicionar campos adicionais à sua exceção personalizada para armazenar informações relevantes, como o usuário que causou o erro ou a data e hora do ocorrido.
---
## Afinando a Granularidade e Definindo a Hierarquia das Exceções de Negócio

Ao criar uma hierarquia de exceções de negócio, estamos buscando uma forma mais granular e organizada de lidar com os diferentes tipos de erros que podem ocorrer em uma aplicação. Essa abordagem permite um tratamento mais específico para cada tipo de exceção, tornando o código mais robusto e fácil de manter.

**Por que definir uma hierarquia?**

* **Organização:** Agrupa exceções relacionadas, facilitando a compreensão e a manutenção do código.
* **Tratamento específico:** Permite implementar tratamentos personalizados para diferentes tipos de exceções.
* **Flexibilidade:** Facilita a adição de novas exceções à medida que a aplicação evolui.
* **Reutilização:** Permite a criação de tratadores de exceções genéricos para grupos de exceções relacionadas.

**Exemplo de hierarquia:**

```java
public class NegocioException extends RuntimeException {
    // ...
}

public class ValidacaoException extends NegocioException {
    // ...
}

public class AutorizacaoException extends NegocioException {
    // ...
}

public class RecursoNaoEncontradoException extends NegocioException {
    // ...
}
```

**Nessa hierarquia:**

* **NegocioException:** Exceção base para todos os erros de negócio.
* **ValidacaoException:** Representa erros de validação de dados.
* **AutorizacaoException:** Representa erros de autorização.
* **RecursoNaoEncontradoException:** Representa erros quando um recurso não é encontrado.

**Como definir a granularidade:**

A granularidade da hierarquia depende da complexidade da sua aplicação e do nível de detalhe que você deseja capturar. Alguns fatores a considerar:

* **Frequência:** Exceções que ocorrem com frequência podem merecer sua própria classe.
* **Impacto:** Exceções que causam um grande impacto na aplicação podem exigir um tratamento mais específico.
* **Tratamento:** Se um tipo de exceção requer um tratamento significativamente diferente, ele pode justificar uma classe própria.

**Dicas para criar uma boa hierarquia:**

* **Comece com o geral e vá para o específico:** Defina as exceções mais abstratas primeiro e, em seguida, crie subclasses para casos mais específicos.
* **Use nomes claros e descritivos:** Os nomes das exceções devem refletir a causa do erro.
* **Evite hierarquias muito profundas:** Uma hierarquia muito complexa pode dificultar a compreensão.
* **Considere usar anotações:** Utilize anotações para adicionar metadados às suas exceções, como códigos de erro ou informações adicionais.

**Exemplo de uso com anotações:**

```java
@ResponseStatus(HttpStatus.BAD_REQUEST)
public class ValidacaoException extends NegocioException {
    // ...
}
```

**Tratamento das exceções:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ValidacaoException.class)
    public ResponseEntity<String> handleValidacaoException(ValidacaoException ex) {
        // Tratamento específico para erros de validação
    }
}
```

**Benefícios de uma hierarquia bem definida:**

* **Melhora a manutenibilidade:** Facilita a localização e correção de erros.
* **Aumenta a reutilização de código:** Permite criar tratadores de exceções genéricos.
* **Melhora a legibilidade do código:** Torna o código mais fácil de entender.
* **Facilita a criação de logs detalhados:** Permite registrar informações mais precisas sobre os erros.
---
## Tratando Exceções em Nível de Controlador com @ExceptionHandler

A anotação `@ExceptionHandler` no Spring é uma ferramenta poderosa para centralizar o tratamento de exceções em seus controladores. Ao utilizar essa anotação, você pode interceptar exceções específicas e retornar respostas personalizadas para o cliente, garantindo uma experiência de usuário mais consistente e informativa.

### Como funciona o @ExceptionHandler?

* **Interceptação:** O método anotado com `@ExceptionHandler` é chamado quando a exceção especificada é lançada dentro do método do controlador ou em qualquer método chamado por ele.
* **Personalização:** Você pode personalizar a resposta HTTP, incluindo o status HTTP, corpo da resposta e cabeçalhos.
* **Hierarquia:** O Spring procura por `@ExceptionHandler`s que correspondam à exceção lançada ou a uma superclasse dela.

### Exemplo Prático

```java
@RestControllerAdvice
public class CustomExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleResourceNotFoundException(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Recurso não encontrado");
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGenericException(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("Erro interno do servidor");
    }
}
```

* **@RestControllerAdvice:** Essa anotação indica que essa classe contém conselhos para controladores REST.
* **@ExceptionHandler:** Indica que o método irá tratar a exceção especificada.
* **ResponseEntity:** Permite construir uma resposta HTTP personalizada, incluindo o status HTTP, corpo da resposta e cabeçalhos.

### Vantagens de usar @ExceptionHandler

* **Centralização:** Agrupa o tratamento de exceções em um único lugar, facilitando a manutenção.
* **Personalização:** Permite criar respostas personalizadas para diferentes tipos de exceções.
* **Melhora a legibilidade:** Separa a lógica de negócio do tratamento de erros.
* **Aumenta a segurança:** Pode ser usado para ocultar informações sensíveis em mensagens de erro.

### Boas Práticas

* **Hierarquia de exceções:** Crie uma hierarquia de exceções para organizar melhor os diferentes tipos de erros.
* **Mensagens de erro claras:** As mensagens de erro devem ser concisas e informativas, mas sem revelar detalhes sensíveis.
* **Logging:** Registre as exceções para facilitar a depuração.
* **Tratamento de exceções genéricas:** Tenha um `@ExceptionHandler` para capturar exceções não esperadas e retornar uma mensagem de erro genérica.
* **Testes:** Escreva testes unitários para garantir que os `@ExceptionHandler`s estão funcionando corretamente.

### Cenários de uso

* **Erros de validação:** Retornar um status 400 (Bad Request) com uma lista de erros de validação.
* **Recursos não encontrados:** Retornar um status 404 (Not Found).
* **Erros de autorização:** Retornar um status 401 (Unauthorized) ou 403 (Forbidden).
* **Erros internos do servidor:** Retornar um status 500 (Internal Server Error) com uma mensagem genérica.

### Considerações adicionais

* **Customização:** Você pode adicionar informações adicionais à resposta, como um timestamp, um ID de correlação ou um link para documentação.
* **Internacionalização:** Use mensagens internacionalizadas para atender a diferentes idiomas.
* **Performance:** Evite operações caras dentro de um `@ExceptionHandler`, pois isso pode afetar a performance da aplicação.
---
## Tratando Exceções Globais com @ExceptionHandler e @ControllerAdvice

A anotação `@ControllerAdvice` em conjunto com `@ExceptionHandler` oferece uma forma elegante e centralizada de lidar com exceções em aplicações Spring. Ao utilizar essa combinação, você pode interceptar e tratar exceções que ocorrem em qualquer parte da sua aplicação, garantindo uma resposta consistente e informativa ao cliente.

### O que é @ControllerAdvice?

* **Classe de aconselhamento:** Anota uma classe como um conselheiro global para todos os controladores.
* **Interceptação:** Permite interceptar exceções, requisições e respostas antes ou depois de serem processadas pelos controladores.
* **Centralização:** Centraliza a lógica de tratamento de exceções, tornando o código mais limpo e organizado.

### O que é @ExceptionHandler?

* **Método de tratamento:** Anota um método dentro de uma classe `@ControllerAdvice` para tratar uma exceção específica.
* **Personalização:** Permite personalizar a resposta HTTP, incluindo status, corpo e cabeçalhos.
* **Hierarquia:** O Spring procura por `@ExceptionHandler`s que correspondam à exceção lançada ou a uma superclasse dela.

### Exemplo Prático

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleResourceNotFoundException(ResourceNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body("Recurso não encontrado");
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGenericException(Exception ex) {
        return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("Erro interno do servidor");
    }
}
```

* **@RestControllerAdvice:** Indica que a classe contém conselhos para controladores REST.
* **@ExceptionHandler:** Indica que o método irá tratar a exceção especificada.
* **ResponseEntity:** Permite construir uma resposta HTTP personalizada, incluindo o status HTTP, corpo da resposta e cabeçalhos.

### Vantagens do Uso

* **Centralização:** Agrupa o tratamento de exceções em um único lugar, facilitando a manutenção.
* **Personalização:** Permite criar respostas personalizadas para diferentes tipos de exceções.
* **Melhora a legibilidade:** Separa a lógica de negócio do tratamento de erros.
* **Aumenta a segurança:** Pode ser usado para ocultar informações sensíveis em mensagens de erro.
* **Tratamento global:** Captura exceções em toda a aplicação, não apenas nos controladores.

### Boas Práticas

* **Hierarquia de exceções:** Crie uma hierarquia de exceções para organizar melhor os diferentes tipos de erros.
* **Mensagens de erro claras:** As mensagens de erro devem ser concisas e informativas, mas sem revelar detalhes sensíveis.
* **Logging:** Registre as exceções para facilitar a depuração.
* **Tratamento de exceções genéricas:** Tenha um `@ExceptionHandler` para capturar exceções não esperadas e retornar uma mensagem de erro genérica.
* **Testes:** Escreva testes unitários para garantir que os `@ExceptionHandler`s estão funcionando corretamente.

### Cenários de Uso

* **Erros de validação:** Retornar um status 400 (Bad Request) com uma lista de erros de validação.
* **Recursos não encontrados:** Retornar um status 404 (Not Found).
* **Erros de autorização:** Retornar um status 401 (Unauthorized) ou 403 (Forbidden).
* **Erros internos do servidor:** Retornar um status 500 (Internal Server Error) com uma mensagem genérica.

### Considerações Adicionais

* **Customização:** Você pode adicionar informações adicionais à resposta, como um timestamp, um ID de correlação ou um link para documentação.
* **Internacionalização:** Use mensagens internacionalizadas para atender a diferentes idiomas.
* **Performance:** Evite operações caras dentro de um `@ExceptionHandler`, pois isso pode afetar a performance da aplicação.
---
## Criando um Exception Handler Global com ResponseEntityExceptionHandler

**ResponseEntityExceptionHandler** é uma classe base fornecida pelo Spring Framework que simplifica o tratamento de exceções globais em aplicações web. Ao estender essa classe, você pode criar um manipulador de exceções personalizado que interceptará e tratará diferentes tipos de exceções, fornecendo respostas HTTP apropriadas.

### Como criar um ResponseEntityExceptionHandler

1. **Extender a classe:**
   ```java
   @ControllerAdvice
   public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {
       // ...
   }
   ```

2. **Implementar métodos de tratamento:**
   ```java
   @Override
   protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
       Map<String, String> errors = new HashMap<>();
       ex.getBindingResult().getAllErrors().forEach((error) -> {
           String fieldName = ((FieldError) error).getField();
           String errorMessage = error.getDefaultMessage();
           errors.put(fieldName, errorMessage);
       });
       return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
   }

   @Override
   protected ResponseEntity<Object> handleEntityNotFoundException(EntityNotFoundException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
       return new ResponseEntity<>("Recurso não encontrado", HttpStatus.NOT_FOUND);
   }

   // ... outros métodos para tratar diferentes tipos de exceções
   ```

### Como funciona

* **Interceptação:** O Spring Framework intercepta as exceções lançadas em seus controladores.
* **Delegação:** A exceção é delegada ao método `handleMethodArgumentNotValid` ou outro método apropriado, dependendo do tipo de exceção.
* **Personalização:** Você pode personalizar a resposta HTTP, incluindo o status HTTP, corpo da resposta e cabeçalhos.

### Vantagens do uso de ResponseEntityExceptionHandler

* **Centralização:** Agrupa o tratamento de exceções em um único lugar, facilitando a manutenção.
* **Personalização:** Permite criar respostas HTTP personalizadas para diferentes tipos de exceções.
* **Reutilização:** Pode ser reutilizado em diferentes projetos Spring.
* **Integração com Spring Framework:** Aproveita as funcionalidades do Spring Framework para o tratamento de exceções.

### Considerações adicionais

* **Hierarquia de exceções:** Crie uma hierarquia de exceções personalizadas para organizar melhor os diferentes tipos de erros.
* **Mensagens de erro claras:** As mensagens de erro devem ser concisas e informativas, mas sem revelar detalhes sensíveis.
* **Logging:** Registre as exceções para facilitar a depuração.
* **Tratamento de exceções genéricas:** Tenha um `@ExceptionHandler` para capturar exceções não esperadas e retornar uma mensagem de erro genérica.
* **Testes:** Escreva testes unitários para garantir que os `@ExceptionHandler`s estão funcionando corretamente.

### Exemplo de uso em um controlador

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        User user = userService.getUserById(id);
        if (user == null) {
            throw new EntityNotFoundException("User not found");
        }
        return user;
    }
}
```

Quando uma `EntityNotFoundException` é lançada, o `GlobalExceptionHandler` interceptará a exceção e retornará uma resposta HTTP com status 404 e a mensagem "Recurso não encontrado".

---
## Customizando o Corpo da Resposta Padrão de ResponseEntityExceptionHandler

O `ResponseEntityExceptionHandler` oferece uma base sólida para personalizar as respostas HTTP em caso de exceções, mas você pode ir além e criar respostas mais informativas e personalizadas para atender às suas necessidades específicas.

**Personalizando o Corpo da Resposta:**

* **Criando uma classe de erro personalizada:**
  ```java
  public class ApiError {
      private String message;
      private List<String> errors;

      // Construtores, getters e setters
  }
  ```
* **Retornando a classe personalizada:**
  ```java
  @Override
  protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
      ApiError apiError = new ApiError("Validation error");
      ex.getBindingResult().getAllErrors().forEach((error) -> {
          String fieldName = ((FieldError) error).getField();
          String errorMessage = error.getDefaultMessage();
          apiError.getErrors().add(fieldName + ": " + errorMessage);
      });
      return new ResponseEntity<>(apiError, HttpStatus.BAD_REQUEST);
  }
  ```

**Exemplo completo:**

```java
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @Override
    protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
        ApiError apiError = new ApiError("Validation error");
        ex.getBindingResult().getAllErrors().forEach((error) -> {
            String fieldName = ((FieldError) error).getField();
            String errorMessage = error.getDefaultMessage();
            apiError.getErrors().add(fieldName + ": " + errorMessage);
        });
        return new ResponseEntity<>(apiError, HttpStatus.BAD_REQUEST);
    }

    @Override
    protected ResponseEntity<Object> handleEntityNotFoundException(EntityNotFoundException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
        ApiError apiError = new ApiError("Resource not found");
        return new ResponseEntity<>(apiError, HttpStatus.NOT_FOUND);
    }
}
```

**Personalizando ainda mais:**

* **Adicionando informações de timestamp:**
  ```java
  apiError.setTimestamp(LocalDateTime.now());
  ```
* **Adicionando informações de path:**
  ```java
  apiError.setPath(request.getDescription(false));
  ```
* **Adicionando um código de erro:**
  ```java
  apiError.setCode("ERR_VALIDATION");
  ```
* **Utilizando um formato específico para a resposta:**
  ```java
  ObjectMapper objectMapper = new ObjectMapper();
  return new ResponseEntity<>(objectMapper.writeValueAsString(apiError), HttpStatus.BAD_REQUEST);
  ```

**Considerações:**

* **Clareza:** As mensagens de erro devem ser claras e concisas, facilitando a identificação do problema.
* **Consistência:** Mantenha um formato consistente para as respostas de erro em toda a aplicação.
* **Detalhes:** Inclua detalhes suficientes para ajudar na depuração, mas evite expor informações sensíveis.
* **Personalização:** Adapte a estrutura da resposta às suas necessidades específicas.

**Exemplo de resposta personalizada:**

```json
{
  "timestamp": "2023-11-23T10:15:30Z",
  "status": 400,
  "error": "Bad Request",
  "message": "Validation error",
  "path": "/api/users",
  "errors": [
    "email: Email is required",
    "password: Password must be at least 8 characters"
  ]
}
```

**Benefícios da personalização:**

* **Melhor experiência do usuário:** Mensagens de erro mais claras e informativas.
* **Facilidade de depuração:** Informações detalhadas sobre o erro.
* **Conformidade com padrões:** Possibilidade de seguir padrões como RFC 7807 (Problem Details for HTTP APIs).
---
## Entendendo a RFC 7807 e Implementando-a no Spring Boot

**RFC 7807** é um padrão que define uma estrutura comum para respostas de erro em APIs HTTP. Ela visa fornecer informações mais detalhadas e consistentes sobre os erros, facilitando a depuração e a criação de clientes mais robustos.

### Por que usar a RFC 7807?

* **Padronização:** Garante um formato consistente para todas as respostas de erro, facilitando a compreensão por diferentes clientes.
* **Detalhes:** Permite incluir informações mais específicas sobre o erro, como o tipo, a causa e uma referência para mais informações.
* **Facilidade de uso:** A estrutura é simples e fácil de entender, tanto por humanos quanto por máquinas.
* **Melhor experiência do desenvolvedor:** Ajuda a criar APIs mais robustas e fáceis de manter.

### Implementando no Spring Boot

**1. Criando uma classe para representar o erro:**

```java
public class ApiError implements ProblemDetails {

    private final String type;
    private final String title;
    private final int status;
    private final String detail;
    private final String instance;

    // Construtor, getters e setters
}
```

**2. Customizando o ResponseEntityExceptionHandler:**

```java
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @Override
    protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
        ApiError apiError = new ApiError();
        apiError.setStatus(status.value());
        apiError.setTitle("Erro de validação");
        apiError.setDetail("Os dados fornecidos não são válidos.");

        // ... (preencher outros campos)

        return new ResponseEntity<>(apiError, status);
    }

    // ... outros manipuladores de exceção
}
```

**Exemplo de resposta:**

```json
{
  "type": "https://sua-api.com/errors/validation",
  "title": "Erro de validação",
  "status": 400,
  "detail": "Os dados fornecidos não são válidos.",
  "instance": "/api/users"
}
```

### Campos da RFC 7807

* **type:** Um URI que identifica o tipo de problema.
* **title:** Um título descritivo para o problema.
* **status:** O código de status HTTP correspondente.
* **detail:** Uma explicação detalhada do problema.
* **instance:** Um URI que identifica a instância específica do problema.

### Benefícios da implementação

* **Respostas de erro mais informativas:** Facilitam a depuração e o entendimento dos problemas.
* **Padronização:** Garante consistência em todas as respostas de erro.
* **Melhora a experiência do desenvolvedor:** Torna a criação de APIs mais fácil e eficiente.
* **Facilita a criação de ferramentas de automação:** As respostas de erro no formato RFC 7807 podem ser facilmente processadas por ferramentas.

### Considerações adicionais

* **Personalização:** Você pode personalizar a resposta adicionando campos extras, como um timestamp ou um ID de correlação.
* **Internacionalização:** As mensagens de erro podem ser internacionalizadas para atender a diferentes idiomas.
* **Hierarquia de erros:** Você pode criar uma hierarquia de tipos de erro para organizar melhor as suas exceções.
---
## Padronizando Respostas de Erro com a RFC 7807: Um Guia Completo

A **RFC 7807** oferece um padrão consistente para formatar as respostas de erro em APIs HTTP. Ao adotar essa norma, você garante que seus clientes recebam informações claras e detalhadas sobre os problemas ocorridos, facilitando a depuração e a resolução de problemas.

### Por que usar a RFC 7807?

* **Padronização:** Define um formato único para todas as respostas de erro, facilitando a compreensão por diferentes clientes.
* **Detalhes:** Permite incluir informações específicas sobre o erro, como o tipo, a causa e uma referência para mais informações.
* **Legibilidade:** A estrutura é simples e fácil de entender, tanto por humanos quanto por máquinas.
* **Melhora a experiência do desenvolvedor:** Torna a criação de APIs mais robusta e fácil de manter.

### Implementando a RFC 7807 no Spring Boot

**1. Criando uma classe para representar o erro:**

```java
public class ApiError implements ProblemDetails {

    private final String type;
    private final String title;
    private final int status;
    private final String detail;
    private final String instance;

    // Construtor, getters e setters
}
```

**2. Customizando o ResponseEntityExceptionHandler:**

```java
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @Override
    protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
        ApiError apiError = new ApiError();
        apiError.setStatus(status.value());
        apiError.setTitle("Erro de validação");
        apiError.setDetail("Os dados fornecidos não são válidos.");

        // ... (preencher outros campos)

        return new ResponseEntity<>(apiError, status);
    }

    // ... outros manipuladores de exceção
}
```

**Exemplo de resposta:**

```json
{
  "type": "https://sua-api.com/errors/validation",
  "title": "Erro de validação",
  "status": 400,
  "detail": "Os dados fornecidos não são válidos.",
  "instance": "/api/users"
}
```

### Campos da RFC 7807

* **type:** Um URI que identifica o tipo de problema.
* **title:** Um título descritivo para o problema.
* **status:** O código de status HTTP correspondente.
* **detail:** Uma explicação detalhada do problema.
* **instance:** Um URI que identifica a instância específica do problema.

### Benefícios da implementação

* **Respostas de erro mais informativas:** Facilitam a depuração e o entendimento dos problemas.
* **Padronização:** Garante consistência em todas as respostas de erro.
* **Melhora a experiência do desenvolvedor:** Torna a criação de APIs mais fácil e eficiente.
* **Facilita a criação de ferramentas de automação:** As respostas de erro no formato RFC 7807 podem ser facilmente processadas por ferramentas.

### Personalizando as Respostas de Erro

* **Campos adicionais:** Você pode adicionar campos personalizados para incluir informações específicas da sua aplicação.
* **Hierarquia de erros:** Organize seus tipos de erro em uma hierarquia para representar melhor a estrutura de sua aplicação.
* **Formatação:** Utilize formatos como JSON ou XML para representar a resposta, de acordo com suas necessidades.
* **Internacionalização:** Traduza as mensagens de erro para diferentes idiomas.

### Exemplo Avançado

```java
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @ExceptionHandler(CustomException.class)
    public ResponseEntity<ProblemDetails> handleCustomException(CustomException ex) {
        ApiError apiError = new ApiError();
        apiError.setType("https://sua-api.com/errors/custom");
        apiError.setTitle(ex.getMessage());
        apiError.setStatus(HttpStatus.INTERNAL_SERVER_ERROR.value());
        apiError.setDetail("Ocorreu um erro inesperado.");
        return new ResponseEntity<>(apiError, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```
---
## Customizando o ResponseEntityExceptionHandler

O `ResponseEntityExceptionHandler` é uma classe base poderosa do Spring Framework que permite personalizar o tratamento de exceções globais em suas aplicações web. Ao estender essa classe, você pode criar um manipulador de exceções personalizado que interceptará e tratará diferentes tipos de exceções, fornecendo respostas HTTP apropriadas.

### Customizando Respostas HTTP

Para personalizar a resposta HTTP, você pode:

1. **Modificar o status HTTP:**
   ```java
   @Override
   protected ResponseEntity<Object> handleEntityNotFoundException(EntityNotFoundException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
       return new ResponseEntity<>("Recurso não encontrado", HttpStatus.NOT_FOUND);
   }
   ```
2. **Alterar o corpo da resposta:**
   ```java
   @Override
   protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
       Map<String, String> errors = new HashMap<>();
       ex.getBindingResult().getAllErrors().forEach((error) -> {
           String fieldName = ((FieldError) error).getField();
           String errorMessage = error.getDefaultMessage();
           errors.put(fieldName, errorMessage);
       });
       return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
   }
   ```
3. **Adicionar cabeçalhos personalizados:**
   ```java
   HttpHeaders headers = new HttpHeaders();
   headers.add("X-Error-Code", "CUSTOM_ERROR_CODE");
   return new ResponseEntity<>("Custom error message", headers, HttpStatus.INTERNAL_SERVER_ERROR);
   ```

### Criando Exceções Customizadas

Para tratar exceções específicas, você pode criar suas próprias exceções e personalizar o tratamento:

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    // ...
}
```

```java
@ExceptionHandler(ResourceNotFoundException.class)
public ResponseEntity<Object> handleResourceNotFoundException(ResourceNotFoundException ex) {
    return new ResponseEntity<>("Recurso não encontrado", HttpStatus.NOT_FOUND);
}
```

### Considerações Importantes

* **Hierarquia de Exceções:** Crie uma hierarquia de exceções para organizar melhor o tratamento de erros.
* **Mensagens de Erro Informativas:** As mensagens de erro devem ser claras e concisas, mas sem revelar informações sensíveis.
* **Logging:** Registre as exceções para facilitar a depuração.
* **Testes Unitários:** Escreva testes para garantir que os `@ExceptionHandler`s estão funcionando corretamente.
* **Segurança:** Evite expor informações sensíveis nas mensagens de erro.

### Exemplo Avançado: Usando a RFC 7807

```java
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @Override
    protected ResponseEntity<Object> handleMethodArgumentNotValid(MethodArgumentNotValidException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
        ApiError apiError = new ApiError();
        apiError.setStatus(status.value());
        apiError.setTitle("Validation Error");
        apiError.setDetail("Invalid input parameters");

        // ... (populate other fields)

        return new ResponseEntity<>(apiError, status);
    }
}
```
---
## Tratando a Exceção InvalidFormatException na Desserialização

A exceção `InvalidFormatException` geralmente ocorre quando há um problema na conversão de um formato de dados para outro durante a desserialização. No contexto do Spring, essa exceção pode surgir quando você está tentando converter um JSON ou XML para um objeto Java e algum campo não está no formato esperado.

### Entendendo a Causa

* **Formato de dados inválido:** O dado enviado não está no formato esperado (por exemplo, um número em vez de uma string).
* **Tipo de dado incompatível:** O tipo de dado do campo na classe Java não corresponde ao tipo do dado enviado.
* **Propriedade inexistente:** A propriedade enviada não existe na classe Java.
* **Valor nulo:** Um valor nulo foi enviado para um campo que não aceita nulos.

### Tratando a Exceção no Spring

**1. Utilizando o ResponseEntityExceptionHandler:**

* **Criar um manipulador de exceções personalizado:**

```java
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @Override
    protected ResponseEntity<Object> handleInvalidFormatException(MethodArgumentTypeMismatchException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
        // ...
    }
}
```

* **Personalizar a resposta:**

```java
@Override
    protected ResponseEntity<Object> handleInvalidFormatException(MethodArgumentTypeMismatchException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
        String error = "Formato inválido para o campo " + ex.getName() + ": " + ex.getValue();
        return new ResponseEntity<>(error, HttpStatus.BAD_REQUEST);
    }
```

**2. Usando a anotação @ControllerAdvice:**

* **Criar um método para tratar a exceção específica:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentTypeMismatchException.class)
    public ResponseEntity<String> handleMethodArgumentTypeMismatch(MethodArgumentTypeMismatchException ex) {
        String error = "Formato inválido para o campo " + ex.getName() + ": " + ex.getValue();
        return new ResponseEntity<>(error, HttpStatus.BAD_REQUEST);
    }
}
```

### Exemplo Completo com Mensagem Personalizada e Detalhes da Exceção

```java
@ControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @Override
    protected ResponseEntity<Object> handleMethodArgumentTypeMismatch(MethodArgumentTypeMismatchException ex, HttpHeaders headers, HttpStatus status, WebRequest request) {
        Map<String, String> errors = new HashMap<>();
        errors.put("campo", ex.getName());
        errors.put("valor", ex.getValue() != null ? ex.getValue().toString() : "<nulo>");
        errors.put("mensagem", "Formato inválido para o campo. Esperado: " + ex.getRequiredType().getSimpleName());
        return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
    }
}
```
---
## Habilitando Erros na Desserialização de Propriedades Inexistentes ou Ignoradas

**Entendendo o Problema**

Quando uma aplicação tenta desserializar um JSON ou XML em um objeto Java, pode ocorrer situações onde:

* **Propriedade inexistente:** O JSON ou XML contém uma propriedade que não existe na classe Java.
* **Propriedade ignorada:** A propriedade existe na classe Java, mas foi configurada para ser ignorada durante a desserialização.

**Por que Habilitar Erros?**

* **Detecção precoce de problemas:** Permite identificar erros de mapeamento logo no início do processo.
* **Melhora na qualidade do código:** Incentiva a criação de modelos de dados mais precisos e consistentes.
* **Prevenção de bugs:** Evita que dados inválidos sejam persistidos no sistema.

**Como Habilitar Erros no Spring**

O Spring, com a ajuda de bibliotecas como Jackson, oferece diversas formas de configurar o comportamento da desserialização.

### 1. Utilizando o Jackson ObjectMapper

* **Configurando o ObjectMapper:**

```java
ObjectMapper objectMapper = new ObjectMapper();
objectMapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, true);
```

* **Aumentando a verbosidade:**

```java
objectMapper.configure(DeserializationFeature.FAIL_ON_IGNORED_PROPERTIES, true);
```

* **Personalizando as mensagens de erro:**

```java
objectMapper.setHandler(new DefaultTypingStrategy(ObjectMapper.DefaultTyping.JAVA_LANG_OBJECT)) {
    @Override
    public String typeIdResolver(JavaType baseType) {
        return baseType.getRawClass().getName();
    }
};
```

### 2. Utilizando a anotação @JsonIgnoreProperties

* **Ignorando propriedades desconhecidas:**

```java
@JsonIgnoreProperties(ignoreUnknown = true)
public class MyObject {
    // ...
}
```

### 3. Utilizando o @JsonAnySetter

* **Capturando propriedades desconhecidas:**

```java
public class MyObject {
    @JsonAnySetter
    public void handleUnknown(String key, Object value) {
        // Lógica para tratar propriedades desconhecidas
    }
}
```

### 4. Utilizando o @JsonIgnore

* **Ignorando propriedades específicas:**

```java
public class MyObject {
    @JsonIgnore
    private String ignoredProperty;
}
```

**Exemplo Completo:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @PostMapping
    public ResponseEntity<User> createUser(@RequestBody User user) {
        // ...
    }
}
```

**Importante:**
* **Equilíbrio:** Habilitar todos os erros pode tornar o código mais verboso e difícil de manter. Encontre um equilíbrio entre a detecção de erros e a flexibilidade.
* **Mensagens de erro personalizadas:** Crie mensagens de erro claras e informativas para facilitar a depuração.
* **Tratamento de exceções:** Implemente um `@ExceptionHandler` para capturar as exceções de desserialização e fornecer uma resposta adequada ao cliente.
---
## Lançando Exceções de Desserialização em Atualizações Parciais (PATCH)

**Entendendo o Cenário**

Em APIs REST, o método HTTP `PATCH` é utilizado para realizar atualizações parciais em recursos. Isso significa que apenas os campos especificados no corpo da requisição serão atualizados. Ao lidar com essas atualizações, é crucial garantir a integridade dos dados e lançar exceções apropriadas quando ocorrerem problemas na desserialização.

**Por que Lançar Exceções?**

* **Indicar erros:** Avisar o cliente sobre problemas na requisição.
* **Gerenciar fluxos:** Permitir que a aplicação tome decisões com base no tipo de erro.
* **Melhorar a robustez:** Prevenir que dados inválidos sejam persistidos.

**Como Lançar Exceções no Spring**

O Spring oferece diversas ferramentas para lidar com a desserialização e o lançamento de exceções.

### 1. **Utilizando o @JsonIgnoreProperties**

* **Ignorando propriedades desconhecidas:**

```java
@JsonIgnoreProperties(ignoreUnknown = true)
public class User {
    // ...
}
```
**Observação:** Essa configuração ignora propriedades desconhecidas, mas não lança exceções.

### 2. **Configurando o ObjectMapper**

* **Habilitando a falha em propriedades desconhecidas:**

```java
ObjectMapper objectMapper = new ObjectMapper();
objectMapper.configure(DeserializationFeature.FAIL_ON_UNKNOWN_PROPERTIES, true);
```
**Observação:** Essa configuração fará com que o Jackson lance uma `JsonMappingException` quando encontrar propriedades desconhecidas.

### 3. **Criando um Custom Deserializer**

* **Personalizando a desserialização:**

```java
class UserDeserializer extends JsonDeserializer<User> {
    @Override
    public User deserialize(JsonParser p, DeserializationContext ctxt) throws IOException, JsonProcessingException {
        // Lógica de desserialização personalizada
        if (/* algum erro ocorreu */) {
            throw new InvalidRequestException("Propriedade inválida");
        }
        // ...
    }
}
```

### 4. **Utilizando o @JsonAnySetter**

* **Capturando propriedades desconhecidas:**

```java
public class User {
    @JsonAnySetter
    public void handleUnknown(String key, Object value) {
        throw new InvalidRequestException("Propriedade desconhecida: " + key);
    }
}
```

### 5. **Tratando Exceções com @ExceptionHandler**

* **Personalizando a resposta:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(JsonMappingException.class)
    public ResponseEntity<String> handleJsonMappingException(JsonMappingException ex) {
        return new ResponseEntity<>("Erro na desserialização: " + ex.getMessage(), HttpStatus.BAD_REQUEST);
    }
}
```

### **Exemplo Completo com Validação e Exceções Personalizadas**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @PatchMapping("/{id}")
    public ResponseEntity<User> updateUser(@PathVariable Long id, @RequestBody @Valid @PatchValue User user) {
        // ...
    }
}
```
---
## Estendendo o Formato do Problema para Adicionar Novas Propriedades na RFC 7807

**Entendendo a Necessidade**

A RFC 7807 fornece uma estrutura básica para representar problemas em APIs HTTP. No entanto, à medida que a complexidade das aplicações aumenta, pode ser necessário adicionar informações mais específicas para cada tipo de problema.

**Como Estender o Formato**

Existem diversas formas de estender o formato do problema definido pela RFC 7807 para adicionar novas propriedades:

### 1. **Campos Personalizados**

* **Diretamente no objeto:** Adicione novos campos diretamente ao objeto que representa o problema. Por exemplo:
  ```java
  public class ApiError implements ProblemDetails {
      // ... outros campos
      private String customProperty1;
      private Map<String, Object> additionalProperties;
  }
  ```
* **Utilizando uma classe base:** Crie uma classe base que estenda `ProblemDetails` e adicione os campos personalizados.
* **Utilizando uma interface:** Defina uma interface com os campos personalizados e faça com que sua classe de erro implemente essa interface.

### 2. **Utilizando Extensões**

* **JSON Schema:** Defina um JSON Schema para validar e documentar as propriedades adicionais.
* **Profiles:** Utilize perfis para definir diferentes conjuntos de propriedades para diferentes ambientes ou clientes.

### 3. **Utilizando Links**

* **Relacionamentos:** Utilize o campo `links` para fornecer links para recursos relacionados, como documentação ou soluções.

**Exemplo Prático**

```java
public class ApiError implements ProblemDetails {
    // ... outros campos
    private String customProperty1;
    private Map<String, Object> extensions;

    public Map<String, Object> getExtensions() {
        return extensions;
    }

    public void addExtension(String name, Object value) {
        if (extensions == null) {
            extensions = new HashMap<>();
        }
        extensions.put(name, value);
    }
}
```

**Considerações Importantes**

* **Semântica:** As novas propriedades devem ter um significado claro e consistente.
* **Evitar poluição:** Não adicione um grande número de propriedades desnecessárias.
* **Compatibilidade:** Ao adicionar novas propriedades, considere a compatibilidade com versões anteriores da API.
* **Documentação:** Documente as novas propriedades para que os consumidores da API possam entendê-las.

**Exemplo de Uso**

```java
ApiError error = new ApiError();
error.setTitle("Erro de validação");
error.setDetail("O campo 'nome' é obrigatório");
error.addExtension("errorCode", "VALIDATION_ERROR");
error.addExtension("fieldName", "nome");
```

**Benefícios da Extensão**

* **Flexibilidade:** Permite adaptar a representação do erro às necessidades específicas da aplicação.
* **Informação adicional:** Fornece informações mais detalhadas para o cliente, facilitando a depuração.
* **Personalização:** Permite criar respostas de erro mais personalizadas para diferentes cenários.
---
