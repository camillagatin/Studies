## Introdução à API Clássica de I/O
Uma **API de I/O (Input/Output)**, ou Interface de Programação de Aplicações de Entrada e Saída, é um conjunto de funções e rotinas que permitem a um programa interagir com dispositivos externos, como o teclado, o mouse, o disco rígido, a rede, etc. Essas APIs fornecem uma camada de abstração, facilitando o desenvolvimento de programas que precisam realizar operações de entrada e saída, sem que o programador precise se preocupar com os detalhes de baixo nível de cada dispositivo.

### A API Clássica de I/O
A API clássica de I/O, também conhecida como **API de sistema de arquivos**, é a interface mais básica para realizar operações de entrada e saída em sistemas operacionais. Ela fornece um conjunto de funções para criar, abrir, fechar, ler e escrever arquivos, além de outras operações relacionadas a diretórios e dispositivos de bloco.

**Características da API Clássica:**
* **Baseada em arquivos:** A maioria das operações é centrada em arquivos, que são abstrações de dispositivos de armazenamento.
* **Bloqueante:** Muitas funções da API clássica são bloqueantes, o que significa que o processo que chama a função é bloqueado até que a operação seja concluída.
* **Síncrona:** As operações são realizadas de forma síncrona, ou seja, a chamada a uma função de I/O só retorna quando a operação é concluída.
* **Simples:** A API clássica é relativamente simples e fácil de usar, o que a torna adequada para muitas aplicações.

**Limitações da API Clássica:**
* **Desempenho:** Em algumas situações, a API clássica pode apresentar um desempenho inferior, especialmente em aplicações que realizam um grande número de operações de I/O de forma concorrente.
* **Escalabilidade:** A API clássica pode não ser a melhor opção para aplicações altamente escaláveis, que precisam lidar com um grande número de requisições de I/O simultaneamente.
* **Complexidade:** Para aplicações mais complexas, como servidores web e bancos de dados, a API clássica pode não fornecer todas as funcionalidades necessárias.

### Funcionalidades típicas da API Clássica de I/O
* **Abertura e fechamento de arquivos:** `open()`, `close()`
* **Leitura e escrita de dados:** `read()`, `write()`
* **Busca dentro de arquivos:** `seek()`
* **Obtenção de informações sobre arquivos:** `stat()`
* **Criação e remoção de arquivos:** `create()`, `remove()`
* **Manipulação de diretórios:** `mkdir()`, `rmdir()`, `chdir()`

### Exemplos de uso
```c
#include <stdio.h>

int main() {
    FILE *fp;
    char buffer[100];

    // Abre um arquivo para leitura
    fp = fopen("meu_arquivo.txt", "r");
    if (fp == NULL) {
        perror("Erro ao abrir o arquivo");
        return 1;
    }

    // Lê uma linha do arquivo
    fgets(buffer, 100, fp);

    // Imprime o conteúdo do buffer
    printf("%s", buffer);

    // Fecha o arquivo
    fclose(fp);

    return 0;
}
```
---
## Instanciando e Criando Arquivos e Pastas com a Classe File em Java
A classe `File` oferece uma interface para interagir com o sistema de arquivos, permitindo criar, apagar, navegar e inspecionar arquivos e diretórios. É uma ferramenta fundamental para qualquer desenvolvedor Java que precise manipular o sistema de arquivos.

### Instanciando um Objeto File
Para criar um objeto `File`, você precisa fornecer o caminho para o arquivo ou diretório que deseja representar:
```java
import java.io.File;

// Criando um objeto File para um arquivo existente
File arquivo = new File("C:\\meus_arquivos\\documento.txt");

// Criando um objeto File para um diretório
File diretorio = new File("C:\\meus_arquivos");
```

### Criando um Novo Arquivo
Para criar um novo arquivo, você pode utilizar o método `createNewFile()`:
```java
import java.io.File;
import java.io.IOException;

public class CriarArquivo {
    public static void main(String[] args) {
        try {
            File novoArquivo = new File("C:\\meus_arquivos\\novo_arquivo.txt");
            if (novoArquivo.createNewFile()) {
                System.out.println("Arquivo criado com sucesso!");
            } else {
                System.out.println("O arquivo já existe.");
            }
        } catch (IOException e) {
            System.out.println("Erro ao criar o arquivo: " + e.getMessage());
        }
    }
}
```

**Observações:**
* O método `createNewFile()` retorna `true` se o arquivo foi criado com sucesso e `false` se ele já existir.
* É recomendado envolver a chamada ao método `createNewFile()` em um bloco `try-catch` para tratar possíveis exceções de I/O.

### Criando um Novo Diretório
Para criar um novo diretório, você pode utilizar o método `mkdir()` ou `mkdirs()`:
```java
import java.io.File;

public class CriarDiretorio {
    public static void main(String[] args) {
        File novoDiretorio = new File("C:\\meus_arquivos\\novo_diretorio");

        if (novoDiretorio.mkdir()) {
            System.out.println("Diretório criado com sucesso!");
        } else {
            System.out.println("O diretório já existe ou ocorreu um erro.");
        }
    }
}
```
* **`mkdir()`:** Cria um único diretório. Se algum dos diretórios pais não existir, a operação falhará.
* **`mkdirs()`:** Cria o diretório e todos os diretórios pais necessários.

### Outros Métodos Úteis
A classe `File` oferece diversos outros métodos úteis para manipulação de arquivos e diretórios:
* **`exists()`:** Verifica se um arquivo ou diretório existe.
* **`delete()`:** Exclui um arquivo ou diretório vazio.
* **`renameTo()`:** Renomeia um arquivo ou diretório.
* **`isDirectory()`:** Verifica se um caminho representa um diretório.
* **`isFile()`:** Verifica se um caminho representa um arquivo.
* **`listFiles()`:** Retorna uma lista de arquivos e subdiretórios dentro de um diretório.
* **`length()`:** Retorna o tamanho de um arquivo em bytes.
* **`lastModified()`:** Retorna a última data de modificação de um arquivo.

