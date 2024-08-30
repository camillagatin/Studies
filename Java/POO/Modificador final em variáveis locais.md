CadastroPortaria.java
```java
static final int TEMPO_EXPIRACAO_PADRAO_EM_MESES = 1;

void cadastrar(final Visitante visitante) {
	this.cadastrar(visitante, TEMPO_EXPIRACAO_PADRAO_EM_MESES);
}

void cadastrar(final Visitante visitante, final int tempoExpiracaoEmMeses) {
	final int tempoExpiracaoEmDias = tempoExpiracaoEmMeses * 30;

    System.out.printf("Visitante %s cadastrado para %d dias%n", visitante.nome, tempoExpiracaoEmDias);
}
```

Principal.java
```java
public static void main(String[] args) {
    Visitante novoVisitante = new Visitante();
    novoVisitante.nome = "João";
    novoVisitante.idade = 15;

    CadastroPortaria cadastroPortaria = new CadastroPortaria();
//  cadastroPortaria.cadastrar(novoVisitante);
    cadastroPortaria.cadastrar(novoVisitante, 2);
}
```

Visitante.java
```java
static final int IDADE_MINIMA_ACESSO_IRRESTRITO = 16;

String nome;
int idade;

boolean possuiAcessoRestritoPorIdade() {
	return idade < IDADE_MINIMA_ACESSO_IRRESTRITO;
}
```
