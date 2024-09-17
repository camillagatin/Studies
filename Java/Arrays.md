## Iterando em arrays
```java
public class Calculadora {

    static double calcularMedia(int[] numeros) {
        int total = 0;

        // for aprimorado (enhanced for)
        for (int numero : numeros) {
            total += numero;
        }

        // for tradicional
//        for (int i = 0; i < numeros.length; i++) {
//            total += numeros[i];
//        }

        return (double) total / numeros.length;
    }

}
```

```java
public class Principal {

    public static void main(String[] args) {
        int[] notas = {8, 5, 4, 9, 10};

        double media = Calculadora.calcularMedia(notas);

        System.out.println(media);
    }

}
```

---
## Transformando arrays em representações em string
```java
import java.util.Arrays;

public class Principal {

    public static void main(String[] args) {
        int[] notas = {8, 5, 4, 9, 10};

        String notasEmString = Arrays.toString(notas);

        System.out.println(notasEmString);
    }

}
```

---
## Ordenando arrays em ordem natural e reversa
```java
import java.util.Arrays;
import java.util.Comparator;

public class Principal {

    public static void main(String[] args) {
        // int[] notas = {8, 5, 4, 10, 9};
        Integer[] notas = {8, 5, 4, 10, 9};

        // Ordem natural
        // Arrays.sort(notas);

        // Ordem decrescente
        Arrays.sort(notas, Comparator.reverseOrder()); //não funciona com tipos primitivos

        System.out.println(Arrays.toString(notas));
    }

}
```

---
## Criando arrays de objetos
```java
public class Aluno {

    String nome;
    int idade;

}
```

```java
public class Turma {

    String identificacao;
    String nomeProfessora;
    Aluno[] alunos;

}
```

```java
public class Principal {

    public static void main(String[] args) {
        Turma turmaB = new Turma();
        turmaB.identificacao = "Maternal B";
        turmaB.nomeProfessora = "Tia Maria";
        turmaB.alunos = new Aluno[3];

        turmaB.alunos[0] = new Aluno();
        turmaB.alunos[0].nome = "João";
        turmaB.alunos[0].idade = 3;

        Aluno aluno1 = new Aluno();
        aluno1.nome = "Laura";
        aluno1.idade = 4;

        turmaB.alunos[1] = aluno1;
    }

}
```

---
## Iterando em arrays objetos
Turma.java
```java
void imprimirListaAlunos() {
	for (Aluno aluno : alunos) {
		if (aluno != null) {
			souf("%s (%d anos)%n", alunos.nome, alunos.idade);
		} else {
			sout("vago");
		}
	}
}

/*
for (int i = 0; i < turmaB.alunos.length; i++) {
	Aluno aluno = turmaB.alunos[i];

	if (aluno != null) {
	souf("%d - %s (%d anos)%n", i, aluno.nome, aluno.idade);
	} else {
		souf("%d - vago%n", i);
	}
}
*/
```

---
## Copiando e expandindo arrays
```java
import java.util.Arrays;

public class Principal1 {

    public static void main(String[] args) {
        int[] numerosJogo1 = {25, 11, 8, 46, 37, 14};

		int[]numerosJogo2 = Arrays.copyOf(numerosJogo1, /*newLength:*/ numerosJogo1.length /*ou um número*/) // copiando

        int[] numerosJogo3 = Arrays.copyOf(numerosJogo1, numerosJogo1.length + 1); // expandindo
        
        numerosJogo3[numerosJogo3.length - 1] = 44; // atribuindo um número para o novo indice

        System.out.println(Arrays.toString(numerosJogo1));
        System.out.println(Arrays.toString(numerosJogo2));
        System.out.println(Arrays.toString(numerosJogo3));
    }

}
```

outro exemplo:

Aluno.java

```java
import java.util.Arrays;

public class Turma {

    String identificacao;
    String nomeProfessora;
    Aluno[] alunos = new Aluno[0];

    void adicionarAluno(Aluno aluno) {
        alunos = Arrays.copyOf(alunos, alunos.length + 1);
        alunos[alunos.length - 1] = aluno;
    }

    void imprimirListaDeAlunos() {
        for (Aluno aluno : alunos) {
            if (aluno != null) {
                System.out.printf("%s (%d anos)%n", aluno.nome, aluno.idade);
            } else {
                System.out.println("vago");
            }
        }
    }

}
```

```java
public class Principal {

    public static void main(String[] args) {
        Turma turmaB = new Turma();
        turmaB.identificacao = "Maternal B";
        turmaB.nomeProfessora = "Tia Maria";

        Aluno aluno1 = new Aluno();
        aluno1.nome = "João";
        aluno1.idade = 3;

        Aluno aluno2 = new Aluno();
        aluno2.nome = "Laura";
        aluno2.idade = 4;

        turmaB.adicionarAluno(aluno1);
        turmaB.adicionarAluno(aluno2);

        turmaB.imprimirListaDeAlunos();
    }

}
```

---
## Removendo elementos de array
```java
import java.util.Arrays;

public class Principal {

    public static void main(String[] args) {
        int[] numerosJogoAtual = {25, 11, 8, 46, 37, 14, 55};
        int[] numerosNovoJogo = new int[numerosJogoAtual.length - 1];

        int indiceExclusao = 2;

        System.arraycopy(numerosJogoAtual, 0,
                numerosNovoJogo, 0, indiceExclusao);

        System.arraycopy(numerosJogoAtual, indiceExclusao + 1, numerosNovoJogo, indiceExclusao, numerosNovoJogo.length - indiceExclusao);

        System.out.println(Arrays.toString(numerosJogoAtual));
        System.out.println(Arrays.toString(numerosNovoJogo));
    }

}
```