### Exemplo Completo
```java
import java.io.File;

public class ExemploFile {
    public static void main(String[] args) {
        File diretorioRaiz = new File("C:\\meus_arquivos");

        // Criando um novo diretório dentro do diretório raiz
        File novoDiretorio = new File(diretorioRaiz, "subdiretorio");
        novoDiretorio.mkdir();

        // Criando um novo arquivo dentro do novo diretorio
        File novoArquivo = new File(novoDiretorio, "arquivo.txt");
        try {
            novoArquivo.createNewFile();
        } catch (Exception e) {
            System.out.println("Erro ao criar o arquivo: " + e.getMessage());
        }

        // Listando os arquivos e subdiretórios do diretório raiz
        File[] listaArquivos = diretorioRaiz.listFiles();
        for (File arquivo : listaArquivos) {
            System.out.println(arquivo.getName());
        }
    }
}
```
---
## Obtendo o Caminho Absoluto e Canônico de um Objeto File
* **Caminho Absoluto:** Representa a localização completa de um arquivo ou diretório a partir da raiz do sistema de arquivos. Ele inclui todas as subpastas necessárias para chegar ao arquivo.
* **Caminho Canônico:** É uma forma normalizada do caminho absoluto, onde os links simbólicos são resolvidos e os componentes redundantes (como "../") são removidos.

### Métodos para Obter Caminhos em Objetos File
A classe `File` oferece diversos métodos para obter informações sobre o caminho de um arquivo ou diretório:

#### 1. getAbsolutePath()
* Retorna o caminho absoluto do arquivo ou diretório representado pelo objeto File.
* **Exemplo:**
  ```java
  File file = new File("arquivo.txt");
  String caminhoAbsoluto = file.getAbsolutePath();
  System.out.println(caminhoAbsoluto); // Imprime algo como "C:\Users\seu_usuario\Documents\arquivo.txt"
  ```

#### 2. getCanonicalPath()
* Retorna o caminho canônico do arquivo ou diretório.
* **Exemplo:**
  ```java
  File file = new File("arquivo.txt");
  try {
      String caminhoCanonico = file.getCanonicalPath();
      System.out.println(caminhoCanonico);
  } catch (IOException e) {
      // Tratar exceção caso ocorra algum problema ao obter o caminho canônico
      e.printStackTrace();
  }
  ```
  **Observação:** O método `getCanonicalPath()` pode lançar uma `IOException` se houver problemas ao resolver links simbólicos ou acessar o sistema de arquivos.

#### 3. getPath()
* Retorna o caminho original que foi passado para o construtor do objeto File.
* **Exemplo:**
  ```java
  File file = new File("arquivo.txt");
  String caminhoOriginal = file.getPath();
  System.out.println(caminhoOriginal); // Imprime "arquivo.txt"
  ```

### Quando Usar Cada Método?
* **getAbsolutePath():** Ideal para obter o caminho completo do arquivo, mesmo que ele tenha sido especificado com um caminho relativo.
* **getCanonicalPath():** Utilizado quando você precisa de uma representação normalizada e resolvida do caminho, especialmente ao lidar com links simbólicos.
* **getPath():** Útil para obter o caminho original que foi fornecido ao criar o objeto File.

### Exemplo Completo
```java
import java.io.File;
import java.io.IOException;

public class CaminhosFile {
    public static void main(String[] args) {
        File arquivo = new File("..\\dados\\arquivo.txt");

        try {
            System.out.println("Caminho absoluto: " + arquivo.getAbsolutePath());
            System.out.println("Caminho canônico: " + arquivo.getCanonicalPath());
            System.out.println("Caminho original: " + arquivo.getPath());
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**Observações:**
* **Caminhos Relativos:** Se você passar um caminho relativo para o construtor de `File`, os métodos `getAbsolutePath()` e `getCanonicalPath()` irão resolver o caminho em relação ao diretório corrente da sua aplicação.
* **Links Simbólicos:** O método `getCanonicalPath()` é especialmente útil para lidar com links simbólicos, pois ele resolve esses links e retorna o caminho real do arquivo.
* **Exceções:** É importante tratar a exceção `IOException` que pode ser lançada por `getCanonicalPath()`, especialmente ao trabalhar com sistemas de arquivos remotos ou com configurações de segurança mais restritivas.
---
## Excluindo, Renomeando e Movendo Arquivos e Pastas com a Classe File
A classe `File` em Java oferece métodos para realizar diversas operações no sistema de arquivos, incluindo exclusão, renomeação e movimentação de arquivos e pastas.

### Excluindo Arquivos e Pastas
Para excluir um arquivo ou uma pasta, utilizamos o método `delete()`:
```java
import java.io.File;

public class ExcluirArquivo {
    public static void main(String[] args) {
        File arquivoParaExcluir = new File("C:\\temp\\arquivo.txt");
        File diretorioParaExcluir = new File("C:\\temp\\pasta_vazia");

        if (arquivoParaExcluir.delete()) {
            System.out.println("Arquivo excluído com sucesso.");
        } else {
            System.out.println("Erro ao excluir o arquivo.");
        }

        if (diretorioParaExcluir.delete()) {
            System.out.println("Diretório excluído com sucesso.");
        } else {
            System.out.println("Erro ao excluir o diretório. Verifique se o diretório está vazio.");
        }
    }
}
```
**Observações:**
* **Diretórios:** Para excluir um diretório, ele precisa estar vazio. Caso contrário, o método `delete()` retornará `false`.
* **Exceções:** É recomendado envolver as chamadas ao método `delete()` em um bloco `try-catch` para tratar possíveis exceções de I/O.

### Renomeando Arquivos e Pastas
Para renomear um arquivo ou uma pasta, utilizamos o método `renameTo()`:
```java
import java.io.File;

public class RenomearArquivo {
    public static void main(String[] args) {
        File arquivo = new File("C:\\temp\\arquivo.txt");
        File novoNome = new File("C:\\temp\\novo_nome.txt");

        if (arquivo.renameTo(novoNome)) {
            System.out.println("Arquivo renomeado com sucesso.");
        } else {
            System.out.println("Erro ao renomear o arquivo.");
        }
    }
}
```
**Observações:**
* O método `renameTo()` move o arquivo para o novo local. Se o novo nome já existir, a operação falhará.

### Movendo Arquivos e Pastas
Mover um arquivo ou pasta é equivalente a renomeá-lo para um novo local. Portanto, utilizamos o mesmo método `renameTo()` para realizar essa operação.

```java
import java.io.File;

public class MoverArquivo {
    public static void main(String[] args) {
        File arquivo = new File("C:\\temp\\arquivo.txt");
        File novoLocal = new File("C:\\nova_pasta");

        File destino = new File(novoLocal, arquivo.getName());

        if (arquivo.renameTo(destino)) {
            System.out.println("Arquivo movido com sucesso.");
        } else {
            System.out.println("Erro ao mover o arquivo.");
        }
    }
}
```
**Observações:**
* **Criação de Diretório:** Se o diretório de destino não existir, ele será criado automaticamente.
* **Sobrescrita:** Se um arquivo com o mesmo nome já existir no destino, ele será sobrescrito.

### Considerações Importantes
* **Permissões:** Certifique-se de que sua aplicação tenha as permissões necessárias para realizar as operações no sistema de arquivos.
* **Exceções:** Sempre trate as exceções que podem ocorrer durante a manipulação de arquivos e diretórios.
* **Eficiência:** Para mover grandes quantidades de dados, considere utilizar bibliotecas de terceiros que oferecem otimizações de desempenho.
* **Segurança:** Ao excluir ou mover arquivos, tenha cuidado para não apagar dados importantes por engano.

**Exemplo Completo: Mover Todos os Arquivos .txt de uma Pasta para Outra**
```java
import java.io.File;

