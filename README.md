# An-lise-Estat-stica-de-Vendas-e-Engenharia-de-Atributos-para-E-commerce
Pipeline em Python para simulação estocástica de dados de e-commerce e aplicação prática de engenharia de atributos (Feature Engineering) e análise de dados com Pandas e NumPy.

Este projeto foi desenvolvido com o objetivo de simular, processar e analisar dados de transações diárias de uma plataforma de e-commerce em crescimento. O foco principal está na aplicação prática de **Engenharia de Atributos**, estruturação de pipelines de dados com **Pandas** e **NumPy**, e na transformação de dados brutos em insights estratégicos de negócios (Data-Driven Decisions).

## 📌 O Problema de Negócio

Em cenários reais de e-commerce, grandes volumes de transações são gerados a cada segundo. No entanto, dados brutos isolados não trazem valor preditivo ou operacional direto. O desafio deste projeto consistiu em estruturar um ambiente de dados que permitisse solucionar problemas comuns de gestão, tais como:
* **Gestão de Estoque Ineficiente:** Falta de clareza sobre produtos de alta e baixa rotatividade ("campeões de venda" vs. itens obsoletos).
* **Decisões Baseadas em Intuição:** Ausência de métricas consolidadas sobre faturamento por categoria regional e comportamento temporal das vendas.
* **Logística Descentralizada:** Necessidade de segmentar e identificar gargalos na velocidade de distribuição por estados.

---

## 🛠️ Tecnologias e Ferramentas Utilizadas

* **Python 3.10+**: Linguagem base para o desenvolvimento de toda a lógica de programação.
* **Pandas**: Manipulação avançada de DataFrames, limpeza, indexação temporal e agregações complexas (`groupby`, `crosstab`).
* **NumPy**: Geração de distribuições numéricas aleatórias, matrizes e aplicação de lógica condicional vetorizada (`np.random`, `np.where`).
* **Matplotlib & Seaborn**: Construção de visualizações gráficas de alta fidelidade com customização de eixos (ex: formatação monetária dinâmica usando `FuncFormatter`).
* **Watermark**: Utilizado para garantir a reprodutibilidade do projeto, documentando as versões exatas de cada biblioteca.

---

## 🧠 Raciocínio Lógico e Arquitetura do Projeto

O projeto foi dividido em etapas modulares, simulando o ciclo de vida real de um projeto de análise de dados:

┌──────────────────────────┐     ┌──────────────────────────┐     ┌──────────────────────────┐
│  Geração Estocástica     │ ──> │   Pré-Processamento &    │ ──> │  Engenharia de Atributos │
│  de Dados (NumPy/Random) │     │   Exploração Avançada    │     │   (Criação de Variáveis) │
└──────────────────────────┘     └──────────────────────────┘     └──────────────────────────┘
│
▼
┌──────────────────────────┐     ┌──────────────────────────┐     ┌──────────────────────────┐
│ Insights de Negócio e    │ <── │ Visualizações de Dados   │ <── │ Agregações e Métricas    │
│ Próximos Passos (Ação)   │     │ (Plots Customizados)     │     │ Grupos (Pandas GroupBy)  │
└──────────────────────────┘     └──────────────────────────┘     └──────────────────────────┘

### 1. Modelagem Dinâmica de Dados (Data Synthesis)
Para refletir um ambiente real, foi criada a função `gera_dados_ficticios()`. A lógica foi construída para evitar dados perfeitamente uniformes, inserindo regras de negócios estocásticas:
* **Flutuação de Preço e Descontos:** Implementação de ruído estatístico uniforme (`np.random.uniform(0.9, 1.0)`) simulando políticas de desconto dinâmico de até 10% exclusivas para categorias específicas (Acessórios: Mouse Vertical e Teclado Mecânico).
* **Indexação Temporal:** Geração através de incrementos controlados combinada com distribíveis discretas de quantidades vendidas por pedido (`np.random.randint`).

