package controller;

import model.CalcadaIrregular;
import model.Degrau;
import model.Obstaculo;
import model.RampaInexistente;
import service.MapaService;

/**
 * Controller do sistema RotaAcessivel.
 * Faz a ponte entre a View (menu) e o Service (regras/operacoes do mapa).
 */
public class ObstaculoController {

    private MapaService mapaService;

    public ObstaculoController() {
        this.mapaService = new MapaService();
    }

    public void carregarDadosExemplo() {
        adicionarObstaculo(new Degrau("Rua Augusta, 100", "Degrau alto na entrada da farmacia", 8, 25.5));
        adicionarObstaculo(new CalcadaIrregular("Av. Paulista, 1500", "Buracos na via de pedestres", 6, "Raizes de arvore quebrando o cimento"));
        adicionarObstaculo(new RampaInexistente("Rua Consolacao, 50", "Cruzamento sem guia rebaixada", 10, "Esquina com Rua Oscar Freire"));
        System.out.println("3 obstaculos de exemplo carregados.\n");
    }

    public void adicionarObstaculo(Obstaculo obstaculo) {
        mapaService.adicionarPonto(obstaculo);
    }

    public void listarObstaculos() {
        mapaService.listarAlertas();
    }

    public void buscarObstaculo(String palavraChave) {
        mapaService.buscarObstaculo(palavraChave);
    }

    public void atualizarNivelPerigo(int numero, int novoNivel) {
        mapaService.atualizarNivelPerigo(numero, novoNivel);
    }

    public void removerObstaculo(int numero) {
        mapaService.removerObstaculo(numero);
    }

    public void exibirEstatisticas() {
        mapaService.exibirEstatisticas();
    }

    public int getTotalObstaculos() {
        return mapaService.getTotalObstaculos();
    }
}