public class MoverArquivosTxt {
    public static void main(String[] args) {
        File origem = new File("C:\\temp");
        File destino = new File("C:\\nova_pasta");

        File[] arquivos = origem.listFiles((dir, name) -> name.endsWith(".txt"));

        for (File arquivo : arquivos) {
            File novoDestino = new File(destino, arquivo.getName());
            if (arquivo.renameTo(novoDestino)) {
                System.out.println("Arquivo movido: " + arquivo.getName());
            } else {
                System.out.println("Erro ao mover o arquivo: " + arquivo.getName());
            }
        }
    }
}
```
**Este código:**
1. Lista todos os arquivos .txt em um diretório.
2. Move cada arquivo para um novo diretório.
3. Imprime mensagens informando sobre o sucesso ou falha da operação.
---
## Obtendo Informações de Arquivos e Diretórios
A classe `File` oferece uma rica API para interagir com o sistema de arquivos, permitindo não apenas criar, modificar e excluir arquivos e diretórios, mas também obter diversas informações sobre eles.

### Informações Básicas
* **Existência:**
  * `exists()`: Verifica se o arquivo ou diretório existe.
* **Tipo:**
  * `isFile()`: Verifica se é um arquivo regular.
  * `isDirectory()`: Verifica se é um diretório.
* **Nome:**
  * `getName()`: Retorna o nome do arquivo ou diretório.
* **Caminho:**
  * `getPath()`: Retorna o caminho relativo.
  * `getAbsolutePath()`: Retorna o caminho absoluto.
  * `getCanonicalPath()`: Retorna o caminho canônico, resolvendo links simbólicos.

### Informações Detalhadas
* **Tamanho:**
  * `length()`: Retorna o tamanho do arquivo em bytes.
* **Data de Modificação:**
  * `lastModified()`: Retorna o milissegundos desde 1º de janeiro de 1970 para a última modificação.
* **Informações do Sistema:**
  * `canRead()`, `canWrite()`, `canExecute()`: Verificam as permissões de leitura, escrita e execução.
  * `isHidden()`: Verifica se o arquivo está oculto.

### Listando Conteúdo de um Diretório
* `listFiles()`: Retorna um array de `File` representando os arquivos e subdiretórios.
* `listFiles(FilenameFilter filter)`: Permite filtrar os arquivos listados.

### Exemplo Completo:
```java
import java.io.File;

public class InformacoesArquivo {
    public static void main(String[] args) {
        File arquivo = new File("C:\\meus_arquivos\\documento.txt");

        if (arquivo.exists()) {
            System.out.println("O arquivo existe.");
            System.out.println("É um arquivo? " + arquivo.isFile());
            System.out.println("É um diretório? " + arquivo.isDirectory());
            System.out.println("Tamanho: " + arquivo.length() + " bytes");
            System.out.println("Última modificação: " + new java.util.Date(arquivo.lastModified()));
            System.out.println("Caminho absoluto: " + arquivo.getAbsolutePath());
        } else {
            System.out.println("O arquivo não existe.");
        }
    }
}
```

### Trabalhando com Diretórios
Para listar os arquivos em um diretório:
```java
File diretorio = new File("C:\\meus_arquivos");
File[] arquivos = diretorio.listFiles();
for (File arquivo : arquivos) {
    System.out.println(arquivo.getName());
}
```

**Filtrando Arquivos:**
```java
File[] arquivosTxt = diretorio.listFiles((dir, name) -> name.endsWith(".txt"));
```

### Considerações Adicionais:
* **Performance:** Para grandes diretórios, listar todos os arquivos de uma vez pode ser ineficiente. Considere utilizar `listFiles()` com um filtro ou bibliotecas especializadas.
* **Exceções:** Sempre trate as possíveis exceções, como `IOException`, que podem ocorrer ao interagir com o sistema de arquivos.
* **Caminhos Relativos:** Se você fornecer um caminho relativo, o método `getAbsolutePath()` irá resolvê-lo em relação ao diretório corrente da sua aplicação.
* **Links Simbólicos:** O método `getCanonicalPath()` é útil para resolver links simbólicos e obter o caminho real do arquivo.
---
## Listando Arquivos e Diretórios
A classe `File` oferece ferramentas poderosas para interagir com o sistema de arquivos, incluindo a listagem de arquivos e diretórios. Vamos explorar as diferentes formas de realizar essa tarefa.

### Listando Todos os Arquivos e Subdiretórios
```java
import java.io.File;

public class ListarArquivos {
    public static void main(String[] args) {
        File diretorio = new File("C:\\meus_arquivos");

        // Listar todos os arquivos e subdiretórios
        File[] arquivos = diretorio.listFiles();

        for (File arquivo : arquivos) {
            System.out.println(arquivo.getName());
        }
    }
}
```
O código acima:
1. Cria um objeto `File` representando o diretório que você deseja listar.
2. Utiliza o método `listFiles()` para obter um array de `File` contendo todos os arquivos e subdiretórios dentro do diretório especificado.
3. Itera sobre o array, imprimindo o nome de cada elemento.

### Filtrando Arquivos por Extensão
```java
import java.io.File;

public class ListarArquivosPorExtensao {
    public static void main(String[] args) {
        File diretorio = new File("C:\\meus_arquivos");

        // Filtrar apenas arquivos com extensão .txt
        File[] arquivosTxt = diretorio.listFiles((dir, name) -> name.endsWith(".txt"));

        for (File arquivo : arquivosTxt) {
            System.out.println(arquivo.getName());
        }
    }
}
```
Neste exemplo, utilizamos um `FilenameFilter` para filtrar os arquivos. A expressão lambda `(dir, name) -> name.endsWith(".txt")` verifica se o nome do arquivo termina com ".txt".

### Listando Recursivamente Todos os Arquivos
Para listar todos os arquivos em um diretório e seus subdiretórios recursivamente, você pode implementar uma função recursiva:
```java
import java.io.File;

public class ListarArquivosRecursivamente {
    public static void listarArquivos(File diretorio) {
        File[] arquivos = diretorio.listFiles();

        for (File arquivo : arquivos) {
            if (arquivo.isDirectory()) {
                listarArquivos(arquivo);
            } else {
                System.out.println(arquivo.getAbsolutePath());
            }
        }
    }

