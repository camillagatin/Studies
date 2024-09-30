## Adicionando o Driver JDBC ao Projeto e Criando uma Conexão em Java

**O que é JDBC?**
JDBC (Java Database Connectivity) é uma API Java que permite que aplicações Java se conectem a uma variedade de bancos de dados. É uma interface padrão para acessar bancos de dados relacionais e, com ela, você pode executar consultas SQL, inserir, atualizar e excluir dados.

**Por que adicionar um driver JDBC?**
Cada banco de dados (MySQL, PostgreSQL, Oracle, etc.) possui seu próprio driver JDBC, que serve como uma ponte entre sua aplicação Java e o banco de dados. Esse driver traduz as chamadas JDBC em comandos específicos que o banco de dados entende.

**Como adicionar um driver JDBC ao projeto?**
A forma de adicionar o driver JDBC ao seu projeto varia um pouco dependendo do ambiente de desenvolvimento que você está utilizando (Eclipse, IntelliJ, etc.). No entanto, o conceito geral é o mesmo:

1. **Baixe o driver:**
   * Acesse o site do banco de dados que você está utilizando e baixe o driver JDBC correspondente à sua versão do Java. O driver geralmente vem em formato JAR.

2. **Adicione o JAR ao projeto:**
   * **Eclipse:** Clique com o botão direito no projeto, vá em "Properties", selecione "Java Build Path" na árvore esquerda, clique na aba "Libraries", clique no botão "Add External JARs", selecione o arquivo JAR do driver e clique em "OK".
   * **IntelliJ:** Clique com o botão direito no projeto, vá em "File" -> "Project Structure", selecione "Modules" e, em seguida, "Dependencies". Clique no sinal de "+" para adicionar o JAR.

**Criando uma conexão JDBC**
Uma vez que o driver esteja adicionado ao seu projeto, você pode criar uma conexão com o banco de dados utilizando o seguinte código:
```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class Principal {

    public static void main(String[] args) {
        try (Connection conexao = DriverManager
                .getConnection("jdbc:mysql://localhost:3306/comercial", "root", "")) {
            System.out.println("Conexão aberta!");

            System.out.println(conexao.getClass());
        } catch (SQLException e) {
            System.out.println("Erro de banco de dados");
            e.printStackTrace();
        }
    }

}
```
ou
```java
import java.sql.*;

public class ConexaoBanco {
    public static void main(String[] args) {
        try {
            // Carrega o driver
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Cria a conexão
            String url = "jdbc:mysql://localhost:3306/meu_banco";
            String user = "seu_usuario";
            String password = "sua_senha";
            Connection conn = DriverManager.getConnection(url, user, password);

            System.out.println("Conexão estabelecida com sucesso!");

        } catch (ClassNotFoundException | SQLException e) {
            System.out.println("Erro ao conectar ao banco de dados: " + e.getMessage());
        }
    }
}
```
**Explicação do código:**
1. **Carregando o driver:** `Class.forName("com.mysql.cj.jdbc.Driver");`
   * Substitua `com.mysql.cj.jdbc.Driver` pela classe do driver do seu banco de dados.
2. **Criando a conexão:** `DriverManager.getConnection(url, user, password);`
   * `url`: URL de conexão com o banco de dados, incluindo o nome do host, porta e banco de dados.
   * `user`: Nome do usuário do banco de dados.
   * `password`: Senha do usuário do banco de dados.

**Observações:**
* **Informações de conexão:** Certifique-se de substituir as informações de conexão (URL, usuário e senha) pelas informações corretas do seu banco de dados.
* **Tratamento de exceções:** É importante tratar as exceções `ClassNotFoundException` (caso o driver não seja encontrado) e `SQLException` (caso ocorra algum erro na conexão ou na execução de comandos SQL).
* **Fechamento da conexão:** Após utilizar a conexão, é fundamental fechá-la para liberar os recursos. Utilize os métodos `conn.close()` para fechar a conexão e `stmt.close()` para fechar os `Statement` e `ResultSet` que você utilizar.

