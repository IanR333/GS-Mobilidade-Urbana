# 🚌 Global Solution — CitizenTech
## Mobilidade Urbana Inteligente: Modelagem Matemática para a Gestão do Transporte Público

**FIAP — Modelagem Matemática e Computacional**

## 👥 Integrantes

| Nome | RM | GitHub |
|---|---|---|
| Ian Rodrigues Martins | 570540 | [@IanR333](https://github.com/IanR333) |
| Patrick Fernandes Martins Pais | 572899 | — |
| Gabriel Del Pizzo Pintor | 570436 | [@gabrieldelpizzo47-pixel](https://github.com/gabrieldelpizzo47-pixel) |

## 📌 Sobre o projeto

Uma empresa municipal de transporte perdeu os registros de quantos ônibus estavam alocados em cada região da cidade (Norte, Sul, Leste e Oeste). Restaram apenas alguns indicadores consolidados e uma pesquisa de demanda de passageiros.

Usando **sistemas lineares, matrizes e transformações lineares** implementados em **Python (NumPy)**, o projeto:

1. **Reconstrói** a distribuição atual da frota a partir dos registros operacionais;
2. **Diagnostica** os desequilíbrios entre oferta de ônibus e demanda de passageiros;
3. **Propõe** uma política de redistribuição modelada como transformação linear, provando que ela conserva a frota total e não gera valores negativos.

## 📂 Arquivos

| Arquivo | Descrição |
|---|---|
| `GS_Mobilidade_Urbana.ipynb` | Notebook com toda a modelagem matemática, código e resultados |

## 🧮 Etapa 1 — Diagnóstico da situação atual

Variáveis: `N`, `S`, `L`, `O` = número de ônibus em cada região.

Sistema linear `A·x = b`:

```
N +  S +  L +  O = 72
N + 2S       +  O = 76
     S + 2L       = 52
N       +  L + 2O = 76
```

- `det(A) = 3 ≠ 0` → posto(A) = posto([A|b]) = 4 → **sistema possível e determinado (solução única)**
- **Distribuição atual:** Norte = 12 · Sul = 20 · Leste = 16 · Oeste = 24 (total 72)
- Todos os registros operacionais foram verificados ✅

## 🔁 Etapa 2 — Política de redistribuição

| Região | Passageiros | Ônibus necessários | Atual | Saldo |
|---|---|---|---|---|
| Norte | 560 | 14 | 12 | −2 |
| Sul | 760 | 19 | 20 | +1 |
| Leste | 720 | 18 | 16 | −2 |
| Oeste | 840 | 21 | 24 | +3 |
| **Total** | **2880** | **72** | **72** | 0 |

**Política:** Oeste → Norte (2), Oeste → Leste (1), Sul → Leste (1). Apenas 4 ônibus são movidos, entre regiões vizinhas.

**Transformação linear** `T(x) = M·x`, em que `mᵢⱼ` = fração dos ônibus da região *j* enviada para a região *i*:

```
        N     S      L     O
N  [    1     0      0   1/12 ]
S  [    0   19/20    0    0   ]
L  [    0    1/20    1   1/24 ]
O  [    0     0      0   7/8  ]
```

- Cada coluna soma 1 → `1ᵀM = 1ᵀ` → **o total de ônibus é preservado**
- Todas as entradas são ≥ 0 → **nenhuma alocação negativa**
- Resultado: **(14, 19, 18, 21)**, atendendo 100% da demanda (antes, 160 passageiros ficavam sem vaga)

## ▶️ Como executar

1. Abra o notebook no [Google Colab](https://colab.research.google.com/) (Arquivo → Fazer upload de notebook) ou no Jupyter;
2. Execute todas as células (`Ambiente de execução → Executar tudo`).

Dependência: `numpy`