    public static void main(String[] args) {
        File diretorio = new File("C:\\meus_arquivos");
        listarArquivos(diretorio);
    }
}
```
A função `listarArquivos` verifica se cada elemento é um diretório. Se for, ela chama recursivamente a si mesma para listar os arquivos dentro desse subdiretório.

### Outros Métodos Úteis
* **`listFiles(FileFilter filter)`:** Permite filtrar os arquivos usando um objeto `FileFilter`.
* **`walk()`:** (Java 8+) Permite percorrer um diretório e seus subdiretórios de forma mais funcional.
---
## Entendendo Streams de Entrada e Saída (I/O) e Streams Orientados a Bytes em Java
### O que são Streams?
Streams são abstrações que representam uma sequência contínua de dados. Eles fornecem uma maneira conveniente de ler dados de uma fonte (como um arquivo, uma rede ou um dispositivo de entrada) e escrever dados para um destino.

**Tipos de Streams:**
* **InputStream:** Representa uma sequência de bytes para leitura.
* **OutputStream:** Representa uma sequência de bytes para escrita.

### Streams Orientados a Bytes
Streams orientados a bytes operam em nível de byte, ou seja, leem ou escrevem dados em unidades de 8 bits. Eles são os mais básicos e são usados para uma ampla variedade de operações de entrada e saída.

**Por que usar streams orientados a bytes?**
* **Flexibilidade:** Permitem lidar com qualquer tipo de dado, desde texto até dados binários.
* **Eficiência:** São eficientes para operações de baixo nível.
* **Base para outros streams:** Muitos outros tipos de streams (como streams de caracteres) são construídos sobre os streams de bytes.

**Classes principais:**
* **InputStream:** Classe abstrata que representa a fonte de dados.
    * Subclasses comuns:
        * `FileInputStream`: Lê dados de um arquivo.
        * `ByteArrayInputStream`: Lê dados de um array de bytes.
        * `BufferedInputStream`: Adiciona um buffer para melhorar o desempenho da leitura.
* **OutputStream:** Classe abstrata que representa o destino dos dados.
    * Subclasses comuns:
        * `FileOutputStream`: Escreve dados em um arquivo.
        * `ByteArrayOutputStream`: Escreve dados em um array de bytes.
        * `BufferedOutputStream`: Adiciona um buffer para melhorar o desempenho da escrita.

### Exemplo Prático: Copiando um Arquivo
```java
import java.io.*;

public class CopiarArquivo {
    public static void main(String[] args) throws IOException {
        FileInputStream in = new FileInputStream("arquivo_original.txt");
        FileOutputStream out = new FileOutputStream("novo_arquivo.txt");

        byte[] buffer = new byte[1024];
        int bytesLidos;
        while ((bytesLidos = in.read(buffer)) != -1) {
            out.write(buffer, 0, bytesLidos);
        }

        in.close();
        out.close();
    }
}
```
**Explicação:**
1. **Criar streams:** Criamos um `FileInputStream` para ler o arquivo original e um `FileOutputStream` para escrever no novo arquivo.
2. **Buffer:** Um array de bytes é usado como buffer para transferir dados em blocos, melhorando o desempenho.
3. **Loop de leitura e escrita:** Enquanto houver dados para ler, lemos um bloco de bytes do `InputStream` e escrevemos no `OutputStream`.
4. **Fechar streams:** Ao final, fechamos os streams para liberar os recursos.

### Vantagens dos Streams Orientados a Bytes
* **Versatilidade:** Podem ser usados para uma ampla variedade de tarefas, como ler e escrever arquivos, processar dados de rede, etc.
* **Eficiência:** Oferecem um controle preciso sobre a leitura e escrita de dados em nível de byte.
* **Base para outros streams:** São a base para streams de caracteres, streams compactados, etc.

### Quando usar Streams Orientados a Bytes?
* **Operações de baixo nível:** Quando você precisa de controle preciso sobre os dados em nível de byte.
* **Processamento de arquivos binários:** Para lidar com arquivos que não são simples arquivos de texto.
* **Criação de formatos de arquivo personalizados:** Quando você precisa definir um formato de arquivo específico.
---
## Lendo Arquivos com FileInputStream
O `FileInputStream` é uma classe fundamental em Java para ler dados de um arquivo. Ele permite que você acesse o conteúdo de um arquivo byte a byte, oferecendo um alto nível de controle sobre a leitura.

**Como funciona o FileInputStream?**
* **Criação:** Você cria um objeto `FileInputStream` passando o caminho do arquivo como parâmetro.
* **Leitura:** Utiliza o método `read()` para ler bytes do arquivo.
* **Fechamento:** Após a leitura, é essencial fechar o stream usando o método `close()`.

**Exemplos:**
```java
import java.io.FileInputStream;
import java.io.IOException;

public class LerArquivo {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("meu_arquivo.txt")) {
            int byteLido;
            while ((byteLido = fis.read()) != -1) {
                System.out.print((char) byteLido);
            }
        } catch (IOException e) {
            System.out.println("Erro ao ler o arquivo: " + e.getMessage());
        }
    }
}
```
**Explicação do código:**
1. **Criar o FileInputStream:** Um objeto `FileInputStream` é criado para o arquivo "meu_arquivo.txt".
2. **Ler byte a byte:** O método `read()` lê um byte por vez. Se o valor retornado for -1, significa que o final do arquivo foi alcançado.
3. **Converter para caractere:** O byte lido é convertido para um caractere e impresso na console.
4. **Tratamento de exceções:** Um bloco `try-with-resources` é utilizado para garantir que o `FileInputStream` seja fechado automaticamente, mesmo que ocorra uma exceção.


```java
import java.io.*;

