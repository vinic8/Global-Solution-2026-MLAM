# Análise Estatística do Setor de Lançamentos Espaciais

Avaliação de **Estatística Descritiva** aplicada a uma base de dados **real** de missões
espaciais. Toda a solução está em **um único notebook** (`analise_missoes_espaciais.ipynb`),
pronto para rodar no **Google Colab**. O notebook lê a base a partir do arquivo
`space_missions1.csv` (incluído nesta entrega), que é enviado ao Colab no momento da
execução.

A análise cobre os cinco itens exigidos: seleção e justificativa da base, tabelas de
distribuição de frequências, gráficos estatísticos, análises univariadas (tendência
central, dispersão e separatrizes) e o relatório/interpretação consolidado.

---

## A base de dados (real, não simulada)

| Item | Descrição |
|------|-----------|
| **Nome** | Space Missions |
| **Arquivo** | `space_missions1.csv` |
| **Origem** | Coletada do portal *Next Spaceflight* (nextspaceflight.com) e distribuída em repositórios públicos (Kaggle / Maven Analytics Data Playground) |
| **Registros** | 4.626 lançamentos orbitais e suborbitais |
| **Período** | 1957 (Sputnik-1) a agosto de 2022 — cerca de 65 anos |
| **Abrangência** | 62 organizações, 370 foguetes e 22 países |

**Por que esta base?** É um conjunto **real, abrangente, bem estruturado e auditável**,
com variáveis quantitativas e qualitativas de boa qualidade. O tema (setor espacial)
tem alto valor analítico: permite estudar a evolução temporal do volume de lançamentos,
a confiabilidade operacional e a estrutura de custos do mercado.

### Dicionário de variáveis

| Variável | Descrição | Natureza |
|----------|-----------|----------|
| `Company` | Organização responsável | Qualitativa nominal |
| `Location` | Local / país de lançamento | Qualitativa nominal |
| `Year` | Ano do lançamento | **Quantitativa discreta** |
| `Time` | Horário do lançamento | Quantitativa (hora) |
| `Rocket` | Veículo lançador | Qualitativa nominal |
| `MissionStatus` | Desfecho (1 = sucesso; 0 = falha) | Qualitativa binária |
| `RocketStatus` | Situação do foguete (ativo / aposentado) | Qualitativa nominal |
| `Price` | Custo do lançamento (US$ milhões) | **Quantitativa contínua** |
| `Mission` | Nome da missão / carga útil | Qualitativa nominal |

As duas variáveis quantitativas centrais da análise são **`Year`** (discreta) e
**`Price`** (contínua).

> **Observação sobre qualidade dos dados:** o campo `Price` está preenchido em ~27% das
> missões (1.264 de 4.626) — custos de lançamento raramente são públicos. As análises de
> preço são, portanto, conduzidas sobre os registros disponíveis. O campo `Time` traz um
> artefato de exportação do Excel (data fictícia `1899-12-30`); apenas a hora é válida.

---

## O que o notebook entrega (os 5 itens)

**Item 1 — Seleção e justificativa da base.** Base real *Space Missions*, justificada
por relevância, qualidade, aderência ao tema e potencial analítico.

**Item 2 — Tabelas de distribuição de frequências.**
- *Variável discreta* (`Year`, agrupada por década): frequências absoluta, relativa,
  acumulada e relativa acumulada.
- *Variável contínua* (`Price`, em classes por faixa de custo): mesmas colunas, com ponto
  médio de cada classe.

**Item 3 — Gráficos estatísticos.** Cinco gráficos com título, rótulos de eixos, cores e
legendas, usando variáveis diferentes (década, preço, organização e taxa de sucesso):
lançamentos por década, histograma de preço, top 10 organizações, sucesso/falha por
década com taxa de sucesso, e boxplot de preço.

**Item 4 — Análises univariadas.** Para `Year` e `Price`: média, mediana, moda; máximo,
mínimo, amplitude, variância e desvio padrão; quartis (Q1, Q2, Q3) e intervalo
interquartílico — cada uma acompanhada de interpretação.

**Item 5 — Relatório e interpretação.** Conclusões consolidadas em linguagem técnica ao
longo do notebook, com leitura de negócio dos resultados.

### Principais resultados

- **Volume:** pico histórico nos anos 1970 (1.012 lançamentos); 53,3% de todas as missões
  ocorreram até o fim dos anos 1980; forte retomada a partir dos anos 2010.
- **Confiabilidade:** taxa de sucesso global de **89,9%**, subindo de 31,4% (anos 1950)
  para patamar estável acima de 92% desde os anos 1970.
- **Custo:** distribuição fortemente assimétrica à direita — mediana de **US$ 63 mi**
  contra média de **US$ 128 mi** (coeficiente de variação ≈ 200%). Cerca de 70% dos
  lançamentos custam menos de US$ 100 mi; outliers como o Energiya/Buran (US$ 5.000 mi)
  e o Saturn V (US$ 1.160 mi) puxam a média. Recomenda-se a **mediana** como medida de
  custo típico.

---

## Arquivos da entrega

- **`analise_missoes_espaciais.ipynb`** — notebook com todo o código, narrativa, tabelas
  e os 5 gráficos (com saídas já executadas e visíveis).
- **`space_missions1.csv`** — base de dados (enviada ao Colab na execução).
- **`README.md`** — este arquivo.

Tecnologias: **Python 3**, `pandas`, `numpy`, `matplotlib`.

---

## Notas metodológicas

- **Agrupamento da variável discreta:** `Year` assume 66 valores distintos; o agrupamento
  por **década** preserva a leitura temporal e torna a tabela interpretável.
- **Classes da variável contínua:** a regra de Sturges sugeriu 11 classes, mas, devido à
  forte assimetria, ~99% dos dados caíam em uma única classe. Adotaram-se, então, **faixas
  de custo de mercado** ([2;30), [30;60), [60;100), [100;200), [200;500), [500;5000)),
  que preservam o poder interpretativo da distribuição.
- **Escopo:** a análise é estritamente descritiva e não infere relações de causa e efeito.