---
## [[Collections API#ArrayList|ArrayList da Collections API]]

Aluno.java

```java
import java.util.ArrayList;

public class Turma {

    String identificacao;
    String nomeProfessora;
    ArrayList<Aluno> alunos = new ArrayList<>();

    void adicionarAluno(Aluno aluno) {
        alunos.add(aluno);
    }

    void removerAluno(int indice) {
        alunos.remove(indice);
    }

    void imprimirListaDeAlunos() {
        for (Aluno aluno : alunos) {
            System.out.printf("%s (%d anos)%n", aluno.nome, aluno.idade);
        }
    }

}
```

```java
import java.util.ArrayList;

public class Principal {

    public static void main(String[] args) {
        ArrayList<String> alunos = new ArrayList<>();
        alunos.add("João");
        alunos.add("Maria");

//        for (int i = 0; i < alunos.size(); i++) {
//            String aluno = alunos.get(i);
//            System.out.println(aluno);
//        }

        for (String aluno : alunos) {
            System.out.println(aluno);
        }
    }

}
```

```java
public class Principal2 {

    public static void main(String[] args) {
        Turma turmaB = new Turma();
        turmaB.identificacao = "Maternal B";
        turmaB.nomeProfessora = "Tia Maria";

        Aluno aluno1 = new Aluno();
        aluno1.nome = "João";
        aluno1.idade = 3;

        Aluno aluno2 = new Aluno();
        aluno2.nome = "Laura";
        aluno2.idade = 4;

        Aluno aluno3 = new Aluno();
        aluno3.nome = "Miguel";
        aluno3.idade = 3;

        turmaB.adicionarAluno(aluno1);
        turmaB.adicionarAluno(aluno2);
        turmaB.adicionarAluno(aluno3);

        turmaB.removerAluno(1);

        turmaB.imprimirListaDeAlunos();
    }

}
```

---
## Retorne arrays ou coleções vazias no lugar de null
```java
import java.util.ArrayList;

public class Cardapio {

    ArrayList<ItemCardapio> consultarItensPorPreco(double precoMinimo, double precoMaximo) {
        ArrayList<ItemCardapio> itensEncontrados = new ArrayList<>();

        for (ItemCardapio item : itens) {
            if (item.possuiPrecoEntre(precoMinimo, precoMaximo)) {
                itensEncontrados.add(item);
            }
        }

        // boa prática
        return itensEncontrados;

        // má prática
        // return itensEncontrados.isEmpty() ? null : itensEncontrados;
    }

}
```

---
## Criando arrays multidimensionais

|         | coluna 0   |    coluna 1    | coluna 2       |
| ------- | ---------- | :------------: | -------------- |
| linha 0 | Uberlândia |    Uberaba     | Belo Horizonte |
| linha 1 | São Paulo  | Ribeirão Preto | null           |
| linha 2 | Fortaleza  |      null      | null           |

```java
public class Principal1 {

    public static void main(String[] args) {
        String[][] cidades = new String[3][3];
        cidades[0][0] = "Uberlândia";
        cidades[0][1] = "Uberaba";
        cidades[0][2] = "Belo Horizonte";

        cidades[1][0] = "São Paulo";
        cidades[1][1] = "Ribeirão Preto";

        cidades[2][0] = "Fortaleza";
    }

}
```


```java
public class Principal2 {

    public static void main(String[] args) {
        String[][][] cidades = new String[2][2][2];
        cidades[0][0][0] = "Uberlândia";
        cidades[0][0][1] = "Uberaba";
    }

}
```


```java
public class Principal3 {

    public static void main(String[] args) {
        String[][] cidades = new String[3][];
        cidades[0] = new String[3];
        cidades[0][0] = "Uberlândia";
        cidades[0][1] = "Uberaba";
        cidades[0][2] = "Belo Horizonte";

        cidades[1] = new String[2];
        cidades[1][0] = "São Paulo";
        cidades[1][1] = "Ribeirão Preto";

        cidades[2] = new String[1];
        cidades[2][0] = "Fortaleza";
    }

}
```

---
## Iterando em arrays multidimensionais
Principal3.java
```java
String[][] cidades = new String[3][];
cidadesPorEstado[0] = new String[3];
cidadesPorEstado[0][0] = "Uberlândia";
cidadesPorEstado[0][1] = "Uberaba";
cidadesPorEstado[0][2] = "Belo Horizonte";

cidadesPorEstado[1] = new String[2];
cidadesPorEstado[1][0] = "São Paulo";
cidadesPorEstado[1][1] = "Ribeirão Preto";

cidadesPorEstado[2] = new String[1];
cidadesPorEstado[2][0] = "Fortaleza";

// má prática quando não precisa do índice
for (int i = 0; i< cidades.length; i++) {
	for (int j = 0; j < cidades[i].length; j++) {
		souf("[%d][%d] = %s%n", i, j, cidades[i][j]);
	}
}

// boa prática quando não precisa do índice
for (Strings[] cidadesPorEstado : todasCidades) {
	for (String cidade : cidadesPorEstado) {
		sout(cidade)
	}
}

```

---
## [[Unified Modeling Language#Multiplicidade para arrays|Diagrama de Classes: Multiplicidade para arrays]]
![[multiplicidade para arrays.png]]