public class Principal {
    public static void main(String[] args) {
        File arquivoOrigem = new File("docs/contrato.txt");
        InputStream inputStream = null;

        try {
            inputStream = new FileInputStream(arquivoOrigem);
            int conteudo;

            while ((conteudo = inputStream.read()) != -1) {
                System.out.print((char) conteudo);
            }
        } catch (FileNotFoundException e) {
            throw new RuntimeException("Arquivo não encontrado", e);
        } catch (IOException e) {
            throw new RuntimeException("Erro de I/O", e);
        } finally {
            if (inputStream != null) {
                try {
                    inputStream.close();
                } catch (IOException e) {
                    System.out.println("Não foi possível fechar fluxo com arquivo");
                }
            }
        }
    }
}
```

**Lendo em um buffer:**
Para melhorar o desempenho, é comum ler dados em um buffer de bytes:
```java
byte[] buffer = new byte[1024];
int bytesLidos;
while ((bytesLidos = fis.read(buffer)) != -1) {
    // Processar os bytes lidos no buffer
    System.out.write(buffer, 0, bytesLidos);
}
```

**Aplicações:**
* **Leitura de arquivos de texto:** Para processar o conteúdo de arquivos de texto.
* **Leitura de arquivos binários:** Para ler qualquer tipo de arquivo, incluindo imagens, vídeos, etc.
* **Processamento de dados de entrada:** Para ler dados de dispositivos de entrada, como teclados e sensores.
---
## Boas Práticas: Tratando IOException com try-with-resources
O `try-with-resources` é uma construção do Java que simplifica significativamente o tratamento de recursos que precisam ser fechados após o uso, como streams de arquivos. Ao utilizar essa estrutura, garantimos que o recurso seja fechado corretamente, mesmo que ocorram exceções durante o processamento.

**Por que usar try-with-resources?**
* **Prevenção de vazamentos de recursos:** Garante que recursos como arquivos sejam fechados, evitando problemas de desempenho e corrupção de dados.
* **Código mais limpo:** Elimina a necessidade de escrever blocos `finally` para fechar os recursos manualmente.
* **Melhora a legibilidade:** Torna o código mais conciso e fácil de entender.

**Exemplo:**
```java
import java.io.FileInputStream;
import java.io.IOException;

public class LerArquivoComTryWithResources {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("meu_arquivo.txt")) {
            // Código para ler o arquivo
            int byteLido;
            while ((byteLido = fis.read()) != -1) {
                System.out.print((char) byteLido);
            }
        } catch (IOException e) {
            System.out.println("Erro ao ler o arquivo: " + e.getMessage());
        }
    }
}
```

**Explicação:**
* **try-with-resources:** O `FileInputStream` é declarado dentro dos parênteses do `try`. Isso indica que ele é um recurso que será automaticamente fechado ao final do bloco `try`.
* **Tratamento de exceções:** O bloco `catch` captura qualquer `IOException` que possa ocorrer durante a leitura do arquivo.

**Vantagens do try-with-resources:**
* **Simplicidade:** A sintaxe é clara e concisa.
* **Segurança:** Garante o fechamento do recurso em todas as situações.
* **Leiturabilidade:** Melhora a legibilidade do código, pois o fechamento do recurso está próximo do local onde ele é criado.
* **Múltiplos recursos:** Você pode declarar múltiplos recursos separados por vírgula dentro dos parênteses do `try`.

**Outras considerações:**
* **AutoCloseable:** Para que um objeto possa ser usado com `try-with-resources`, sua classe deve implementar a interface `AutoCloseable`. A maioria das classes que representam recursos, como `FileInputStream`, `FileOutputStream`, `Connection`, já implementam essa interface.
* **Exceções:** O `try-with-resources` garante que o método `close()` seja chamado, mesmo que uma exceção seja lançada dentro do bloco `try`. No entanto, se uma exceção ocorrer durante o fechamento do recurso, ela será suprimida e a exceção original será propagada.
* **Nested try-with-resources:** Você pode aninhar múltiplos `try-with-resources` para gerenciar vários recursos.

**Exemplo com múltiplos recursos:**
```java
try (BufferedReader reader = new BufferedReader(new FileReader("meu_arquivo.txt"));
     BufferedWriter writer = new BufferedWriter(new FileWriter("novo_arquivo.txt"))) {
    // Ler e escrever dados entre os arquivos
} catch (IOException e) {
    // Tratar a exceção
}
```
---
## Escrevendo Arquivos com FileOutputStream
O `FileOutputStream` é uma classe fundamental para escrever dados em um arquivo. Ele permite que você grave dados em um arquivo byte a byte, oferecendo um alto nível de controle sobre a escrita.

### Como funciona o FileOutputStream?
* **Criação:** Você cria um objeto `FileOutputStream` passando o caminho do arquivo como parâmetro. Se o arquivo não existir, ele será criado. Se ele já existir, o conteúdo existente será sobrescrito.
* **Escrita:** Utiliza o método `write()` para escrever bytes no arquivo.
* **Fechamento:** Após a escrita, é essencial fechar o stream usando o método `close()`.

### Exemplo Básico:
```java
import java.io.FileOutputStream;
import java.io.IOException;

public class EscreverArquivo {
    public static void main(String[] args) {
        try (FileOutputStream fos = new FileOutputStream("meu_arquivo.txt")) {
            String texto = "Olá, mundo!";
            byte[] bytes = texto.getBytes();
            fos.write(bytes);
        } catch (IOException e) {
            System.out.println("Erro ao escrever no arquivo: " + e.getMessage());
        }
    }
}
```
**Explicação do código:**
1. **Criar o FileOutputStream:** Um objeto `FileOutputStream` é criado para o arquivo "meu_arquivo.txt".
2. **Converter para bytes:** A string a ser escrita é convertida em um array de bytes.
3. **Escrever os bytes:** O método `write()` escreve o array de bytes no arquivo.
4. **Tratamento de exceções:** Um bloco `try-with-resources` é utilizado para garantir que o `FileOutputStream` seja fechado automaticamente, mesmo que ocorra uma exceção.

### Escrevendo em um buffer:
Para melhorar o desempenho, é comum escrever dados em um buffer de bytes:
```java
byte[] buffer = new byte[1024];
// Preencher o buffer com os dados a serem escritos
fos.write(buffer, 0, bytesAEscrever);
```

### Aplicações:
* **Criação de arquivos de texto:** Para gerar arquivos de texto com conteúdo dinâmico.
* **Gravação de dados:** Para salvar dados gerados por uma aplicação, como logs, configurações, etc.
* **Geração de relatórios:** Para criar arquivos de relatório em formato texto ou outros formatos.

### Boas práticas:
* **Utilizar o try-with-resources:** Garante que o `FileOutputStream` seja fechado corretamente, mesmo em caso de exceções.
* **Flush:** Use o método `flush()` para garantir que todos os dados escritos sejam persistidos no disco.
* **Buffer:** Utilize buffers para melhorar o desempenho, especialmente para grandes volumes de dados.
* **Tratamento de exceções:** Implemente um tratamento de exceções adequado para lidar com erros durante a escrita.
---
## Character-oriented Streams

**O que são Streams Orientados a Caracteres?**
Enquanto os streams orientados a bytes operam em nível de byte, os streams orientados a caracteres trabalham com unidades de texto, ou seja, caracteres. Isso os torna mais adequados para lidar com dados textuais, como arquivos de texto, entrada do usuário e saída para a console.

**Por que usar streams orientados a caracteres?**
* **Abstração:** Escondem a complexidade da codificação de caracteres, permitindo que você trabalhe com texto de forma mais natural.
* **Facilidade de uso:** Oferecem métodos convenientes para ler e escrever linhas de texto.
* **Maior nível de abstração:** Permitem que você se concentre no conteúdo do texto, em vez dos detalhes de representação dos caracteres.

**Classes principais:**
* **Reader:** Classe abstrata que representa a fonte de dados de caracteres.
    * Subclasses comuns:
        * `FileReader`: Lê caracteres de um arquivo.
        * `BufferedReader`: Adiciona um buffer para melhorar o desempenho da leitura e permite ler linhas inteiras.
* **Writer:** Classe abstrata que representa o destino dos dados de caracteres.
    * Subclasses comuns:
        * `FileWriter`: Escreve caracteres em um arquivo.
        * `BufferedWriter`: Adiciona um buffer para melhorar o desempenho da escrita.

**Exemplo Prático: Copiando um Arquivo de Texto**
```java
import java.io.*;

