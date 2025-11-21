# Análise Estratégica de Turnover

**Classificação:** Técnico & Estratégico  
**Status:** Produção  
**Autor:** Gabriel Braga

---

## A Pergunta Estratégica

O turnover é realmente o problema? Ou o problema é não entender quem está saindo e por quê?

Esta análise responde a essa questão através de três camadas integradas que transformam "saída de pessoas" em uma narrativa clara e orientada a decisões de negócio.

---

## Framework de Análise em Três Camadas

### Camada 1: Estratégia | O Impacto Financeiro Real

Em vez de tratar turnover como um número isolado, analisamos pela ótica de contribuição e risco: quem entrega mais, quem sustenta a operação e quais perfis merecem atenção imediata.

A discussão deixa de ser "perdemos pessoas" e passa a ser: **estamos perdendo a parte errada da força de trabalho?**

### Camada 2: Diagnóstico | Por Que Isso Está Acontecendo?

Ao aprofundar comportamento, carga de trabalho e contexto organizacional, identificamos que muitas saídas não têm relação direta com salário. Elas acontecem por sobrecarga, exaustão ou desalinhamento de escopo.

**Insight crítico:** Turnover não é causa, é sintoma.

### Camada 3: Ação | Gestão de Saída Baseada em Resultados

A questão não é evitar todas as saídas. A questão é gerir saída com estratégia: saber quem precisa de retenção, quem precisa de readequação e onde a saída pode acontecer sem prejudicar o negócio.

É gestão focada em impacto, não em achismos.

---

## Metodologia & Framework Técnico

Esta iniciativa utiliza uma abordagem híbrida combinando ciência de dados avançada com inteligência estratégica de negócios:

### Componentes Centrais

**Engenharia Comportamental**  
Desenvolvimento de indicadores sintéticos (ex.: Índice de Risco de Burnout, Score de Estagnação de Carreira) projetados para capturar dinâmicas organizacionais invisíveis em dados brutos.

**Modelagem Não-Linear**  
Implementação de algoritmos Random Forest para detectar interdependências complexas—como o impacto variável da remuneração através de diferentes estágios de carreira e segmentos demográficos.

**Arquitetura de IA Explicável**  
Integração de valores SHAP (SHapley Additive exPlanations) para garantir transparência do modelo, fornecendo insights acionáveis para Business Partners de RH em vez de previsões opacas.

**Performance Otimizada para Recall**  
Calibração do modelo prioriza a minimização de falsos negativos—sendo o resultado mais custoso a não-detecção de evasão de talentos de alto valor.

---

## Indicadores Desenvolvidos

O modelo deriva seu poder preditivo de features construídas especificamente:

**Risk_Burnout**  
Composição ponderada de horas extras e frequência de viagens, isolando indivíduos operando sob cargas de trabalho insustentáveis.

**Index_Stagnation**  
Razão entre tempo no cargo atual e tempo total de organização, quantificando a velocidade percebida de carreira.

**Index_Manager_Stability**  
Duração sob liderança atual, mensurando efeitos da continuidade gerencial na retenção.

**Market_Pressure**  
Posicionamento inferido de remuneração relativo a benchmarks de mercado, ajustado por níveis de educação e experiência.

---

## Stack Tecnológico

**Ambiente:** Python 3.8+

**Bibliotecas:**
- Processamento de Dados: `pandas`, `numpy`
- Machine Learning: `scikit-learn` (RandomForestClassifier, StratifiedKFold)
- Interpretação do Modelo: `shap`
- Visualização: `matplotlib`, `seaborn`

### Instalação

```bash
pip install pandas numpy scikit-learn shap matplotlib seaborn
```

---

## Protocolo de Execução

1. Certifique-se de que `Base_RH.csv` está presente no diretório raiz
2. Execute `Turnover_Senior_Analytics.ipynb`
3. O pipeline automatizado irá:
   - Validar integridade dos dados e executar procedimentos de limpeza
   - Gerar features engenheiradas
   - Treinar e validar cruzadamente o modelo
   - Calcular valores SHAP para interpretabilidade
4. **Entregável:** `HR_Retention_Priority_List.csv` contendo colaboradores ativos com probabilidade de desligamento superior a 60%, formatado para integração direta com PowerBI ou Excel (padrão brasileiro)

---

## Achados Estratégicos

O framework analítico validou três hipóteses críticas com implicações significativas de negócio:

### O Custo da Exaustão
Horas extras emergem como o principal driver de atrito. O ônus financeiro de compensar jornadas estendidas correlaciona-se diretamente com custos de reposição relacionados ao turnover.

**Validação empírica:** Turnover não é uma questão salarial isolada—é uma questão de sustentabilidade operacional.

### A Zona de Risco Júnior
A evasão concentra-se entre profissionais em início de carreira nas faixas salariais de entrada, indicando desalinhamento estrutural nas proposições de valor inicial.

### O Efeito da Estagnação
Colaboradores sem mobilidade lateral ou promoção por três ou mais anos demonstram risco exponencial de saída, sinalizando necessidade de revisão da arquitetura de carreira.

---

## Ações Recomendadas

### Intervenções Imediatas
**Entrevistas de Permanência:** RH deve utilizar a lista de prioridade para conduzir conversas estruturadas de retenção com talentos de alto risco identificados pelo modelo.

### Revisão de Políticas
**Gestão de Carga de Trabalho:** Reavaliar políticas de horas extras e requisitos de viagem para mitigar indicadores de burnout antes que se convertam em desligamentos.

**Arquitetura de Remuneração:** Avaliar posicionamento da compensação de entrada versus benchmarks de mercado, especialmente para perfis júnior.

### Operações Contínuas
**Recalibração do Modelo:** Implementar ciclos trimestrais de retreinamento para capturar dinâmicas de mercado e mudanças organizacionais em evolução.

**Monitoramento de Performance:** Estabelecer KPIs rastreando acurácia do modelo e efetividade das intervenções implementadas.

---

## Framework de Impacto de Negócio

Este sistema transiciona a retenção de talentos de centro de custo para capacidade estratégica:

- **Redução de Custos de Recrutamento:** Retenção proativa e direcionada diminui ciclos caros de substituição
- **Preservação de Conhecimento:** Minimiza perda de conhecimento institucional e relacionamentos críticos com clientes
- **Continuidade Operacional:** Reduz disrupção de projetos por desligamentos inesperados de perfis-chave
- **Planejamento Estratégico de Força de Trabalho:** Viabiliza sucessão baseada em dados e investimento focado em desenvolvimento de talentos

**Princípio orientador:** Gerir saída com estratégia, não evitar toda saída. Saber onde investir em retenção e onde permitir renovação natural da força de trabalho.

---

## Estrutura do Repositório

```
turnover-analysis/
│
├── notebook.ipynb    # Análise completa e pipeline de modelagem
├── Base_RH.csv                         # Dataset de entrada (não incluído no repositório)     # Output: lista priorizada de risco
├── requirements.txt                    # Dependências Python
└── README.md                           # Este documento
```

---

## Exploração Técnica Completa

Para acessar a análise exploratória detalhada, incluindo:
- Métricas de performance do modelo
- Lógica de segmentação por perfil de risco
- Fluxo analítico completo com interpretação de SHAP values
- Visualizações executivas e técnicas

Acesse o notebook completo no repositório GitHub.

---

## Documentação & Suporte

Para consultas técnicas, questionamentos sobre metodologia do modelo ou suporte de integração, contate a equipe de Data Science através dos canais estabelecidos.

**Versão:** 1.0  
**Última Atualização:** 2025