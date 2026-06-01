# Dados

Esta pasta hospeda as bases consumidas pelos notebooks 03–06. Os arquivos
são gerados pelos notebooks 01 e 02 (com exceção do `cds_brasil_5y.csv`,
coletado manualmente do Investing.com).

## Conteúdo esperado

| Arquivo | Origem | Como obter |
|---|---|---|
| `dados_modelo_tcc_cdi.xlsx` | Gerado | Executar `notebooks/01_coleta_dados_cdi.ipynb` |
| `dados_modelo_tcc_di_futuro.xlsx` | Gerado | Executar `notebooks/02_coleta_dados_di_futuro.ipynb` |
| `cds_brasil_5y.csv` | Manual | Baixar de [Investing.com — CDS Brasil 5Y](https://br.investing.com/) |

Os arquivos `.xlsx` não são versionados por padrão (verifique `.gitignore`).