**Próximos passos:**
Após estabelecer a conexão, você pode executar comandos SQL, como consultas, inserções, atualizações e deleções. Para isso, você utilizará os objetos `Statement`, `PreparedStatement` e `ResultSet`.

**Exemplos de consulta:**
```java
Statement stmt = conn.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM minha_tabela");
while (rs.next()) {
    // Processar os resultados
    String nome = rs.getString("nome");
    int idade = rs.getInt("idade");
    
	System.out.printf("%s - %d", nome, idade)
}
```

```java
try (Statement comando = conexao.createStatement();
	ResultSet resultado = comando.executeQuery("select * from venda")) {
		while (resultado.next()) {
	        Long id = resultado.getLong("id");
	        String nomeCliente = resultado.getString("nome_cliente");
	        BigDecimal valorTotal = resultado.getBigDecimal("valor_total");
	        Date dataPagamento = resultado.getDate("data_pagamento");

	        System.out.printf("%d - %s - R$%.2f - %s%n", id, nomeCliente, valorTotal, dataPagamento);
	    }
} catch (SQLException e) {
            System.out.println("Erro de banco de dados");
            e.printStackTrace();
}
```
---
## Executando Consultas SQL com Statement em Java

**O que é um Statement?**
Em JDBC, um `Statement` é um objeto que representa uma única instrução SQL a ser executada em um banco de dados. Ele é utilizado para enviar comandos SQL simples ao banco de dados e obter os resultados.

**Como utilizar um Statement?**
1. **Criar um Statement:**
   `{java}Statement stmt = conn.createStatement();`
   
   Onde `conn` é o objeto `Connection` que representa a conexão com o banco de dados.

2. **Executar a consulta:**
   `{java}ResultSet rs = stmt.executeQuery("SELECT * FROM minha_tabela");`
   
   * `executeQuery`: Método utilizado para executar consultas que retornam um conjunto de resultados.
   * `ResultSet`: Objeto que armazena os resultados da consulta, permitindo que você itere sobre eles.

3. **Processar os resultados:**
   ```java
   while (rs.next()) {
       String nome = rs.getString("nome");
       int idade = rs.getInt("idade");
       // ...
   }
   ```
   * `rs.next()`: Avança para o próximo registro no conjunto de resultados.
   * `rs.getString("nome")`, `rs.getInt("idade")`: Obtém os valores das colunas especificadas.

**Exemplo completo:**
```java
import java.sql.*;

public class ConsultaExemplo {
    public static void main(String[] args) {
        try (
            // ... (Código para estabelecer a conexão)
            Statement stmt = conn.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM clientes")) {
            while (rs.next()) {
                int id = rs.getInt("id");
                String nome = rs.getString("nome");
                String email = rs.getString("email");
                System.out.println("ID: " + id + ", Nome: " + nome + ", Email: " + email);
            }
            rs.close();
            stmt.close();
            conn.close();
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

**Quando utilizar Statement?**
* **Consultas simples:** Para consultas que não requerem parâmetros dinâmicos ou pré-compilação.
* **Consultas estáticas:** Quando a consulta é conhecida antecipadamente e não precisa ser modificada com frequência.

**Limitações do Statement:**
* **Desempenho:** Para consultas que serão executadas várias vezes com diferentes parâmetros, o `Statement` pode ser menos eficiente do que o `PreparedStatement`, pois a consulta é compilada a cada execução.
* **Segurança:** A inserção direta de valores em uma string SQL pode levar a injeção de SQL, uma vulnerabilidade de segurança.
---
## Executando Consultas SQL com a Cláusula WHERE
**Exemplo:**
```java
import java.sql.*;