### 2. Engenharia de Atributos (Feature Engineering)
A transformação de dados brutos em novos atributos foi crucial para responder às perguntas de negócio:
* **Métrica de Faturamento:** Criação da feature `Faturamento` através da multiplicação vetorizada (`Preco_Unitario * Quantidade`). Essa abordagem garante eficiência computacional ao utilizar as otimizações em baixo nível do Pandas, evitando loops iterativos manuais (`for`) altamente ineficientes.
* **Lógica de Segmentação Logística:** Aplicação de funções anônimas (`lambda`) estruturando a variável `Status_Entrega`. Pedidos destinados a `SP`, `RJ` e `MG` foram indexados como entrega **Rápida** devido à proximidade dos centros de distribuição (Malha Sudeste), enquanto os demais estados receberam status **Normal**.

---

## 🎓 Principais Aprendizados e Competências Desenvolvidas

A execução deste projeto proporcionou o amadurecimento de conceitos fundamentais em Ciência de Dados, englobando habilidades técnicas (hard skills) e analíticas (soft skills):

### 1. Manipulação Eficiente de Dados com Processamento Vetorizado
* **O Aprendizado:** No início do desenvolvimento de lógica condicional, a primeira intuição costuma ser o uso de laços `for` ou estruturas iterativas linha por linha. Durante o projeto, compreendi a importância e a enorme diferença de performance trazida pelas operações **vetorizadas** nativas do Pandas e NumPy. 
* **Aplicação Prática:** A criação da coluna de Faturamento e o tratamento de tipos com `pd.to_numeric` mostraram como alinhar o código para que o interpretador utilize otimizações escritas in C, reduzindo drasticamente o tempo de computação em conjuntos de dados massivos.

### 2. Tradução de Regras de Negócio em Algoritmos (Feature Engineering)
* **O Aprendizado:** Aprendi que os dados em seu estado original raramente estão prontos para gerar valor de mercado. A verdadeira inteligência analítica reside na capacidade de criar novos atributos a partir dos existentes.
* **Aplicação Prática:** Desenvolvi autonomia para correlacionar colunas distintas e mapear variáveis geográficas complexas (transformando siglas de Estados em categorias logísticas de entrega: *Rápida* vs. *Normal*), gerando indicadores acionáveis para tomadores de decisão em Cadeia de Suprimentos (Supply Chain).

### 3. Ciclo de Execução e Gerenciamento de Memória (Notebook Lifecycle)
* **O Aprendizado:** Trabalhar em ambientes baseados em células (como Jupyter Notebook ou Google Colab) exige um controle estrito sobre o ciclo de vida das variáveis e a ordem de execução do Kernel. Compreendi como erros comuns de `NameError` e inconsistências de mutabilidade ocorrem quando alteramos o estado do DataFrame sem re-executar as dependências anteriores.
* **Aplicação Prática:** Criação de blocos estruturados de teste com tratamento de exceções (`try/except`) para auditar ativamente os tipos de dados (`dtypes`) e a presença das colunas esperadas em tempo de execução.

### 4. Pensamento Crítico focado na Integridade Analítica
* **O Aprendizado:** Compreensão profunda do impacto que os arredondamentos numéricos (`round()`) causam na modelagem de dados. Percebi que para visualizações o formato string (`.2f`) é ideal, mas para o pipeline de análise, manter a precisão flutuante protege o faturamento de distorções estatísticas acumuladas ao efetuar somas globais.

---

## 📊 Estrutura das Análises Práticas

O repositório contém análises detalhadas orientadas a responder perguntas estratégicas:

1.  **Top 10 Produtos Mais Vendidos:** Identificação do volume de escoamento de mercadorias para otimização de estoque.
2.  **Análise de Faturamento Mensal:** Avaliação da linha de tendência temporal do faturamento para identificar sazonalidades.
3.  **Distribuição Geográfica (Vendas Por Estado):** Mapeamento de calor comercial para identificar quais regiões demandam maior foco de marketing.
4.  **Análise de Margem por Categoria (Faturamento Por Categoria):** Visão macro do portfólio de produtos (Eletrônicos, Hardware, Acessórios, Móveis).

---

## 🚀 Link para Executar o Projeto:

https://colab.research.google.com/github/Paulocgarcia/analise-estatistica-vendas-ecommerce/blob/main/AnaliseDeVendasParaLojaE-commerce.ipynb
   
👨‍💻 Autor
Desenvolvido por Paulo Garcia. Sinta-se à vontade para entrar em contato, propor melhorias no código ou deixar uma estrela (⭐) se este projeto foi útil para os seus estudos!   
