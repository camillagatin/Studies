https://github.com/camillagatin/collections-java-api-2023
## Introdução aos Mapas
É uma interface que representa uma coleção de pares **chave-valor**. Cada chave é única e está associada a um valor específico. Essa estrutura de dados é extremamente útil quando você precisa armazenar e recuperar informações com base em um índice específico, ou seja, a chave.

#### Características principais:
- **Chaves únicas:** Cada chave dentro de um Map deve ser única. Se você tentar adicionar uma chave duplicada, o valor associado à chave anterior será sobrescrito.
- **Pares chave-valor:** Cada elemento em um Map consiste em um par chave-valor.
- **Não ordenados:** A ordem dos elementos em um Map não é garantida, a menos que você use uma implementação específica como o `LinkedHashMap`.

#### Para que servem os Mapas?
- **Armazenamento de dados associativos:** Quando você precisa armazenar dados relacionados, como nomes e idades, ou produtos e preços, um Map é a estrutura ideal.
- **Criação de caches:** Mapas são frequentemente usados para implementar caches, onde os dados são armazenados temporariamente para melhorar o desempenho.
- **Configurações:** Armazenar configurações de uma aplicação em um Map permite um acesso rápido e fácil aos valores.

### Implementações comuns de Map:
- **HashMap:** A implementação mais comum, oferece acesso rápido aos elementos, mas não garante a ordem dos elementos.
- **TreeMap:** Mantém os elementos ordenados de acordo com a chave natural ou um Comparator fornecido.
- **LinkedHashMap:** Mantém a ordem de inserção dos elementos.
- **HashTable:** Uma versão antiga e sincronizada do HashMap, geralmente evitada em favor de ConcurrentHashMap para concorrência.
- **ConcurrentHashMap:** Uma versão thread-safe do HashMap, ideal para ambientes multithread.

### Exemplo básico:
```java
import java.util.HashMap;
import java.util.Map;

public class MapExemplo {
    public static void main(String[] args) {
        Map<String, Integer>    idades = new HashMap<>();
        idades.put("João", 30);
        idades.put("Maria", 25);
        idades.put("Pedro", 35);

        // Acessando um valor
        int idadeDeMaria = idades.get("Maria");
        System.out.println("A idade de Maria é: " + idadeDeMaria);
    }
}
```
Neste exemplo, criamos um Map para armazenar nomes e idades. A chave é o nome e o valor é a idade.

#### Quando usar Map?
- **Quando você precisa de uma associação entre chaves e valores:** Se você precisa armazenar dados relacionados, um Map é a escolha ideal.
- **Quando você precisa acessar elementos por uma chave:** Mapas são eficientes para buscar elementos por sua chave.
- **Quando a ordem dos elementos não é importante:** Se a ordem dos elementos não é relevante para sua aplicação, um HashMap é uma boa escolha.
---
## HashMap e HashTable
**HashMap** e **HashTable** são duas implementações da interface `Map` em Java, utilizadas para armazenar pares chave-valor. Embora compartilhem algumas características, existem diferenças cruciais entre elas, principalmente no que diz respeito à **concorrência** e **flexibilidade**.

### HashMap
- **Não sincronizado:** O HashMap não é thread-safe, ou seja, não é seguro para uso em ambientes multithread sem sincronização adicional. Isso significa que se múltiplas threads acessarem um HashMap simultaneamente, podem ocorrer problemas de concorrência.
- **Permite chaves nulas:** Um HashMap pode conter uma única chave nula e múltiplos valores nulos.
- **Mais rápido:** Geralmente mais rápido que o HashTable devido à ausência de sincronização.
- **Ideal para:** Aplicações onde a concorrência não é um fator crítico e a performance é priorizada.

### HashTable
- **Sincronizado:** O HashTable é thread-safe, o que significa que é seguro para uso em ambientes multithread. Todas as operações no HashTable são sincronizadas, garantindo a consistência dos dados.
- **Não permite chaves nulas:** Um HashTable não permite chaves nulas.
- **Mais lento:** Geralmente mais lento que o HashMap devido à sobrecarga da sincronização.
- **Ideal para:** Aplicações onde a segurança de threads é uma prioridade e a performance não é o fator mais crítico.

### Quando usar cada um?
- **HashMap:**
    - Aplicações de um único thread ou com pouca concorrência.
    - Quando a performance é crucial e a segurança de threads não é uma preocupação.
    - Em coleções que não precisam ser sincronizadas externamente.
