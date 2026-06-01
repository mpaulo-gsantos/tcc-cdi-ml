# Aplicação de modelo de machine learning na previsão do CDI

Código-fonte do Trabalho de Conclusão de Curso de Engenharia de Produção
do Centro Universitário FEI, 2026.

**Autor:** Marcos Paulo Galli dos Santos
**Orientador:** Prof. Dr. José Agostinho Baitello
**Defesa:** <data da defesa>

## Sobre

Este repositório contém o pipeline completo do experimento descrito no TCC
*"Aplicação de modelo de machine learning na previsão do CDI e seus efeitos
na precificação de ativos financeiros"*. O trabalho:

1. Coleta automatizadamente 73 variáveis macroeconômicas, de mercado, de
   expectativas Focus e de comportamento informacional, entre setembro de 2022
   e abril de 2026.
2. Treina um modelo XGBoost para prever o CDI médio nos 22 dias úteis
   subsequentes a cada data, sob desenho experimental com embargo entre treino
   (jan/2023–nov/2025) e teste (jan/2026–mar/2026).
3. Avalia o modelo em três planos complementares: estatístico (métricas MAE,
   RMSE, MAPE e teste de Diebold-Mariano com correção HLN), interpretativo
   (SHAP) e econômico (precificação de uma debênture pós-fixada e da perna
   pós-fixada de um swap DI).

## Estrutura

| Notebook | Objetivo |
|---|---|
| `01_coleta_dados.ipynb` | Coleta das séries via APIs do BCB-SGS, Olinda-Focus, Yahoo Finance e CSV do Investing.com; consolida a base `dados_modelo_tcc_cdi.xlsx`. |
| `02_treinamento_xgboost.ipynb` | Construção do alvo (CDI médio em 22 du), validação cruzada temporal com embargo, busca em grade de hiperparâmetros e treinamento do modelo final. |
| `03_avaliacao_preditiva.ipynb` | Comparação tripla XGBoost × curva DI implícita × CDI realizado; cálculo de métricas e aplicação do teste de Diebold-Mariano (HAC Newey-West, correção HLN). |
| `04_analise_shap.ipynb` | Decomposição SHAP das previsões (importância global por feature e grupo, análises locais via waterfall, estabilidade temporal). |
| `05_precificacao.ipynb` | Conversão das três curvas em fatores acumulados; precificação de debênture pós-fixada e da perna pós-fixada de um swap DI; análise do erro de preço por sub-período. |

## Reprodução

### Requisitos
- Python 3.10+
- Pacotes em `requirements.txt`

### Instalação
```bash
git clone https://github.com/mpaulo-gsantos/tcc-cdi-ml.git
cd tcc-cdi-ml
pip install -r requirements.txt
```

### Execução
Os notebooks foram desenvolvidos no Google Colab. Para reproduzir localmente:
1. Execute `01_coleta_dados.ipynb` para gerar `dados_modelo_tcc_cdi.xlsx`.
2. Coloque o arquivo `cds_brasil_5y.csv` (Investing.com) no diretório `dados/`.
3. Execute os notebooks 02 a 05 na ordem indicada.

## Fontes de dados

| Origem | Acesso | Variáveis |
|---|---|---|
| Banco Central – SGS | API pública | CDI, Selic Over, Selic Meta, PTAX, IPCA, IPCA-15, núcleos, IBC-Br, Produção Industrial, Vendas no Varejo |
| Banco Central – Olinda | API pública | Boletim Focus (Selic, IPCA, PIB, câmbio — mediana, dispersão, nº de respondentes) |
| Yahoo Finance | `yfinance` | Ibovespa, Brent, WTI, soja CBOT, S&P 500, DXY |
| TradingView (não oficial) | `tvDatafeed` | Contratos DI Futuro (G/H/J/K 2026) |
| Investing.com | Download manual | CDS Brasil 5 anos |

## Citação

```bibtex
@thesis{santos2026cdi,
  author       = {Marcos Paulo Galli dos Santos},
  title        = {Aplicação de modelo de machine learning na previsão do CDI
                  e seus efeitos na precificação de ativos financeiros},
  type         = {Trabalho de Conclusão de Curso},
  institution  = {Centro Universitário FEI},
  address      = {São Bernardo do Campo},
  year         = {2026}
}
```

## Licença

[MIT](LICENSE)

## Limitações e ressalvas

- A biblioteca `tvDatafeed` é não-oficial e pode quebrar com alterações no
  protocolo do TradingView; estudos futuros se beneficiariam do uso de
  fontes oficiais (B3 ASTEC, plataformas profissionais).
- A janela de teste (jan–mar/2026) tem amplitude do CDI de apenas 0,26 p.p.
  e uma única decisão efetiva do Copom — reconhecida como limitação no §3.14
  do TCC. Replicar a metodologia em janelas voláteis é direção sugerida para
  trabalhos futuros (§5.6).
