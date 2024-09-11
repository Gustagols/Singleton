# Singleton
atividade


public class Fila {
    private static Fila uniqueInstance;
    private int[] fila;
    private int capacidade;
    private int tamanho;
    private int frente;
    private int tras;

 
    private Fila(int capacidade) {
        this.capacidade = capacidade;
        this.fila = new int[capacidade];
        this.tamanho = 0;
        this.frente = 0;
        this.tras = -1;
    }

    public static synchronized Fila getInstance(int capacidade) {
        if (uniqueInstance == null) {
            uniqueInstance = new Fila(capacidade);
        }
        return uniqueInstance;
    }
    
    public void adicionar(int elemento) {
        if (tamanho == capacidade) {
            throw new RuntimeException("Fila cheia");
        }
        tras = (tras + 1) % capacidade;
        fila[tras] = elemento;
        tamanho++;
    }

    public int remover() {
        if (tamanho == 0) {
            throw new RuntimeException("Fila vazia");
        }
        int elemento = fila[frente];
        frente = (frente + 1) % capacidade;
        tamanho--;
        return elemento;
    }

    public boolean estaVazia() {
        return tamanho == 0;
    }

    public boolean estaCheia() {
        return tamanho == capacidade;
    }

    public int obterTamanho() {
        return tamanho;
    }

   
    public int getCapacidade() {
        return capacidade;
    }

    public void setCapacidade(int capacidade) {
        if (capacidade < tamanho) {
            throw new IllegalArgumentException("Capacidade não pode ser menor que o tamanho atual.");
        }
        this.capacidade = capacidade;
        int[] novaFila = new int[capacidade];
        for (int i = 0; i < tamanho; i++) {
            novaFila[i] = fila[(frente + i) % fila.length];
        }
        fila = novaFila;
        frente = 0;
        tras = tamanho - 1;
    }
}
