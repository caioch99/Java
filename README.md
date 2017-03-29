# Java
Aula

Fontes https://pt.scribd.com/document/217373092/Padroes-de-Projeto-Solucoes-Reutilizaveis-de-Software-Orientado-a-Objetos-Erich-Gamma-pdf
https://kelvinrodrigues.wordpress.com/2015/03/10/o-que-sao-padroes-de-projeto-gof-gang-of-four/

Exemplo de Prototype : Cria um objeto duplicado ou um clone do objeto

public abstract class CarroPrototype {
    protected double valorCompra;
 
    public abstract String exibirInfo();
 
    public abstract CarroPrototype clonar();
 
    public double getValorCompra() {
        return valorCompra;
    }
 
    public void setValorCompra(double valorCompra) {
        this.valorCompra = valorCompra;
    }
}

public class FiestaPrototype extends CarroPrototype {

   protected FiestaPrototype(FiestaPrototype fiestaPrototype) {
        this.valorCompra = fiestaPrototype.getValorCompra();
    }
 
    public FiestaPrototype() {
        valorCompra = 0.0;
    }
 
    @Override
    public String exibirInfo() {
        return "Modelo: Fiesta\nMontadora: Ford\n" + "Valor: R$"
                + getValorCompra();
    }
 
    @Override
    public CarroPrototype clonar() {
        return new FiestaPrototype(this);
    }
 
}

public static void main(String[] args) {
    PalioPrototype prototipoPalio = new PalioPrototype();
 
    CarroPrototype palioNovo = prototipoPalio.clonar();
    palioNovo.setValorCompra(27900.0);
    CarroPrototype palioUsado = prototipoPalio.clonar();
    palioUsado.setValorCompra(21000.0);
 
    System.out.println(palioNovo.exibirInfo());
    System.out.println(palioUsado.exibirInfo());
}

Decorator : Adicionar responsabilidades para objetos dinamicamente

public abstract class Coquetel {
    String nome;
    double preco;
 
    public String getNome() {
        return nome;
    }
 
    public double getPreco() {
        return preco;
    }
}

public class Caipirinha extends Coquetel {
    public Caipirinha() {
        nome = "Caipirinha";
        preco = 3.5;
    }
}

public class Refrigerante extends CoquetelDecorator {
 
   public Refrigerante(Coquetel umCoquetel) {
        super(umCoquetel);
        nome = "Refrigerante";
        preco = 1.0;
    }
 
}


public static void main(String[] args) {
        Coquetel meuCoquetel = new Cachaca();
        System.out.println(meuCoquetel.getNome() + " = "
                + meuCoquetel.getPreco());
 
        meuCoquetel = new Refrigerante(meuCoquetel);
        System.out.println(meuCoquetel.getNome() + " = "
                + meuCoquetel.getPreco());
    }
    
    
    
Singleton : Garante que a classe só tenha uma instância


public class Singleton {
	private static Singleton uniqueInstance;

	private Singleton() {
	}

	public static synchronized Singleton getInstance() {
		if (uniqueInstance == null)
			uniqueInstance = new Singleton();

		return uniqueInstance;
	}
}


