# Use Métodos de Acesso em Classes Públicas (Tell Don´t Ask)
```java
public class Horario {

    private int[] valores = new int[2];
//    private int hora;
//    private int minuto;

    public Horario(int hora, int minuto) {
        setHora(hora);
        setMinuto(minuto);
    }

    public int getHora() {
//        return hora;
        return valores[0];
    }

    public void setHora(int hora) {
        if (hora < 0 || hora > 23) {
            throw new IllegalArgumentException("Hora inválida: " + hora);
        }

//        this.hora = hora;
        this.valores[0] = hora;
    }

    public int getMinuto() {
//        return minuto;
        return valores[1];
    }

    public void setMinuto(int minuto) {
        if (minuto < 0 || minuto > 59) {
            throw new IllegalArgumentException("Minuto inválido: " + minuto);
        }

//        this.minuto = minuto;
        this.valores[1] = minuto;
    }

    public String formatar() {
        return String.format("%dh%dm", getHora(), getMinuto());
    }

}
```

```java
public class Principal {

    public static void main(String[] args) {
        Horario horario = new Horario(10, 55);
//        System.out.printf("%dh%dm", horario.getHora(), horario.getMinuto()); tell, dont ask
        System.out.println(horario.formatar());
    }

}
```
---
## Não permita instanciação com construtor privado

```java
public class CalculadoraArea {

    public static final double PI = 3.14159265358979323846;

    private CalculadoraArea() {
    }

    public static double calcularAreaQuadrado(double medidaDoLado) {
        return medidaDoLado * medidaDoLado;
    }

    public static double calcularAreaCirculo(double raio) {
        return raio * raio * CalculadoraArea.PI;
    }

}
```

```java
import matematica.CalculadoraArea;

public class Principal {

    public static void main(String[] args) {
        double areaQuadrado = CalculadoraArea.calcularAreaQuadrado(5.2);
        double areaCirculo = CalculadoraArea.calcularAreaCirculo(10.5);

        System.out.printf("PI: %.2f%n", CalculadoraArea.PI);
        System.out.printf("Área do quadrado: %.2f%n", areaQuadrado);
        System.out.printf("Área do círculo: %.2f%n", areaCirculo);
    }

}
```
---
## Crie cópias defensivas
```java
package com.algaworks.agenda;

public class Horario {

    private int hora;
    private int minuto;

    public Horario(int hora, int minuto) {
        setHora(hora);
        setMinuto(minuto);
    }

    public int getHora() {
        return hora;
    }

    public void setHora(int hora) {
        if (hora < 0 || hora > 23) {
            throw new IllegalArgumentException("Hora inválida: " + hora);
        }

        this.hora = hora;
    }

    public int getMinuto() {
        return minuto;
    }

    public void setMinuto(int minuto) {
        if (minuto < 0 || minuto > 59) {
            throw new IllegalArgumentException("Minuto inválido: " + minuto);
        }

        this.minuto = minuto;
    }

    public String formatar() {
        return String.format("%dh%dm", getHora(), getMinuto());
    }

}
```

```java
package com.algaworks.agenda;

public class Agendamento {

    private final Horario horario;
    private String descricao;

    public Agendamento(Horario horario, String descricao) {
        this.horario = new Horario(horario.getHora(), horario.getMinuto());
        this.descricao = descricao;
    }

    public Horario getHorario() {
        return new Horario(horario.getHora(), horario.getMinuto());
    }

    public String getDescricao() {
        return descricao;
    }

    public void setDescricao(String descricao) {
        this.descricao = descricao;
    }

    public String getHorarioFormatado() {
        return horario.formatar();
    }

}
```

