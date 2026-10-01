# Chicago: perfis criminais por distrito

Projeto final da Equipe 04 da CESAR School. Análise acadêmica e descritiva de Chicago (2012–2017).
**2017 é parcial e termina em 18/01/2017 nesta base.** Não há modelos preditivos ou afirmações causais.

## Entrega

- [Notebook executado](Equipe_04_Chicago_Final.ipynb), com código, texto, tabelas e gráficos salvos.
- [Base original completa, compactada](dados/Chicago_Crimes_2012_to_2017.csv.gz). A descompactação recupera o CSV original, com todas as colunas e registros.
- [Slides: Recomendações para o CEO](Recomendacoes_para_o_CEO.pptx), com gráficos editáveis e hipóteses de investigação.
- [Prévia HTML](Equipe_04_Chicago_Final.html), que pode ser aberta localmente sem executar código.
- [Tabelas, figuras e manifesto](resultados/).

## Resultados

1,456,714 registros de entrada; 1,456,686 elegíveis; 22 distritos.
IDs deduplicados, distritos inteiros de 1 a 25 e mais de 10 registros por distrito.
Os códigos 13, 21 e 23 não possuem registros elegíveis neste arquivo e não foram inventados.
Arrest e Domestic são booleanos; ausências não são convertidas em False.

Oito percentuais (THEFT, BATTERY, NARCOTICS, ASSAULT, ROBBERY, HOMICIDE, Arrest e Domestic),
StandardScaler e Ward/Euclidiana. Código do distrito e volume ficam fora da distância.
Cada percentual usa todos os registros elegíveis do distrito como denominador.
O melhor k entre 2 e 6 foi 2: Silhouette 0.4671, Davies–Bouldin 0.7575.

| Grupo | Distritos | Furto (%) | BATTERY (%) | Doméstico (%) |
|---|---|---:|---:|---:|
| 1 | 1, 12, 14, 16, 17, 18, 19, 20 | 34.06 | 13.95 | 8.79 |
| 2 | 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 15, 22, 24, 25 | 17.71 | 20.01 | 17.85 |

Os percentuais acima são médias com peso igual por distrito. Percentuais ponderados pelo volume são exportados separadamente.
Average e Complete reproduzem a partição Ward no mesmo k (ARI=1).
Davies–Bouldin favorece k=3 (0,6724), enquanto a regra de escolha prioriza a Silhouette e seleciona k=2.
Retirar homicídios ou retirar 2017 parcial mantém a partição Ward (ARI=1).

**HOMICIDE representa registros/vítimas**, conforme a [documentação municipal](https://data.cityofchicago.org/Public-Safety/Homicides/k9xv-yxzs).
Não equivale ao número de eventos de homicídio. Arrest não mede elucidação ou eficiência policial.
As proporções não são risco individual, taxas por população ou evidência causal.

## Executar

Python 3.14.3 foi usado na execução validada. Instale as dependências num ambiente virtual:

```bash
python -m pip install -r requirements.txt
python -m ipykernel install --user --name python3
python -m jupyter nbconvert --execute --to notebook --inplace Equipe_04_Chicago_Final.ipynb
```

Execute na raiz deste repositório. O notebook lê `dados/Chicago_Crimes_2012_to_2017.csv.gz`.
Se a base local não estiver presente, baixa exatamente a versão 1 do Kaggle com kagglehub,
verifica a assinatura ZIP quando necessário e valida o SHA-256 do CSV descompactado.
Em Colab, abra o notebook e execute todas as células. Se houver pacote ausente,
instale pandas, numpy, scipy, scikit-learn, matplotlib, seaborn, nbformat, nbclient e kagglehub com `%pip install`.

## Fonte e proveniência

[Kaggle: currie32/crimes-in-chicago, versão 1](https://www.kaggle.com/datasets/currie32/crimes-in-chicago/versions/1).
Arquivo: `Chicago_Crimes_2012_to_2017.csv`. SHA-256 do CSV original:
`44008f2caac73d560fd28515e550bf7cd2431e164ca992becd30e1f3c931aa35`.
O gzip inclui a base original integral, sem regravar linhas ou mudar os bytes do CSV.
A base deriva do Chicago Data Portal e mantém as condições de uso da fonte;
este repositório não atribui uma licença nova aos dados de terceiros.

Materiais da disciplina foram consultados e relacionados no apêndice do notebook.
Os PDFs e notebooks didáticos não são redistribuídos neste repositório.
Notebook de referência: [Colab da equipe](https://colab.research.google.com/drive/1N4DXlE8QAsRX1rPvHVV4GlHykSipf0jX).

## Equipe

Mauro Roberto Barbosa Cahu, Pedro Paulo Sant'Anna Belo Ramos,
Renato Vasconcellos Bittencourt Neto e Vinicius Dantas Batista da Silva.