public class ConsultaComWhere {
    public static void main(String[] args) {
        try {
            // Carregar o driver JDBC
            Class.forName("com.mysql.jdbc.Driver");

            // Criar a conexão com o banco de dados
            Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/meu_banco", "usuario", "senha");

            // Criar o objeto Statement
            Statement stmt = conn.createStatement();

            // Executar a consulta com a cláusula WHERE
            String sql = "SELECT * FROM clientes WHERE cidade = 'São Paulo'";
            ResultSet rs = stmt.executeQuery(sql);

            // Processar os resultados
            while (rs.next()) {
                int id = rs.getInt("id");
                String nome = rs.getString("nome");
                System.out.println("ID: " + id + ", Nome: " + nome);
            }

            // Fechar os recursos
            rs.close();
            stmt.close();
            conn.close();
        } catch (Exception e) {
            System.out.println("Erro: " + e.getMessage());
        }
    }
}
```
**Explicando o Código:**
1. **Carregar o Driver:** Carrega o driver JDBC específico do seu banco de dados (neste caso, MySQL).
2. **Criar a Conexão:** Estabelece uma conexão com o banco de dados, fornecendo as informações de URL, usuário e senha.
3. **Criar o Statement:** Cria um objeto `Statement` para executar as consultas SQL.
4. **Executar a Consulta:** Executa a consulta SQL, especificando a tabela (`clientes`) e a condição de filtro (`WHERE cidade = 'São Paulo'`). O resultado é armazenado em um objeto `ResultSet`.
5. **Processar os Resultados:** Itera sobre o `ResultSet`, recuperando os dados de cada linha e imprimindo na tela.
6. **Fechar os Recursos:** Fecha o `ResultSet`, o `Statement` e a conexão para liberar os recursos.

```java
import java.math.BigDecimal;
import java.sql.*;
import java.util.Scanner;

public class Principal {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Pesquisa por nome: ");
        String nomePesquisa = scanner.nextLine();

        try (Connection conexao = DriverManager
                .getConnection("jdbc:mysql://localhost:3306/comercial", "root", "");
             Statement comando = conexao.createStatement();
             ResultSet resultado = comando.executeQuery(
                     "select * from venda where nome_cliente like '%"
                             + nomePesquisa + "%'")) {
            while (resultado.next()) {
                Long id = resultado.getLong("id");
                String nomeCliente = resultado.getString("nome_cliente");
                BigDecimal valorTotal = resultado.getBigDecimal("valor_total");
                Date dataPagamento = resultado.getDate("data_pagamento");

                System.out.printf("%d - %s - R$%.2f - %s%n",
                        id, nomeCliente, valorTotal, dataPagamento);
            }
        } catch (SQLException e) {
            System.out.println("Erro de banco de dados");
            e.printStackTrace();
        }
    }
}
```
---
## Executando Consultas SQL com PreparedStatement
O `PreparedStatement` é uma interface do JDBC que oferece uma maneira mais segura e eficiente de executar consultas SQL em comparação com o `Statement`. Ao utilizar `PreparedStatement`, você pré-compila a sua consulta, separando a estrutura da consulta dos dados que serão inseridos. Isso traz diversos benefícios:

### Por que usar PreparedStatement?
* **Prevenção de Injeção SQL:** Uma das principais vantagens é a proteção contra ataques de injeção SQL. Ao utilizar parâmetros, você impede que códigos maliciosos sejam inseridos diretamente na consulta, garantindo a integridade dos seus dados.
* **Melhora de Performance:** A pré-compilação da consulta permite que o banco de dados otimize a execução, resultando em um melhor desempenho, especialmente para consultas que são executadas várias vezes com diferentes valores.
* **Facilidade de Uso:** A separação da estrutura da consulta dos dados facilita a criação de consultas dinâmicas, permitindo que você altere apenas os valores dos parâmetros sem precisar reescrever toda a consulta.

### Como funciona o PreparedStatement?
1. **Criação do PreparedStatement:**
   `{java}PreparedStatement pstmt = conn.prepareStatement("SELECT * FROM clientes WHERE nome = ?");`
   Observe o uso do ponto de interrogação (`?`) como marcador de parâmetro.

2. **Configuração dos Parâmetros:**
   `{java}pstmt.setString(1, "João");`
   O primeiro argumento do método `setString` indica a posição do parâmetro (começando em 1) e o segundo argumento é o valor a ser atribuído.

3. **Execução da Consulta:**
   `{java}ResultSet rs = pstmt.executeQuery();`
   O método `executeQuery` executa a consulta e retorna um `ResultSet` com os resultados.

### Exemplo Completo:
```java
import java.sql.*;