```java
package com.algaworks.agenda;

public class Principal {

    public static void main(String[] args) {
        Horario horario = new Horario(10, 30);
        Agendamento agendamentoCabelo = new Agendamento(horario, "Corte de cabelo");
        agendamentoCabelo.getHorario().setHora(20);

        horario.setHora(19);
        Agendamento agendamentoBarba = new Agendamento(horario, "Feitio de barba");

        imprimir(agendamentoCabelo);
        imprimir(agendamentoBarba);
    }

    private static void imprimir(Agendamento agendamento) {
        System.out.printf("%s às %s%n", agendamento.getDescricao(), agendamento.getHorarioFormatado());
    }

}
```
---
## Minimize a mutabilidade (incluindo Value Object)
```java
package com.algaworks.agenda;

public class Agendamento {

    private Horario horario;
    private String descricao;

    public Agendamento(Horario horario, String descricao) {
        this.horario = horario;
        this.descricao = descricao;
    }

    public Horario getHorario() {
        return horario;
    }

    public void setHorario(Horario horario) {
        this.horario = horario;
    }

    public String getDescricao() {
        return descricao;
    }

    public void setDescricao(String descricao) {
        this.descricao = descricao;
    }

    public String getHorarioFormatado() {
        return horario.formatar();
    }

}
```

```java
package com.algaworks.agenda;

public class CalculadoraHorario {

    private CalculadoraHorario() {
    }

    public static Horario somarDuasHoras(Horario horario) {
        int hora = horario.getHora() + 2;

        if (hora > 24) {
            hora = hora - 24;
        }

//        horario.setHora(hora);
//        return horario;

        return new Horario(hora, horario.getMinuto());
    }

}
```

```java
package com.algaworks.agenda;

public final class Horario {

    private final int hora;
    private final int minuto;

    public Horario(int hora, int minuto) {
        if (hora < 0 || hora > 23) {
            throw new IllegalArgumentException("Hora inválida: " + hora);
        }
        if (minuto < 0 || minuto > 59) {
            throw new IllegalArgumentException("Minuto inválido: " + minuto);
        }

        this.hora = hora;
        this.minuto = minuto;
    }

    public int getHora() {
        return hora;
    }

    public int getMinuto() {
        return minuto;
    }

    public String formatar() {
        return String.format("%dh%dm", getHora(), getMinuto());
    }

}
```

```java
package com.algaworks.agenda;

public class Principal1 {

    public static void main(String[] args) {
        Integer idade = 30;
        Integer novaIdade = idade + 1;

        Horario horario = new Horario(10, 30);
//        horario.setHora(15);
    }

}
```

```java
package com.algaworks.agenda;

public class Principal2 {

    public static void main(String[] args) {
        Horario horario = new Horario(10, 30);
        Agendamento agendamentoCabelo = new Agendamento(horario, "Corte de cabelo");

        Horario novoHorario = CalculadoraHorario.somarDuasHoras(horario);

        agendamentoCabelo.setHorario(new Horario(16, 20));

        System.out.println(agendamentoCabelo.getHorarioFormatado());
        System.out.println(novoHorario.formatar());
    }

}
```
---
# Records
```java
package com.algaworks.agenda;

public record Horario(int hora, int minuto) {

    public Horario {
        if (hora < 0 || hora > 23) {
            throw new IllegalArgumentException("Hora inválida: " + hora);
        }
        if (minuto < 0 || minuto > 59) {
            throw new IllegalArgumentException("Minuto inválido: " + minuto);
        }
    }

    public String formatar() {
        return String.format("%dh%dm", hora(), minuto());
    }

}
```

```java
package com.algaworks.agenda;

public class Agendamento {

    private Horario horario;
    private String descricao;

    public Agendamento(Horario horario, String descricao) {
        this.horario = horario;
        this.descricao = descricao;
    }

    public Horario getHorario() {
        return horario;
    }

    public void setHorario(Horario horario) {
        this.horario = horario;
    }

    public String getDescricao() {
        return descricao;
    }

    public void setDescricao(String descricao) {
        this.descricao = descricao;
    }

    public String getHorarioFormatado() {
        return horario.formatar();
    }

}
```

```java
package com.algaworks.agenda;

public class Principal {

    public static void main(String[] args) {
        Horario horario = new Horario(10, 30);

        Agendamento agendamentoCabelo = new Agendamento(horario, "Corte de cabelo");
        agendamentoCabelo.setHorario(new Horario(16, 20));

        System.out.println(agendamentoCabelo.getHorarioFormatado());
    }

}
```
---
### [[Unified Modeling Language#Records|Diagrama de Classes: Records]]
![[record.png]]
![[record-exemplo.png]]