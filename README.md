# ⚽ Copa do Mundo 2026 — Simulador

Simulador interativo do bracket mata-mata da Copa do Mundo FIFA 2026, com probabilidades baseadas em Elo Rating.

**[→ Abrir simulador](https://l34ndro-s.github.io/wc2026/)**

## Como usar

- Clique em um time em qualquer jogo futuro para fixá-lo como vencedor daquela partida
- Clique novamente para remover a fixação
- O bracket propaga automaticamente os vencedores para as fases seguintes
- Disponível em português, inglês e espanhol
- Suporta modo claro e escuro

## Modelo probabilístico

### Probabilidade por confronto

Cada jogo futuro exibe a probabilidade de vitória de cada time calculada pelo **Elo Rating**:

```
P(A vence B) = 1 / (1 + 10 ^ ((Elo_B - Elo_A) / 400))
```

Os ratings utilizados são os valores do [eloratings.net](https://eloratings.net) de junho de 2026.

### Probabilidade de ser campeão

Calculada **analiticamente** — sem simulações Monte Carlo.

Para cada jogo do bracket, a distribuição de probabilidade sobre os possíveis participantes é propagada recursivamente usando os ratings Elo. O jogo da final retorna a distribuição completa de probabilidade de campeonato para todos os times.

Exemplo para um semifinalista que pode enfrentar A ou B na final:

```
P(T campeão) =
  P(A chega à final) × P(T vence A) +
  P(B chega à final) × P(T vence B)
```

Isso se aplica recursivamente para todas as rodadas.

### Resultado dos locks

Quando o usuário fixa um time vencedor, essa fixação afeta **somente o display** do bracket — qual time aparece avançando para a próxima fase. A probabilidade de campeonato continua sendo calculada pelos ratings Elo reais de cada confronto, sem atribuir 100% ao time fixado.

## Dados em tempo real

O bracket é carregado diretamente de [openfootball/worldcup.json](https://github.com/openfootball/worldcup.json) a cada acesso. Resultados dos jogos já disputados são aplicados automaticamente.

## Fontes

| Dado | Fonte |
|------|-------|
| Bracket e resultados | [openfootball/worldcup.json](https://github.com/openfootball/worldcup.json) |
| Elo Ratings | [eloratings.net](https://eloratings.net) — jun/2026 |
| Bandeiras | [hampusborgos/country-flags](https://github.com/hampusborgos/country-flags) |

## Tecnologia

Página única em HTML/CSS/JS — sem frameworks, sem build, sem dependências instaladas.
