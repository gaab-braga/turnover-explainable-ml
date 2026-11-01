# Turnover com random forest, SHAP e curva de sobrevivência

Um notebook que estuda por que as pessoas saem de uma empresa e gera uma base de risco por colaborador para o Power BI.

## Dados

`Base_RH.csv`: 1.470 colaboradores, 21 colunas, com nomes em português. 16,1% saíram da empresa. O tamanho e a taxa de saída são os mesmos da base pública IBM HR Analytics Employee Attrition (dados fictícios), usada também no [hr-attrition-analytics](https://github.com/gaab-braga/hr-attrition-analytics).

## O que o notebook faz

1. Limpa a base e transforma a coluna de saída em 0 e 1.
2. Cria três indicadores:
   - **Índice de estagnação**: anos sem promoção dividido pelo tempo de casa, multiplicado por um peso que cresce quanto menor o último aumento.
   - **Índice de pressão**: hora extra (0 ou 1) somada à frequência de viagens (0 a 2).
   - **Fidelidade à gestão**: anos com o mesmo chefe dividido pelo tempo de casa.
3. Diagnóstico em gráficos: correlação com a saída, turnover por departamento, por faixa salarial e por estado civil.
4. Curva de Kaplan-Meier: a chance de continuar na empresa ao longo dos anos de casa.
5. Random forest: separa 25% da base para teste (estratificado), escolhe os hiperparâmetros com `RandomizedSearchCV` (20 combinações, validação cruzada de 3 dobras, pela AUC) e avalia no teste.
6. SHAP para mostrar quais variáveis mais pesam na previsão.
7. Regras de ação para quem tem risco acima de 50%: hora extra vira "burnout", mais de 3 anos sem promoção vira "estagnação", salário abaixo da mediana vira "salarial", e assim por diante.
8. Exporta `Base_PowerBI_Final.csv` (separador `;` e vírgula decimal) com o risco, o motivo e a categoria de cada pessoa.

## Resultados (conjunto de teste, 368 pessoas, 59 saídas)

| Métrica | Valor |
|---|---|
| AUC | 0,771 |
| Precisão para "saiu" | 0,44 |
| Recall para "saiu" | 0,20 |
| Acurácia | 0,83 |

Com o corte em 50%, o modelo encontra só 20% das pessoas que saíram. A acurácia de 0,83 é menor que a de quem chuta "ninguém sai" (0,84 neste teste), então a comparação deve ser feita pela AUC. O gráfico de precisão e recall por corte, no notebook, mostra quanto recall se ganha baixando o corte.

Os números vêm das saídas salvas no notebook.

## Limitações

- **O risco de cada pessoa é calculado dentro da amostra.** O modelo final dá nota para a base inteira, inclusive para os 75% que usou no treino. As 22 pessoas ativas com risco acima de 50% saem dessa nota, que tende a ser otimista. O [hr-attrition-analytics](https://github.com/gaab-braga/hr-attrition-analytics) resolve isso com previsão fora da dobra (`cross_val_predict`).
- **A simulação de retorno usa premissas, não dados.** O notebook supõe R$ 50.000 para repor uma pessoa, R$ 2.000 por ação de retenção, que metade da lista sairia e que 30% seriam retidos. O resultado (240,9%) só mostra a conta com esses valores.
- As variáveis de texto viram colunas 0/1 (`get_dummies`) antes da divisão entre treino e teste. Não vaza o alvo, mas o certo seria fazer isso dentro de um `Pipeline`.
- O SHAP é calculado no conjunto de treino.
- Os dados são fictícios. As regras de ação são exemplo de como usar a nota, não foram testadas.

## Como rodar

```bash
pip install pandas numpy scikit-learn shap lifelines matplotlib seaborn
jupyter notebook notebook.ipynb
```

O `Base_RH.csv` precisa estar na mesma pasta do notebook.

## Arquivos

```
notebook.ipynb          análise completa
Base_RH.csv             base de entrada
Base_PowerBI_Final.csv  saída para o Power BI (gerada pelo notebook)
```
