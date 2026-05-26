
# RotaAcessível 

**Sistema de Mapeamento Colaborativo de Obstáculos Urbanos**

> Projeto A3 — Disciplinas: Algoritmos e Programação
> Universidade Anhembi Morumbi — 2026/1  
> Integrantes: **Arafat Maratuly** (RA 12526146265) · **Rinat Tagaibekov** (RA 12526144122)

---

## Sobre o Projeto

Pessoas com mobilidade reduzida — cadeirantes, idosos, gestantes — enfrentam diariamente barreiras arquitetônicas invisíveis para quem não precisa delas: um degrau sem rampa, uma calçada esburacada, um cruzamento sem guia rebaixada.

O **RotaAcessível** é um sistema de console em Java que permite que qualquer usuário **registre, consulte, atualize e remova** pontos de obstáculos urbanos de forma colaborativa (crowdsourcing). Os dados gerados ajudam tanto quem planeja um trajeto acessível quanto gestores públicos que precisam priorizar obras.

---

## Funcionalidades

| Opção | Operação | Descrição |
|-------|----------|-----------|
| 1 | **Adicionar** (CREATE) | Registra novo obstáculo: Degrau, Calçada Irregular ou Rampa Inexistente |
| 2 | **Listar** (READ) | Exibe todos os obstáculos cadastrados com detalhes completos |
| 3 | **Buscar** (READ) | Filtra obstáculos por palavra-chave na localização ou descrição |
| 4 | **Atualizar** (UPDATE) | Modifica o nível de perigo de um obstáculo existente |
| 5 | **Remover** (DELETE) | Remove um obstáculo do mapa (ex.: após reforma da via) |
| 6 | **Estatísticas** | Exibe contagem de obstáculos por faixa de risco |
| 0 | **Sair** | Encerra o programa |

---

## Arquitetura — Conceitos POO

O projeto demonstra os principais conceitos de Programação Orientada a Objetos:

### Herança
```
Obstaculo (abstract)
├── Degrau
├── CalcadaIrregular
└── RampaInexistente
```
As três subclasses herdam `localizacao`, `descricao` e `nivelDePerigo` de `Obstaculo` via `extends`, e chamam `super()` nos construtores para inicializar os atributos herdados.

### Polimorfismo (Override)
O método `exibirDetalhes()` é declarado como `abstract` em `Obstaculo` e sobrescrito (`@Override`) em cada subclasse com saída personalizada para seu tipo de barreira. Em `MapaService`, o loop chama `obs.exibirDetalhes()` sem conhecer o tipo concreto — o Java resolve em tempo de execução.

### Sobrecarga (Overload)
Todas as subclasses e `Usuario` possuem dois construtores:
- **Completo** — todos os atributos informados
- **Simplificado** — atributo específico assume valor padrão (ex.: `alturaDegrau = 5.0 cm`)

### Encapsulamento
Todos os atributos são `private`, acessados exclusivamente via `getters` e `setters` públicos.

### Coleção Polimórfica
`MapaService` mantém um `List<Obstaculo>` que armazena qualquer subclasse sem casting, graças ao polimorfismo.

---

## Estrutura de Pacotes

```
src/
├── model/
│   ├── Obstaculo.java         ← classe abstrata (pai)
│   ├── Degrau.java            ← subclasse: barreiras de altura
│   ├── CalcadaIrregular.java  ← subclasse: pavimento danificado
│   ├── RampaInexistente.java  ← subclasse: falta de rampa
│   └── Usuario.java           ← entidade do colaborador
├── service/
│   └── MapaService.java       ← CRUD + lógica de negócio
└── view/
    └── Main.java              ← menu interativo + validação de entrada
```

---

## Como Executar

### Pré-requisitos
- Java JDK 11 ou superior instalado
- Qualquer terminal (CMD, PowerShell, bash)

### Compilar
```bash
# Na pasta raiz do projeto (onde está /src)
javac -d out -sourcepath src src/view/Main.java src/model/*.java src/service/*.java
```

### Executar
```bash
java -cp out view.Main
```

### Saída esperada ao iniciar
```
============================================
   Bem-vindo ao RotaAcessivel!
   Sistema de Mapeamento de Obstaculos
   Usuario: Rinat
============================================
Obstaculo registrado com sucesso! Total no mapa: 1
Obstaculo registrado com sucesso! Total no mapa: 2
Obstaculo registrado com sucesso! Total no mapa: 3
3 obstaculos de exemplo carregados.

========== MENU PRINCIPAL ==========
1. Adicionar obstaculo
2. Listar todos os obstaculos
...
```

---

## Requisitos Técnicos Atendidos

| Requisito | Onde está implementado |
|-----------|----------------------|
| Mínimo 3 classes | `Obstaculo`, `Degrau`, `CalcadaIrregular`, `RampaInexistente`, `Usuario`, `MapaService` (6 classes) |
| Encapsulamento | Todos os atributos `private` com getters/setters em todos os arquivos |
| Construtores | Construtores parametrizados em todas as classes |
| Herança | `Degrau`, `CalcadaIrregular`, `RampaInexistente` extends `Obstaculo` |
| Polimorfismo (override) | `exibirDetalhes()` e `validarPosicao()` sobrescritos nas 3 subclasses |
| Sobrecarga (overload) | 2 construtores em cada subclasse e em `Usuario` |
| ArrayList | `List<Obstaculo>` em `MapaService` |
| Condicionais | `if/else` aninhados em validações + `switch-case` no menu e em `buscarObstaculo()` |
| Loops | `for` e `for-each` em `listarAlertas()`, `buscarObstaculo()`, `exibirEstatisticas()` |
| Validação | `try/catch` para entradas numéricas + checagens de nulo/vazio/intervalo |
| Pacotes | Organizado em `model`, `service`, `view` |
| Código comentado | Javadoc e comentários inline em todos os arquivos |

---

## Links

- **Vídeo de demonstração (Checkpoint 2):** https://youtu.be/-PKtDVYXWf0
- **Vídeo de apresentação (Checkpoint 1):** https://youtu.be/G1Ju18nRkPM
- MANZANO, José Augusto N. G.; OLIVEIRA, Jayr Figueiredo de. *Algoritmos: lógica para desenvolvimento de programação de computadores.* 29. ed. São Paulo: Érica, 2019.
- SOUZA, Marco A. Furlan de et al. *Algoritmos e lógica de programação: um texto introdutório para a engenharia.* 3. ed. São Paulo: Cengage Learning, 2019.
- DEITEL, Paul; DEITEL, Harvey. *Java: como programar.* 10. ed. São Paulo: Pearson, 2016.
