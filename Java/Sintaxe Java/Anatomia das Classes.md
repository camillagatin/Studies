==nome das classes ►== MinhaClasse

==nome de variável ►== minhaVariavel

==variável sem troca de valores ►== final (sem ou com) String BR (variável toda maiúscula) = "Brasil"

==Estrutura método ►==

```java
int somar (int numeroUm, int numeroDois)
public static String fullName (String firstName, String lastName) {
	return firstName.concat(" ").concat(lastName)
;}
```
#### nomes variáveis ►
salarioMedio; email
#### nomes métodos ►
somar(); abrirConexao(); findById()

---
## Tipos e Variáveis
#### int ►
números inteiros; menor valor: -2³¹, maior valor: 2³¹ -1
#### byte ►
números inteiros ↔ 1 byte ↔ 8 bits; menor valor: -2⁷, maior valor: 2⁷ -1
#### short ►
números inteiros ↔ 2 bytes ↔ 16 bits; menor valor: -2¹⁵, maior valor: 2¹⁵ -1
#### long ►
números inteiros ↔ 8 bytes ↔ 64 bits ↔ pouco usado `long cpf = 987654321L;`; menor valor: -2⁶³, maior valor: 2⁶³ -1
#### float ►
números fracionados (reais) ↔ 4 bytes ↔ 32 bits ↔ pouco usado `float pi = 3.14F;`
#### double ►
números fracionados (reais) ↔ 8 bytes ↔ 64 bits
#### boolean ►
true, false ↔ lógico
#### char ►
caracter simples (String - classe) ↔ 2 bytes ↔ 16 bits aspas simples; menor valor: 0, maior valor: 2¹⁶ -1

### Conversão de tipos primitivos

==long para int==
```java
long x = 10;
// int y = x; // não compila
int y = (int) x; // compila (casting)

long a = 9300000035L;
int b = (int) a;
// imprime valores diferentes
sout(a); // 9300000035
sout(b); // 710065443
```

==int para long==
```java
int y = 102344;
long x = y; // não precisa de casting por ser do menor para o maior
```

==double para float==
```java
double peso1 = 20.5;
float peso2 = peso1; // não compila, precisa do casting

float peso2 = (float) peso1; // compila

```

==float para double==
```java
float taxa1 = 934.5f;
double taxa2 = taxa1; // não precisa de casting por ser do menor para o maior
```

==double para int==
```java
double largura = 100.37;
int tamanho = largura; // não compila sem o casting
int tamanho = (int) largura; // 100; perde precisão por virar número inteiro
```

### Estrutura Variável ►
`<Tipo> <nomeVariavel> <atribuiçãoDeValor>;`
`int x = 9;`

---
## Operadores
#### Concatenação ►
junção de uma String com outra
```java
1 + 1 + 1 + "1" = 31;
1 + "1" + 1 + 1 = 1111;
1 + "1" + 1 + "1" = 1111;
"1" + (1 + 1 + 1 ) = 13;
```
#### Unários ►
*  +  valor positivo
*  -  valor negativo
*  ++  incremento de valor
*  --  decremento de valor
*  !  lógico negação
Para tornar um valor positivo, deve-se fazer uma multiplicação `* - 1`
#### Ternários ►
funciona como um if/else
`<expressão condicional/if> ? <caso true> : <senão/caso false>`

---
## Métodos
Para métodos, os critérios são:
- Deve ser nomeado como verbo;
- Seguir o padrão camelCase (Todas as letras minúsculas com a exceção da primeira letra da segunda palavra).
Exemplos sugeridos para nomenclatura de métodos:
```java
somar(int n1, int n2){}

abrirConexao(){}

concluirProcessamento() {}

findById(int id){}

calcularImprimir(){} // há algo de errado neste método, ele deveria ter uma única finalidade

```
Abaixo, temos um exemplo de uma classe com dois métodos e suas respectivas considerações:
```java
public class MyClass {
	
	public double somar(int num1, int num2){
		//LOGICA - FINALIDADE DO MÉTODO
		return ... ;
	}
	
	public void imprimir(String texto){
		/*LOGICA - FINALIDADE DO MÉTODO
		AQUI NÃO PRECISA DO RETURN, POIS NÃO SERÁ RETORNADO NENHUM RESULTADO*/
	}
	
	// throws Exception : indica que o método ao ser utilizado poderá gerar uma exceção
	public double dividir(int dividendo, int divisor) throws Exception{}
	
	// este método não pode ser visto por outras classes no projeto
	private void metodoPrivado(){}
	
	//alguns equívocos estruturais
	public void validar(){
		//este método deveria retornar algum valor, no caso boolean (true ou false)
	}
	public void calcularEnviar(){
		//um método deve representar uma única responsabilidade
	}
	public void gravarCliente(String nome, String cpf, Integer telefone, ....){
		//este método tem a finalidade de gravar informações de um cliente, por que não criar um objeto cliente e passar como parâmetro ? veja abaixo
	}
	public void gravarCliente(Cliente cliente){}
	//ou
	public void gravar(Cliente cliente){}
}
```

---
## Escopos
O escopo pode ser entendido como,o ambiente onde uma variável pode ser acessada. Em Java, o escopo de variáveis **vai de acordo com o bloco onde ela foi declarada**.
Sem um domínio sobre escopo de códigos, seu projeto tende a conter falhas estruturais e comprometer a proposta principal da aplicação.
```java
public class Conta {
	//variavel da classe conta
	double saldo=10.0;
	
	public void sacar(Double valor) {
		//variavel local de método
		double novoSaldo = saldo - valor;
	}
	public void imprimirSaldo(){
		//disponível em toda classe
		System.out.println(saldo);
		//somente o método sacar conhece esta variavel
		System.out.println(novoSaldo);
	
	}
	public double calcularDividaExponencial(){
		//variável local de método
		double valorParcela = 50.0;
		double valorMontante = 0.0; // começando a variável com valor zero
		for(int x=1; x<=5; x++) {//x variável de escopo de fluxo
			//esta variável será reiniciada a cada execução for
			double valorCalculado = valorParcela * x;
			valorMontante = valorMontante + valorCalculado;
		}
		//escopo de fluxo
		//x e valorCalculado nunca estarão disponíveis fora do for
		
		return valorMontante;
	}
}
```