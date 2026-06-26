# ⚽ Copa do Mundo 2026 — Simulador

Simulador interativo do bracket mata-mata da Copa do Mundo FIFA 2026, com probabilidades baseadas em ratings de força de seleções.

**[→ Abrir simulador](https://l34ndro-s.github.io/wc2026/)**

## Como usar

- Clique em um time em qualquer jogo futuro para fixá-lo como vencedor daquela partida
- Clique novamente para remover a fixação
- O bracket propaga automaticamente os vencedores para as fases seguintes
- Disponível em português, inglês e espanhol
- Suporta modo claro e escuro

## Fontes de rating

O simulador oferece duas fontes de rating, alternáveis pelo botão no header:

| Fonte | Descrição |
|-------|-----------|
| **PELE** | Modelo de Nate Silver ([natesilver.net](https://www.natesilver.net/p/pele-international-football-rankings-soccer-ratings-projections)) — leva em conta força do adversário, local do jogo, margem de vitória e outros fatores |
| **WorldElo** | [eloratings.net](https://eloratings.net) — modelo Elo clássico para futebol internacional, atualizado a cada jogo |

Ao alternar a fonte, as simulações rodam novamente com os novos ratings.

## Modelo probabilístico

### Probabilidade por confronto

Cada jogo futuro exibe a probabilidade de vitória de cada time calculada pela fórmula Elo:

```
P(A vence B) = 1 / (1 + 10 ^ ((Rating_B - Rating_A) / 400))
```

### Probabilidade de ser campeão

Calculada via **Monte Carlo** com 30.000 simulações. Em cada simulação, os jogos futuros são resolvidos probabilisticamente usando os ratings Elo. O resultado é a frequência com que cada time vence o torneio.

As probabilidades de campeonato são calculadas **uma vez no carregamento da página** com ratings puros. Travar um time vencedor afeta apenas o display do bracket, não as probabilidades de campeonato — evitando o erro de atribuir 100% de chance a um resultado que pode ser improvável.

## Dados em tempo real

O bracket é carregado diretamente de [openfootball/worldcup.json](https://github.com/openfootball/worldcup.json) a cada acesso. Resultados dos jogos já disputados são aplicados automaticamente.

## Fontes

| Dado | Fonte |
|------|-------|
| Bracket e resultados | [openfootball/worldcup.json](https://github.com/openfootball/worldcup.json) |
| Rating PELE | [natesilver.net](https://www.natesilver.net/p/pele-international-football-rankings-soccer-ratings-projections) — jun/2026 |
| Rating WorldElo | [eloratings.net](https://eloratings.net) — jun/2026 |
| Bandeiras | [hampusborgos/country-flags](https://github.com/hampusborgos/country-flags) |

## Tecnologia

Página única em HTML/CSS/JS — sem frameworks, sem build, sem dependências instaladas.