public class ConsultaComPreparedStatement {
    public static void main(String[] args) {
        try {
            // ... (Código para conectar ao banco de dados)

            String nome = "Maria";
            PreparedStatement pstmt = conn.prepareStatement("SELECT * FROM clientes WHERE nome = ?");
            pstmt.setString(1, nome);

            ResultSet rs = pstmt.executeQuery();

            while (rs.next()) {
                // ... (Processar os resultados)
            }

            // ... (Fechar os recursos)
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

```java
import java.math.BigDecimal;
import java.sql.*;
import java.util.Scanner;

public class Principal {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.print("Pesquisa por nome: ");
        String nomePesquisa = scanner.nextLine();

        try (Connection conexao = DriverManager .getConnection("jdbc:mysql://localhost:3306/comercial", "root", "");
             PreparedStatement comando = conexao .prepareStatement("select * from venda where nome_cliente like ?")) {
            comando.setString(1, "%" + nomePesquisa + "%");
            ResultSet resultado = comando.executeQuery();

            while (resultado.next()) {
                Long id = resultado.getLong("id");
                String nomeCliente = resultado.getString("nome_cliente");
                BigDecimal valorTotal = resultado.getBigDecimal("valor_total");
                Date dataPagamento = resultado.getDate("data_pagamento");

                System.out.printf("%d - %s - R$%.2f - %s%n", id, nomeCliente, valorTotal, dataPagamento);
            }
        } catch (SQLException e) {
            System.out.println("Erro de banco de dados");
            e.printStackTrace();
        }
    }
}
```
### Vantagens em relação ao Statement:

| Característica | Statement                                                  | PreparedStatement                                             |
|:--------------:|:---------------------------------------------------------- |:------------------------------------------------------------- |
|   Segurança    | Suscetível a injeção SQL                                   | Protegido contra injeção SQL                                  |
|  Performance   | Pode ser mais lento para consultas executadas várias vezes | Geralmente mais rápido para consultas executadas várias vezes |
| Flexibilidade  | Menos flexível para consultas dinâmicas                    | Mais flexível para consultas dinâmicas                        |
### Quando usar PreparedStatement?
* Sempre que você precisar inserir valores dinâmicos em uma consulta.
* Quando a mesma consulta será executada várias vezes com diferentes valores.
* Quando a segurança dos dados for uma preocupação.
---
## Executando Comandos DML (Data Manipulation Language)
**Comandos DML** são responsáveis por manipular os dados em um banco de dados relacional. Eles permitem que você **insira**, **atualize** e **exclua** registros em suas tabelas.

**Os principais comandos DML são:**
* **INSERT:** Insere novos registros em uma tabela.
* **UPDATE:** Atualiza os valores de registros existentes.
* **DELETE:** Remove registros de uma tabela.

### INSERT: Inserindo Novos Registros
O comando `INSERT` adiciona uma nova linha a uma tabela.
```sql
INSERT INTO tabela (coluna1, coluna2, ...)
VALUES (valor1, valor2, ...);
```

* **tabela:** O nome da tabela onde os dados serão inseridos.
* **coluna1, coluna2, ...:** As colunas que receberão os valores.
* **valor1, valor2, ...:** Os valores correspondentes a cada coluna.

**Exemplo:**
```sql
INSERT INTO clientes (nome, email, cidade)
VALUES ('João Silva', 'joao@email.com', 'São Paulo');
```

### UPDATE: Atualizando Registros Existentes
O comando `UPDATE` modifica os valores de registros existentes em uma tabela. É crucial utilizar a cláusula `WHERE` para especificar quais registros serão atualizados.
```sql
UPDATE tabela
SET coluna1 = novo_valor1, coluna2 = novo_valor2, ...
WHERE condição;
```

* **tabela:** O nome da tabela a ser atualizada.
* **SET:** Especifica as colunas a serem atualizadas e seus novos valores.
* **WHERE:** Define a condição para filtrar os registros a serem modificados.

**Exemplo:**
```sql
UPDATE clientes
SET email = 'joao@novasoemail.com'
WHERE id = 1;
```

### DELETE: Excluindo Registros
O comando `DELETE` remove registros de uma tabela. Assim como no `UPDATE`, é fundamental utilizar a cláusula `WHERE` para evitar exclusões indesejadas.
```sql
DELETE FROM tabela
WHERE condição;
```

* **tabela:** O nome da tabela da qual os registros serão removidos.
* **WHERE:** Define a condição para filtrar os registros a serem excluídos.

**Exemplo:**
```sql
DELETE FROM pedidos
WHERE data_pedido < '2023-01-01';
```

### Considerações Importantes:
* **Cuidado com o DELETE:** Ao utilizar o `DELETE` sem a cláusula `WHERE`, você excluirá todos os registros da tabela.
* **Transações:** Para garantir a integridade dos dados, utilize transações. As transações permitem agrupar várias operações DML e garantir que todas sejam executadas ou nenhuma seja executada.
* **Índices:** Crie índices nas colunas que são frequentemente utilizadas nas cláusulas `WHERE` para melhorar o desempenho das consultas.
* **Backups:** Realize backups regularmente para se proteger contra perdas de dados.

### Exemplos:
```java
try {
    // Inserir um novo cliente
    String insertSql = "INSERT INTO clientes (nome, email) VALUES (?, ?)";
    PreparedStatement insertStmt = conn.prepareStatement(insertSql);
    insertStmt.setString(1, "Ana Silva");
    insertStmt.setString(2, "ana@email.com");
    insertStmt.executeUpdate();
    
    // Atualizar o email de um cliente
    String updateSql = "UPDATE clientes SET email = ? WHERE id = ?";
    PreparedStatement updateStmt = conn.prepareStatement(updateSql);
    updateStmt.setString(1, "novoemail@email.com");
    updateStmt.setInt(2, 1);
    updateStmt.executeUpdate();
    
    // Excluir um cliente
    String deleteSql = "DELETE FROM clientes WHERE id = ?";
    PreparedStatement deleteStmt = conn.prepareStatement(deleteSql);
    deleteStmt.setInt(1, 2);
    deleteStmt.executeUpdate();

    // ... (Fechar os recursos)
} catch (SQLException e) {
    e.printStackTrace();
}
```

```java
Scanner scanner = new Scanner(System.in);
System.out.print("Nome: ");
String nome = scanner.nextLine();

System.out.print("Valor total: ");
BigDecimal valorTotal = new BigDecimal(scanner.nextLine());

System.out.print("Data de pagamento: ");
LocalDate dataPagamento = LocalDate.parse(scanner.nextLine(), DateTimeFormatter.ofPattern("dd/MM/yyyy"));

String dml = """
        insert into venda (
            nome_cliente,
            valor_total,
            data_pagamento
        ) values (?, ?, ?)
        """;

try (Connection conexao = DriverManager
        .getConnection("jdbc:mysql://localhost:3306/comercial", "root", "");
     PreparedStatement comando = conexao.prepareStatement(dml)) {
    comando.setString(1, nome);
    comando.setBigDecimal(2, valorTotal);
    comando.setDate(3, Date.valueOf(dataPagamento));
    comando.executeUpdate();

    System.out.println("Venda cadastrada!");
} catch (SQLException e) {
    System.out.println("Erro cadastrando venda");
    e.printStackTrace();
}
```
---
## Obtendo o Código de Autoincremento Gerado após a Inserção
Muitas vezes, ao inserir um novo registro em um banco de dados, desejamos que um campo específico, geralmente uma chave primária, seja preenchido automaticamente com um valor numérico único e crescente. Esse mecanismo é conhecido como **autoincremento**. Ele garante a unicidade dos registros e facilita a organização dos dados.

**Exemplos:**
```java
try (Connection conexao = DriverManager.getConnection("jdbc:mysql://localhost:3306/comercial", "root", "");
	 PreparedStatement comando = conexao.prepareStatement(dml, Statement.RETURN_GENERATED_KEYS)) {
    comando.setString(1, nome);
    comando.setBigDecimal(2, valorTotal);
    comando.setDate(3, Date.valueOf(dataPagamento));
    comando.executeUpdate();

    ResultSet codigoResultSet = comando.getGeneratedKeys();
    codigoResultSet.next();
    long codigoGerado = codigoResultSet.getLong(1);

    System.out.println("Venda cadastrada com código " + codigoGerado + "!");
} catch (SQLException e) {
    System.out.println("Erro cadastrando venda");
    e.printStackTrace();
}
```


```java
import java.sql.*;

// ... (código para conectar ao banco de dados)

PreparedStatement stmt = conn.prepareStatement("INSERT INTO clientes (nome, email) VALUES (?, ?)", Statement.RETURN_GENERATED_KEYS);
stmt.setString(1, "João Silva");
stmt.setString(2, "joao@email.com");
int rowsAffected = stmt.executeUpdate();

if (rowsAffected > 0) {
    ResultSet rs = stmt.getGeneratedKeys();
    if (rs.next()) {
        int id = rs.getInt(1);
        System.out.println("O ID gerado é: " + id);
    }
}
```
**Explicando o Código:**
1. **Preparando o Statement:** Ao criar o `PreparedStatement`, passamos o parâmetro `Statement.RETURN_GENERATED_KEYS` para indicar que queremos recuperar as chaves geradas.
2. **Executando a Inserção:** O método `executeUpdate()` retorna o número de linhas afetadas pela inserção.
3. **Obtendo as Chaves Geradas:** O método `getGeneratedKeys()` retorna um `ResultSet` contendo as chaves geradas.
4. **Recuperando o Valor:** Navegamos para o primeiro registro do `ResultSet` e obtemos o valor da primeira coluna (que é o ID gerado).

**Outras Considerações:**
* **Sequências:** Alguns bancos de dados utilizam sequências para gerar valores autoincrementados. Nesses casos, você pode consultar a sequência para obter o último valor gerado.
* **Transações:** Se você estiver trabalhando com transações, certifique-se de que o valor do autoincremento seja obtido após o commit da transação.
* **Performance:** A forma de obter o valor gerado pode impactar o desempenho da sua aplicação. Avalie as diferentes opções e escolha a que melhor se adapta às suas necessidades.
---
## Gerenciando Transações com JDBC
Uma transação em um banco de dados é um conjunto de operações que são tratadas como uma única unidade de trabalho. Ou seja, todas as operações dentro de uma transação devem ser concluídas com sucesso para que os dados sejam persistidos no banco de dados. Caso ocorra algum erro durante a execução da transação, todas as alterações são desfeitas (rollback).

**Por que utilizar transações?**
* **Integridade dos dados:** Garante que os dados sejam consistentes, evitando situações em que apenas parte de uma operação seja concluída.
* **Atomicidade:** As operações dentro de uma transação são indivisíveis. Ou todas ocorrem, ou nenhuma ocorre.
* **Isolamento:** As transações ocorrem de forma isolada, evitando que uma transação interfira nos resultados de outra.
* **Durabilidade:** Uma vez que uma transação é confirmada (commit), as alterações são permanentes, mesmo em caso de falhas no sistema.

**1. Desabilitando o Autocommit:**
Por padrão, o modo autocommit está habilitado, ou seja, cada instrução SQL é automaticamente confirmada. Para controlar manualmente as transações, é necessário desabilitar o autocommit:

```java
Connection conn = DriverManager.getConnection(url, user, password);
conn.setAutoCommit(false);
```

**2. Executando as Operações DML:**
Com o autocommit desabilitado, você pode executar várias instruções SQL. Se todas as instruções forem executadas com sucesso, você confirma a transação. Caso contrário, você reverte a transação.

```java
PreparedStatement pstmt = conn.prepareStatement("INSERT INTO clientes (nome, email) VALUES (?, ?)");
pstmt.setString(1, "João Silva");
pstmt.setString(2, "joao@email.com");
pstmt.executeUpdate();

pstmt.setString(1, "Maria Souza");
pstmt.setString(2, "maria@email.com");
pstmt.executeUpdate();
```

**3. Confirmando ou Revertendo a Transação:**
* **Confirmar:**
  `{java}conn.commit();`
* **Reverter:**
  `{java}conn.rollback();`

**Exemplo Completo:**
```java
import java.sql.*;

public class TransacaoExemplo {
    public static void main(String[] args) {
        try {
            // ... (Código para conectar ao banco de dados)

            conn.setAutoCommit(false);

            // Inserir dois clientes
            // ... (Código para inserir os clientes)

            // Confirmar a transação
            conn.commit();

        } catch (SQLException e) {
            try {
                conn.rollback(); // Reverter a transação em caso de erro
            } catch (SQLException ex) {
                // ...
            }
            e.printStackTrace();
        } finally {
            // ... (Fechar os recursos)
        }
    }
}
```

**Considerações Importantes:**
* **Bloco try-catch:** É fundamental utilizar um bloco `try-catch` para capturar possíveis exceções e realizar o rollback da transação.
* **Finally:** Utilize o bloco `finally` para garantir que os recursos sejam fechados corretamente, independentemente de ocorrer ou não uma exceção.
* **Isolamento:** O nível de isolamento das transações pode variar dependendo do banco de dados. Consulte a documentação do seu banco de dados para obter mais informações.
* **Performance:** O uso excessivo de transações pode afetar o desempenho do banco de dados. Utilize transações de forma estratégica, agrupando operações relacionadas.

**Outras Funcionalidades:**
* **Savepoints:** Permitem criar pontos de restauração dentro de uma transação, permitindo reverter para um estado anterior.
* **Transações Distribuídas:** Envolvem múltiplos bancos de dados e requerem um gerenciador de transações.

**Outro Exemplo Completo:**
```java
import java.math.BigDecimal;
import java.sql.*;
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.util.Scanner;

public class Cadastro {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String dml = """
                insert into venda (
                    nome_cliente,
                    valor_total,
                    data_pagamento
                ) values (?, ?, ?)
                """;

        try (Connection conexao = DriverManager
                .getConnection("jdbc:mysql://localhost:3306/comercial", "root", "");
             PreparedStatement comando = conexao.prepareStatement(dml, Statement.RETURN_GENERATED_KEYS)) {
            conexao.setAutoCommit(false);

            try {
                do {
                    System.out.print("Nome: ");
                    String nome = scanner.nextLine();

                    System.out.print("Valor total: ");
                    BigDecimal valorTotal = new BigDecimal(scanner.nextLine());

                    System.out.print("Data de pagamento: ");
                    LocalDate dataPagamento = LocalDate.parse(scanner.nextLine(),
                            DateTimeFormatter.ofPattern("dd/MM/yyyy"));

                    comando.setString(1, nome);
                    comando.setBigDecimal(2, valorTotal);
                    comando.setDate(3, Date.valueOf(dataPagamento));
                    comando.executeUpdate();

                    ResultSet codigoResultSet = comando.getGeneratedKeys();
                    codigoResultSet.next();
                    long codigoGerado = codigoResultSet.getLong(1);

                    System.out.println("Venda cadastrada com código " + codigoGerado + "!");

                    System.out.print("Continuar? ");
                } while ("sim".equalsIgnoreCase(scanner.nextLine()));

                conexao.commit();
            } catch (Exception e) {
                conexao.rollback();
                throw new RuntimeException(e);
            }
        } catch (Exception e) {
            System.out.println("Erro cadastrando venda");
            e.printStackTrace();
        }
    }
}
```