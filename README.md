# Anlise de Sentimentos em Avaliações de Ecommerce

Este projeto foi desenvolvido de forma colaborativa por uma equipe de 4 pessoas com o objetivo de aplicar técnicas de Processamento de Linguagem Natural (PLN) e Machine Learning em dados reais.

## Objetivo do Projeto

O objetivo principal deste projeto é prever a satisfação de clientes de e-commerce (notas de 1 a 5 estrelas) baseando-se unicamente no texto de suas avaliações (título e mensagem). Para isso, comparamos diferentes abordagens de Processamento de Linguagem Natural (PLN) para entender qual se adapta melhor às nuances do vocabulário brasileiro na internet.

## Limpeza e Engenharia de Atributos (Data Prep)

- Dados reais da internet são ruidosos. Grande parte do nosso esforço foi em tratar esses textos antes de passá-los para a Inteligência Artificial. As principais decisões de tratamento foram:

- Tratamento de Nulos: Remoção de avaliações que não possuíam nota ou que estavam com título e mensagem completamente vazios.

- Padronização: Conversão de todos os textos para minúsculas e remoção de quebras de linha/espaços duplos.

- Tradução de "Internetês": Criação de um dicionário customizado para traduzir abreviações comuns no Brasil (ex: vc, pq, blz, mto, fdp) para suas palavras completas, ajudando os modelos léxicos a entenderem o contexto.

- Detecção de Sarcasmo e Emojis: Implementamos regras de negócio onde a contagem de emojis positivos/negativos e a presença de sarcasmo (ex: "kkkk péssimo") têm peso decisivo na nota final.


## Modelos Utilizados

Para extrair o sentimento dos textos, decidimos testar e comparar 3 abordagens diferentes. Decisão arquitetural: Padronizamos a saída de todos os modelos para a escala real do negócio (1 a 5 estrelas), facilitando a comparação direta.

1- Transformers (RoBERTuito - HuggingFace): Utilização de um modelo de Deep Learning (pysentimiento/robertuito-sentiment-analysis) treinado especificamente para análise de sentimentos em redes sociais em idiomas latinos.

2- LeIA (Léxico Nativo PT-BR): Utilização do repositório LeIA (Lexicon for pt-br), uma adaptação do VADER para português. O modelo avalia a intensidade das palavras (compound) sem precisar de tradução, tornando-o rápido e eficiente. 

3- TextBlob (Tradução + API): Uma biblioteca clássica em inglês. O texto do cliente é traduzido via API para o inglês, a polaridade (-1.0 a 1.0) é calculada e mapeada para as 5 estrelas.

## Análises e Avaliação de Desempenho

Para avaliar qual modelo se saiu melhor e onde estavam errando, geramos as seguintes visualizações:

- Distribuição de Notas (Gráficos de Barras): Para comparar se a curva de notas gerada pela IA acompanhava a curva real de distribuição dos clientes.

- Matrizes de Correlação (Pearson e Spearman): Fundamentais para medir a relação entre a nota real e a nota calculada. Utilizamos Spearman com destaque, por ser ideal para dados ordinais (rankings de 1 a 5).

- Matrizes de Confusão: Analisamos não apenas o quanto o modelo errou, mas como errou. Consideramos aceitável um erro adjacente (o modelo prever 4 quando a nota era 5), mas focamos em mitigar os erros graves (o modelo prever 5 para um cliente que deu nota 1 por conta de ironias).


  ## Como Executar o Projeto

  1- Clone este repositório.

  2- Certifique-se de ter as bibliotecas instaladas (pandas, seaborn, matplotlib, transformers, textblob, scikit-learn).

  3- O repositório oficial do LeIA será clonado automaticamente pelo script.

  4- Execute os blocos do Jupyter Notebook na ordem para visualizar a limpeza, aplicação dos modelos e geração dos gráficos.

  Linguagens e Ferramentas: Python, Pandas, Scikit-Learn, Transformers (HuggingFace), Seaborn.

