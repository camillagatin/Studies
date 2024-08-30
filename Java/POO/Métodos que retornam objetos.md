

IndiceMassaCorporal.java
```java
double resultado;
double peso;
double altura;
```

Paciente.java
```java
double peso;
double altura;

IndiceMassaCorporal calcularIndiceMassaCorporal() {
	IndiceMassaCorporal imc = new IndiceMassaCorporal();
	imc.resultado = peso / (altura * altura);
	imc.peso = peso;
	imc.altura = altura;

	return imc;
}
```

Principal.java
```java
Paciente paciente = new Paciente();
paciente.altura = 1.82;
paciente.peso = 175;

IndiceMassaCorporal imc = paciente.calcularIndiceMassaCorporal();

if (imc.resultado >= 30) {
	System.out.printf("Paciente com altura de %.2f e peso de %.2f " + "está com obesidade%n", imc.altura, imc.peso);
}

System.out.printf("IMC: %.2f%n", imc.resultado);
```

---
## Refatorando para tornar uma classe mais rica

IndiceMassaCorporal.java
```java
double resultado;
double peso;
double altura;

boolean estaComObesidade() {
    return resultado >= 30;
}

boolean estaAbaixoDoPesoIdeal() {
    return resultado < 18.5;
}
```

Paciente.java
```java
double peso;
double altura;

IndiceMassaCorporal calcularIndiceMassaCorporal() {
    IndiceMassaCorporal imc = new IndiceMassaCorporal();
    imc.resultado = peso / (altura * altura);
    imc.peso = peso;
    imc.altura = altura;

    return imc;
}
```

Principal.java
```java
Paciente paciente = new Paciente();
paciente.altura = 1.82;
paciente.peso = 175;

IndiceMassaCorporal imc = paciente.calcularIndiceMassaCorporal();

if (imc.estaComObesidade()) {
    System.out.printf("Paciente com altura de %.2f e peso de %.2f " + "está com obesidade%n", imc.altura, imc.peso);
}

System.out.printf("IMC: %.2f%n", imc.resultado);
```

## Discutindo nome e responsabilidade da classe

IndiceMassaCorporal.java
```java
double resultado;
double peso;
double altura;

boolean estaComObesidade() {
    return resultado >= 30;
}

boolean estaAbaixoDoPesoIdeal() {
    return resultado < 18.5;
}
```

Paciente.java → CalculadoraImc
```java
double peso;
double altura;

IndiceMassaCorporal calcular() {
    IndiceMassaCorporal imc = new IndiceMassaCorporal();
    imc.resultado = peso / (altura * altura);
    imc.peso = peso;
    imc.altura = altura;

    return imc;
}
```

Principal.java
```java
CalculadoraImc calculadoraImc = new CalculadoraImc();
calculadoraImc.altura = 1.82;
calculadoraImc.peso = 175;

IndiceMassaCorporal imc = calculadoraImc.calcular();

if (imc.estaComObesidade()) {
    System.out.printf("Paciente com altura de %.2f e peso de %.2f " + "está com obesidade%n", imc.altura, imc.peso);
}

System.out.printf("IMC: %.2f%n", imc.resultado);
```

## Métodos com argumentos

IndiceMassaCorporal.java
```java
double resultado;
double peso;
double altura;

boolean estaComObesidade() {
    return resultado >= 30;
}

boolean estaAbaixoDoPesoIdeal() {
    return resultado < 18.5;
}
```

CalculadoraImc.java
```java
IndiceMassaCorporal calcular(double peso, double altura) {
    IndiceMassaCorporal imc = new IndiceMassaCorporal();
    imc.resultado = peso / (altura * altura);
    imc.peso = peso;
    imc.altura = altura;

    return imc;
}
```

Principal.java
```java
CalculadoraImc calculadoraImc = new CalculadoraImc();
double peso = 175;
double altura = 1.82;

IndiceMassaCorporal imc = calculadoraImc.calcular(peso, altura);

if (imc.estaComObesidade()) {
	System.out.printf("Paciente com altura de %.2f e peso de %.2f " + "está com obesidade%n", imc.altura, imc.peso);
}

System.out.printf("IMC: %.2f%n", imc.resultado);
```

---
## Passando objetos como argumentos de métodos

IndiceMassaCorporal.java
```java
double resultado;
double peso;
double altura;

boolean estaComObesidade() {
    return resultado >= 30;
}

boolean estaAbaixoDoPesoIdeal() {
	return resultado < 18.5;
}
```

CalculadoraImc.java
```java
IndiceMassaCorporal calcular(Paciente paciente) {
	IndiceMassaCorporal imc = new IndiceMassaCorporal();
	imc.resultado = paciente.peso / (paciente.altura * paciente.altura);
	imc.peso = paciente.peso;
	imc.altura = paciente.altura;

	return imc;
}
```

Paciente.java
```java
double peso;
double altura;
```

Principal.java
```java
CalculadoraImc calculadoraImc = new CalculadoraImc();

Paciente joao = new Paciente();
joao.peso = 175;
joao.altura = 1.82;

IndiceMassaCorporal imc = calculadoraImc.calcular(joao);

if (imc.estaComObesidade()) {
	System.out.printf("Paciente com altura de %.2f e peso de %.2f " + "está com obesidade%n", imc.altura, imc.peso);
}

System.out.printf("IMC: %.2f%n", imc.resultado);
```

(~~ver desafios composição de objetos e metodos~~)