public class CopiarArquivoTexto {
    public static void main(String[] args) throws IOException {
        try (BufferedReader reader = new BufferedReader(new FileReader("arquivo_original.txt"));
             BufferedWriter writer = new BufferedWriter(new FileWriter("novo_arquivo.txt"))) {
            String linha;
            while ((linha = reader.readLine()) != null) {
                writer.write(linha);
                writer.newLine();
            }
        } catch (IOException e) {
            System.out.println("Erro ao copiar o arquivo: " + e.getMessage());
        }
    }
}
```
**Explicação:**
* **Criar streams:** Criamos um `BufferedReader` para ler o arquivo original e um `BufferedWriter` para escrever no novo arquivo.
* **Ler linhas:** O método `readLine()` lê uma linha completa de texto.
* **Escrever linhas:** O método `write()` escreve a linha e o `newLine()` adiciona uma nova linha.

**Vantagens dos Streams Orientados a Caracteres**
* **Facilidade de uso:** Oferecem métodos convenientes para trabalhar com texto, como `readLine()`, `write()` e `newLine()`.
* **Abstração:** Escondem a complexidade da codificação de caracteres.
* **Alto nível:** Permitem que você se concentre no conteúdo do texto, em vez dos detalhes de representação.

**Quando usar Streams Orientados a Caracteres?**
* **Manipulação de texto:** Para ler e escrever arquivos de texto, processar strings, etc.
* **Interação com o usuário:** Para ler dados da entrada do usuário e escrever na saída.

**Relação com Streams Orientados a Bytes**
* **Construídos sobre bytes:** Os streams de caracteres são construídos sobre os streams de bytes.
* **Codificação de caracteres:** A conversão entre bytes e caracteres é feita com base em uma codificação específica (UTF-8, ISO-8859-1, etc.).
---
## Lendo Arquivos de Texto com FileReader
O `FileReader` é uma classe que nos permite ler dados de um arquivo de texto caractere por caractere. Ele é ideal para lidar com arquivos que armazenam dados textuais, como arquivos de configuração, logs e outros tipos de arquivos que contenham texto legível.

**Como funciona o FileReader?**
1. **Criação:** Você cria um objeto `FileReader` passando o caminho do arquivo como parâmetro.
2. **Leitura:** Utiliza o método `read()` para ler um caractere por vez ou o método `readLine()` para ler uma linha completa.
3. **Fechamento:** Após a leitura, é essencial fechar o stream usando o método `close()`.

**Exemplo Básico:**
```java
import java.io.FileReader;
import java.io.IOException;

public class LerArquivoTexto {
    public static void main(String[] args) {
        try (FileReader reader = new FileReader("meu_arquivo.txt")) {
            int caractere;
            while ((caractere = reader.read()) != -1) {
                System.out.print((char) caractere);
            }
        } catch (IOException e) {
            System.out.println("Erro ao ler o arquivo: " + e.getMessage());
        }
    }
}
```
**Explicação:**
* **Criar o FileReader:** Um objeto `FileReader` é criado para o arquivo "meu_arquivo.txt".
* **Ler caractere por caractere:** O método `read()` lê um caractere por vez. Se o valor retornado for -1, significa que o final do arquivo foi alcançado.
* **Converter para caractere:** O inteiro retornado pelo `read()` é convertido para um caractere e impresso na console.
* **Tratamento de exceções:** Um bloco `try-with-resources` é utilizado para garantir que o `FileReader` seja fechado automaticamente, mesmo que ocorra uma exceção.

**Lendo linha por linha:**
Para ler o arquivo linha por linha, é mais eficiente utilizar o método `readLine()`:
```java
String linha;
while ((linha = reader.readLine()) != null) {
    System.out.println(linha);
}
```

**Considerações importantes:**
* **Codificação de caracteres:** O `FileReader` assume uma codificação de caracteres padrão. Para especificar uma codificação diferente, utilize um `InputStreamReader` com a codificação desejada.
* **Exceções:** Sempre trate as possíveis exceções de I/O, como `FileNotFoundException` (arquivo não encontrado) e `IOException` (outros erros de E/S).
* **Fechamento do stream:** É fundamental fechar o `FileReader` após a leitura para liberar os recursos do sistema.
* **Performance:** Para grandes arquivos, ler em um buffer pode melhorar o desempenho. Para isso, utilize a classe `BufferedReader`.
* **Outras classes:** Existem outras classes como `BufferedReader` que oferecem funcionalidades adicionais, como buffering e marcação de posição.

**Aplicações:**
* **Leitura de arquivos de configuração:** Para carregar configurações de uma aplicação a partir de um arquivo de texto.
* **Processamento de logs:** Para analisar e processar informações de logs.
* **Análise de dados:** Para ler dados de arquivos de texto e realizar análises estatísticas.

**Exemplo com BufferedReader:**
```java
try (BufferedReader reader = new BufferedReader(new FileReader("meu_arquivo.txt"))) {
    String linha;
    while ((linha = reader.readLine()) != null) {
        // Processar cada linha
        System.out.println(linha);
    }
}
```
O `BufferedReader` oferece um buffer para melhorar o desempenho da leitura, além de permitir que você leia o arquivo linha por linha de forma mais eficiente.

---
## Escrevendo Arquivos de Texto com FileWriter
O `FileWriter` é uma classe em Java utilizada para escrever dados em um arquivo de texto. Ele cria um fluxo de saída de caracteres que pode ser direcionado para um arquivo específico. É uma ferramenta fundamental para a manipulação de arquivos em aplicações Java.

**Como usar FileWriter?**
1. **Importar a classe:**
   ```java
   import java.io.FileWriter;
   import java.io.IOException;
   ```

2. **Criar um objeto FileWriter:**
   ```java
   FileWriter writer = new FileWriter("meu_arquivo.txt");
   ```
   * **"meu_arquivo.txt"**: Nome do arquivo que será criado ou sobrescrito.

3. **Escrever no arquivo:**
   ```java
   writer.write("Olá, mundo!");
   writer.write(System.lineSeparator()); // Adiciona uma nova linha
   ```
   * **write(String s)**: Escreve uma string no arquivo.

4. **Fechar o arquivo:**
   ```java
   writer.close();
   ```
   É fundamental fechar o arquivo após a escrita para garantir que todas as modificações sejam salvas e liberar os recursos do sistema.

**Exemplo completo:**
```java
import java.io.FileWriter;
import java.io.IOException;

