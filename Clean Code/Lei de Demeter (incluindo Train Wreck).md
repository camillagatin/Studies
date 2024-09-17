```java
import com.algaworks.locacao.GrupoVeiculo;
import com.algaworks.locacao.Locacao;
import com.algaworks.locacao.servico.ServicoDeLocacao;
import com.algaworks.locacao.Veiculo;

public class Principal {

    public static void main(String[] args) {
        GrupoVeiculo grupo = new GrupoVeiculo("SUV", 450);
        Veiculo veiculo = new Veiculo("ALG-9999", grupo);
        Locacao locacao = new Locacao(veiculo, 5);

        ServicoDeLocacao servicoDeLocacao = new ServicoDeLocacao();
        servicoDeLocacao.confirmarLocacao(locacao);
    }

}
```

```java
package com.algaworks.locacao;

public class Locacao {

    private Veiculo veiculo;
    private int quantidadeDiarias;

    public Locacao() {
    }

    public Locacao(Veiculo veiculo, int quantidadeDiarias) {
        this.veiculo = veiculo;
        this.quantidadeDiarias = quantidadeDiarias;
    }

    public Veiculo getVeiculo() {
        return veiculo;
    }

    public void setVeiculo(Veiculo veiculo) {
        this.veiculo = veiculo;
    }

    public int getQuantidadeDiarias() {
        return quantidadeDiarias;
    }

    public void setQuantidadeDiarias(int quantidadeDiarias) {
        this.quantidadeDiarias = quantidadeDiarias;
    }

    public double getValorDiaria() {
        return veiculo.getValorDiaria();
    }

    public double calcularTotalDiarias() {
        return getValorDiaria() * quantidadeDiarias;
    }

    public void reservarVeiculo() {
        veiculo.setDisponivel(false);
    }

}
```

```java
package com.algaworks.locacao;

public class Veiculo {

    private String placa;
    private boolean disponivel = true;
    private GrupoVeiculo grupo;

    public Veiculo() {
    }

    public Veiculo(String placa, GrupoVeiculo grupo) {
        this.placa = placa;
        this.grupo = grupo;
    }

    public String getPlaca() {
        return placa;
    }

    public void setPlaca(String placa) {
        this.placa = placa;
    }

    public boolean isDisponivel() {
        return disponivel;
    }

    public void setDisponivel(boolean disponivel) {
        this.disponivel = disponivel;
    }

    public GrupoVeiculo getGrupo() {
        return grupo;
    }

    public void setGrupo(GrupoVeiculo grupo) {
        this.grupo = grupo;
    }

    public double getValorDiaria() {
        return grupo.getValorDiaria();
    }

}
```

```java
package com.algaworks.locacao.servico;

import com.algaworks.locacao.Locacao;
import com.algaworks.locacao.Veiculo;

public class ServicoDeLocacao {

    public void confirmarLocacao(Locacao locacao) {
//        double totalDiarias = locacao.getVeiculo().getGrupo().getValorDiaria()
//                * locacao.getQuantidadeDiarias();

//        double totalDiarias = locacao.getValorDiaria()
//                * locacao.getQuantidadeDiarias();

        double totalDiarias = locacao.calcularTotalDiarias();

        // TODO realiza lógica para registrar locação pelo valor das diárias

//        locacao.getVeiculo().setDisponivel(false);
        locacao.reservarVeiculo();
    }

}
```

```java
import com.algaworks.locacao.GrupoVeiculo;
import com.algaworks.locacao.Locacao;
import com.algaworks.locacao.servico.ServicoDeLocacao;
import com.algaworks.locacao.Veiculo;

public class Principal {

    public static void main(String[] args) {
        GrupoVeiculo grupo = new GrupoVeiculo("SUV", 450);
        Veiculo veiculo = new Veiculo("ALG-9999", grupo);
        Locacao locacao = new Locacao(veiculo, 5);

        ServicoDeLocacao servicoDeLocacao = new ServicoDeLocacao();
        servicoDeLocacao.confirmarLocacao(locacao);
    }

}
```