- **HashTable:**
    - Aplicações multithread onde a segurança de threads é essencial.
    - Quando você precisa de uma coleção sincronizada por padrão.
    - Em ambientes legados onde o HashTable era a única opção.

#### Exemplo:
```java
import java.util.HashMap;
import java.util.Hashtable;

public class MapExemplo {
    public static void main(String[] args) {
        // HashMap
        Map<String, Integer> hashMap = new HashMap<>();
        hashMap.put("João", 30);
        hashMap.put("Maria", 25);

        // HashTable
        Hashtable<String, Integer> hashTable = new Hashtable<>();
        hashTable.put("Pedro", 35);
        hashTable.put("Ana", 28);
    }
}
```

### Considerações adicionais
- **ConcurrentHashMap:** Para aplicações multithread modernas, o `ConcurrentHashMap` é geralmente preferível ao `HashTable`, pois oferece um desempenho melhor e mais flexibilidade.
- **Sincronização explícita:** Se você precisar sincronizar um HashMap em um ambiente multithread, pode usar blocos `synchronized` ou classes como `Collections.synchronizedMap()`.
- **Escolha a implementação correta:** A escolha entre HashMap e HashTable depende das suas necessidades específicas. Considere os requisitos de concorrência, performance e as características das suas aplicações.
---
## LinkedHashMap e TreeMap: outras implementações de mapas

### LinkedHashMap
**LinkedHashMap** preserva a ordem de inserção dos elementos. Isso significa que ao iterar sobre um LinkedHashMap, os elementos serão retornados na mesma ordem em que foram adicionados.

**Características:**
* **Ordem de inserção:** Mantém a ordem em que os elementos foram adicionados.
* **Acesso rápido:** Ainda oferece bom desempenho para operações de busca e inserção, similar ao HashMap.
* **Baseado em hash:** Utiliza uma tabela hash internamente, como o HashMap.
* **Lista duplamente encadeada:** Além da tabela hash, mantém uma lista duplamente encadeada para rastrear a ordem de inserção.

**Quando usar:**
* **Cache:** Implementar caches LRU (Least Recently Used), onde os elementos menos recentemente usados são removidos primeiro.
* **Histórico de ações:** Manter um histórico de ações na ordem em que ocorreram.
* **Quando a ordem de inserção é importante:** Sempre que a ordem em que os elementos foram adicionados precisa ser preservada.

### TreeMap
**TreeMap** armazena os elementos em ordem natural ou de acordo com um Comparator fornecido. Isso significa que as chaves são ordenadas de forma ascendente (ou descendente, se um Comparator for especificado).

**Características:**
* **Ordenado:** Mantém os elementos ordenados de acordo com a chave natural ou um Comparator.
* **Baseado em árvore:** Utiliza uma árvore rubro-negra internamente para manter a ordem.
* **Operações de intervalo:** Permite realizar operações eficientes em intervalos de chaves, como encontrar o primeiro ou último elemento dentro de um intervalo.
* **Não permite chaves nulas:** Assim como o HashTable, não permite chaves nulas.

**Quando usar:**
* **Quando a ordem é importante:** Se você precisa iterar sobre os elementos em ordem crescente ou decrescente.
* **Operações de intervalo:** Quando você precisa realizar operações em intervalos de chaves, como encontrar o menor ou maior elemento.
* **Implementações de estruturas de dados:** Servir como base para implementar outras estruturas de dados, como árvores balanceadas.

### Comparação entre HashMap, LinkedHashMap e TreeMap

| Característica | HashMap | LinkedHashMap | TreeMap |
|---|---|---|---|
| Ordem | Não ordenada | Ordem de inserção | Ordenado por chave |
| Acesso | Rápido | Rápido | Pode ser mais lento para inserção, mas eficiente para buscas ordenadas |
| Implementação interna | Tabela hash | Tabela hash + lista duplamente encadeada | Árvore rubro-negra |
| Chaves nulas | Permite | Permite | Não permite |
**Em resumo:**
* **HashMap:** Desempenho rápido, não ordenado. Se a performance e a flexibilidade são prioridades.
* **LinkedHashMap:** Ordem de inserção, bom desempenho. Se a ordem de inserção é importante.
* **TreeMap:** Ordenado por chave, operações de intervalo eficientes. Se a ordem natural das chaves é relevante.
---