public class EscreverArquivo {
    public static void main(String[] args) {
        try {
            FileWriter writer = new FileWriter("meu_arquivo.txt");
            writer.write("Esta é a primeira linha.\n");
            writer.write("Esta é a segunda linha.");
            writer.close();
            System.out.println("Arquivo criado com sucesso!");
        } catch (IOException e) {
            System.err.println("Erro ao escrever no arquivo: " + e.getMessage());
        }
    }
}
```

**Considerações importantes:**
* **Sobrescrita de arquivos:** Ao criar um objeto `FileWriter` sem o parâmetro `append` (que veremos a seguir), o arquivo existente será sobrescrito.
* **Append:** Para adicionar conteúdo ao final de um arquivo existente, use o construtor com o parâmetro `append` como `true`:
   `{java}FileWriter writer = new FileWriter("meu_arquivo.txt", true);`
* **Exceções:** É sempre recomendado envolver a operação de escrita em um bloco `try-catch` para tratar possíveis exceções, como `IOException`.
* **Buffering:** Para melhorar o desempenho, especialmente ao escrever grandes quantidades de dados, considere utilizar um `BufferedWriter` em conjunto com o `FileWriter`:
   ```java
   BufferedWriter bw = new BufferedWriter(new FileWriter("meu_arquivo.txt"));
   bw.write("Conteúdo a ser escrito");
   bw.close();
   ```
* **Encoding:** O `FileWriter` utiliza o encoding padrão da plataforma. Para especificar um encoding diferente, use a classe `OutputStreamWriter`.

**Quando usar FileWriter?**
O `FileWriter` é ideal para:
* Criar novos arquivos de texto.
* Sobrescrever o conteúdo de arquivos existentes.
* Adicionar conteúdo ao final de arquivos existentes (usando `append`).
* Escrever dados simples em formato de texto.

**Limitações:**
* Não é recomendado para escrever grandes volumes de dados binários.
* Para operações mais complexas com arquivos, como leitura e escrita aleatória, considere utilizar classes como `RandomAccessFile`.
---
## Lendo Arquivos Texto de Forma Otimizada com BufferedReader
O `BufferedReader` é uma classe muito útil em Java quando se trata de ler arquivos de texto de forma eficiente. Ele oferece um buffer para armazenar temporariamente os dados lidos do arquivo, o que reduz o número de operações de entrada/saída e, consequentemente, melhora o desempenho.

**Por que usar BufferedReader?**
* **Desempenho:** Ao utilizar um buffer, o `BufferedReader` reduz significativamente o número de operações de leitura do disco, o que pode levar a um ganho considerável de performance, especialmente ao lidar com arquivos grandes.
* **Facilidade de uso:** Ele fornece métodos como `readLine()` que permitem ler o arquivo linha por linha de forma simples e intuitiva.

**Como usar BufferedReader?**
1. **Importar as classes:**
   ```java
   import java.io.BufferedReader;
   import java.io.FileReader;
   import java.io.IOException;
   ```

2. **Criar um FileReader:**
   `{java}FileReader fr = new FileReader("meu_arquivo.txt");`
   O `FileReader` cria um fluxo de entrada de caracteres a partir do arquivo especificado.

3. **Criar um BufferedReader:**
   ```java
   BufferedReader br = new BufferedReader(fr);
   ```
   O `BufferedReader` encapsula o `FileReader`, fornecendo um buffer para a leitura.

4. **Ler o arquivo:**
   ```java
   String linha;
   while ((linha = br.readLine()) != null) {
       // Processar a linha lida
       System.out.println(linha);
   }
   ```
   O método `readLine()` lê uma linha do arquivo por vez. O loop `while` continua até que o final do arquivo seja alcançado.

5. **Fechar os fluxos:**
   ```java
   br.close();
   fr.close();
   ```
   É fundamental fechar os fluxos para liberar os recursos do sistema.

**Exemplo:**
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class LerArquivo {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("meu_arquivo.txt"))) {
            String linha;
            while ((linha = br.readLine()) != null) {
                System.out.println(linha);
            }
        } catch (IOException e) {
            System.err.println("Erro ao ler o arquivo: " + e.getMessage());
        }
    }
}
```

**Otimizações adicionais:**
* **Utilizar try-with-resources:** O exemplo acima utiliza o try-with-resources, que garante que os recursos (BufferedReader e FileReader) sejam fechados automaticamente, mesmo que ocorra uma exceção.
* **Considerar o tamanho do buffer:** O tamanho padrão do buffer pode ser ajustado através do construtor do BufferedReader para otimizar o desempenho em diferentes cenários.
* **Processar o arquivo em paralelo:** Para arquivos muito grandes, pode ser interessante utilizar threads ou frameworks de processamento paralelo para acelerar a leitura e o processamento.

**Quando usar BufferedReader?**
* **Leitura de arquivos texto:** É ideal para ler arquivos texto linha por linha.
* **Processamento eficiente:** Oferece um bom desempenho, especialmente para arquivos grandes.
* **Facilidade de uso:** A API do BufferedReader é simples e intuitiva.
---
## Escrevendo Arquivos Texto de Forma Otimizada com BufferedWriter
O `BufferedWriter` é uma classe que, assim como o `BufferedReader`, utiliza um buffer para otimizar a escrita em arquivos de texto. Ele agrupa várias chamadas de escrita em uma única operação de escrita no disco, melhorando significativamente o desempenho, especialmente quando se escrevem grandes quantidades de dados.

**Por que usar BufferedWriter?**
* **Desempenho:** Ao utilizar um buffer, o `BufferedWriter` reduz o número de operações de escrita no disco, o que pode levar a um ganho considerável de performance.
* **Facilidade de uso:** Ele fornece métodos como `write()` e `newLine()` que permitem escrever dados no arquivo de forma simples e intuitiva.

**Como usar BufferedWriter?**
1. **Importar as classes:**
   ```java
   import java.io.BufferedWriter;
   import java.io.FileWriter;
   import java.io.IOException;
   ```

2. **Criar um FileWriter:**
   `{java}FileWriter fw = new FileWriter("meu_arquivo.txt");`
   O `FileWriter` cria um fluxo de saída de caracteres para o arquivo especificado.

3. **Criar um BufferedWriter:**
   `{java}BufferedWriter bw = new BufferedWriter(fw);`
   O `BufferedWriter` encapsula o `FileWriter`, fornecendo um buffer para a escrita.

4. **Escrever no arquivo:**
   ```java
   bw.write("Esta é a primeira linha.");
   bw.newLine();
   bw.write("Esta é a segunda linha.");
   ```
   O método `write()` escreve uma sequência de caracteres no buffer, e o método `newLine()` adiciona uma nova linha.

5. **Fechar os fluxos:**
   ```java
   bw.close();
   fw.close();
   ```
   É fundamental fechar os fluxos para garantir que todos os dados sejam escritos no disco e para liberar os recursos do sistema.

**Exemplo completo:**
```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class EscreverArquivo {
    public static void main(String[] args) {
        try (BufferedWriter bw = new BufferedWriter(new FileWriter("meu_arquivo.txt"))) {
            bw.write("Olá, mundo!");
            bw.newLine();
            bw.write("Esta é uma demonstração do BufferedWriter.");
        } catch (IOException e) {
            System.err.println("Erro ao escrever no arquivo: " + e.getMessage());
        }
    }
}
```
---
## Reconhecendo a API de I/O em System.in e Scanner
A entrada e saída de dados (I/O) são fundamentais para a interação entre programas e usuários. A API de I/O do Java oferece diversas classes e interfaces para realizar essas operações, sendo `System.in` e `Scanner` duas das mais utilizadas para obter dados do usuário.

### System.in
* **O que é:** É um fluxo de entrada padrão que, por padrão, está conectado ao teclado. Ele permite ler dados brutos (bytes) a partir da entrada.
* **Como usar:**
  * `System.in.read()`: Lê um único byte da entrada e retorna seu valor como um inteiro.
  * **Exemplo:**
    ```java
    int caractere = System.in.read();
    System.out.println("Você digitou: " + (char)caractere);
    ```
* **Limitações:**
  * Lê dados em nível de byte, o que pode ser menos conveniente para ler dados formatados como strings ou números.
  * Requer um tratamento mais cuidadoso para lidar com diferentes tipos de dados.

### Scanner
* **O que é:** É uma classe mais conveniente para ler dados formatados a partir de várias fontes, incluindo `System.in`. Ele oferece métodos para ler diferentes tipos de dados, como inteiros, números de ponto flutuante e strings.
* **Como usar:**
  * **Criando um Scanner:**
    `{java}Scanner scanner = new Scanner(System.in);`
  * **Lendo dados:**
    * `nextInt()`: Lê um inteiro.
    * `nextDouble()`: Lê um número de ponto flutuante.
    * `nextLine()`: Lê uma linha de texto.
    * **Exemplo:**
      ```java
      System.out.print("Digite seu nome: ");
      String nome = scanner.nextLine();
      System.out.print("Digite sua idade: ");
      int idade = scanner.nextInt();
      System.out.println("Olá, " + nome + "! Você tem " + idade + " anos.");
      ```
* **Vantagens:**
  * Facilidade de uso: Oferece métodos intuitivos para ler diferentes tipos de dados.
  * Flexibilidade: Permite personalizar o delimitador de tokens e ignorar linhas em branco.

### Comparação entre System.in e Scanner

| Característica | System.in | Scanner |
|---|---|---|
| Nível | Baixo nível (bytes) | Alto nível (tipos de dados) |
| Facilidade de uso | Menos intuitivo | Mais intuitivo |
| Flexibilidade | Menos flexível | Mais flexível |
| Desempenho | Potencialmente mais rápido para grandes volumes de dados | Geralmente mais lento para grandes volumes de dados |
### Quando usar cada um?
* **System.in:**
  * Quando você precisa de um controle mais preciso sobre a leitura de dados em nível de byte.
  * Quando o desempenho é crítico e você está lidando com grandes volumes de dados brutos.
* **Scanner:**
  * Para a maioria das aplicações, onde você precisa ler dados formatados de forma conveniente.
  * Quando a legibilidade do código é importante.

### Considerações adicionais
* **Fechamento do Scanner:** Após o uso, é recomendado fechar o Scanner para liberar recursos:
  `{java}scanner.close();`
* **Exceções:** Tanto `System.in.read()` quanto os métodos do Scanner podem lançar exceções, como `IOException`, caso ocorra algum erro durante a leitura. É importante tratar essas exceções adequadamente.
---
## Reconhecendo a API de I/O em System.out e a classe PrintStream
### System.out: A porta de saída padrão
* **O que é:** System.out é um objeto pré-definido em Java que representa a **saída padrão**. Por padrão, a saída padrão é a sua tela, o console.
* **Para que serve:** É utilizado para imprimir dados na tela.
* **Como funciona:** System.out é uma instância da classe **PrintStream**. Essa classe oferece diversos métodos para formatar e enviar dados para a saída.

### PrintStream: A classe por trás da magia
* **O que é:** PrintStream é uma classe que oferece métodos para imprimir vários tipos de dados em um fluxo de saída.
* **Métodos principais:**
    * **print(String s):** Imprime a string sem adicionar uma nova linha no final.
    * **println(String s):** Imprime a string e adiciona uma nova linha no final.
    * **printf(String format, Object... args):** Imprime uma string formatada, similar à função printf em C.
* **Outras funcionalidades:**
    * **flush():** Força a escrita dos dados no fluxo de saída.
    * **close():** Fecha o fluxo de saída.

### Exemplos práticos
```java
// Imprimir uma mensagem simples
System.out.println("Olá, mundo!");

// Imprimir um número e uma string
int idade = 30;
String nome = "João";
System.out.println("Meu nome é " + nome + " e tenho " + idade + " anos.");

// Imprimir com formatação
double pi = 3.14159;
System.out.printf("O valor de pi é: %.2f\n", pi);
```

### Por que usar System.out e PrintStream?
* **Simplicidade:** É a forma mais fácil de mostrar informações na tela.
* **Flexibilidade:** Permite imprimir diversos tipos de dados e formatá-los.
* **Integração:** Faz parte da API padrão do Java, não necessitando de importações adicionais.

### Quando usar outras opções?
* **Gravar em arquivos:** Utilize classes como FileWriter ou BufferedWriter.
* **Formatar dados complexos:** Explore a classe Formatter.
* **Interagir com a rede:** Utilize classes como Socket e PrintWriter.
---
