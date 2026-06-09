# Análise de Sentimentos em Avaliações de E-commerce

Este projeto foi desenvolvido de forma colaborativa por uma equipe de 4 pessoas com o objetivo de aplicar técnicas avançadas de Processamento de Linguagem Natural (PLN) e Machine Learning em dados reais do varejo brasileiro.


## Objetivo do Projeto

O objetivo principal deste projeto é prever a satisfação de clientes de e-commerce (notas de 1 a 5 estrelas) baseando-se unicamente no texto de suas avaliações (título e mensagem). Desde o início, nosso foco principal foi implementar um modelo de Deep Learning robusto (Transformers), utilizando outras abordagens clássicas de PLN apenas como base de comparação (baselines).

## Ambiente e Infraestrutura

Todo o desenvolvimento, treinamento e processamento dos dados foi realizado na nuvem utilizando o Google Colab.
Para viabilizar e acelerar o processamento do nosso modelo principal (que exige alto poder computacional), utilizamos a aceleração de hardware via GPU T4 disponibilizada pelo Colab. Isso reduziu drasticamente o tempo de inferência nas milhares de avaliações da base.

## Preparação dos Dados

Dados reais da internet são ruidosos, cheios de gírias e ironias. Para que a Inteligência Artificial não fosse "enganada" pelos clientes, nós criamos um motor de regras customizadas que roda junto com os modelos:

- Limpeza e Padronização: Remoção de avaliações vazias, conversão para minúsculas e tratamento de espaçamentos.

- Tradução de "Internetês": Criação de um dicionário para expandir abreviações comuns no Brasil (ex: vc, pq, blz, fdp).

- Listas de Palavras Boas e Ruins: Mapeamos termos chaves de alta polaridade (ex: perfeito, amei vs lixo, quebrado). A inclusão dessa lista aumentou significativamente a performance do nosso modelo principal!

- Detecção de Sarcasmo: Criamos regras que cruzam "risadas" (kkk, rsrs) com palavras negativas para identificar ironia (ex: "kkkk péssimo produto"), forçando a nota para baixo.

- Níveis de Penalização (Confiança): Implementamos uma lógica de ajuste fino onde, se o modelo estivesse inseguro (baixa confiança estatística na previsão), a nota era "penalizada" ou puxada para o centro (neutro), evitando extremos errados.

## Modelos Utilizados

Para extrair o sentimento dos textos, padronizamos a saída de todos os algoritmos para a escala real do negócio (1 a 5 estrelas) e estruturamos a seguinte arquitetura:

1- Transformers (Nosso Modelo Principal): Utilizamos o modelo de Deep Learning pysentimiento/robertuito-sentiment-analysis via HuggingFace. Ele foi treinado especificamente para redes sociais em idiomas latinos. Impulsionado pela GPU T4 e calibrado com nossas regras de palavras e sarcasmo, este foi o núcleo do nosso projeto.

2- VADER / LeIA (Modelo de Comparação 1): Utilizamos o repositório LeIA, uma adaptação do VADER para o português. É um modelo léxico de regras que avalia a intensidade das palavras (compound).

3- TextBlob (Modelo de Comparação 2): Uma biblioteca clássica baseada em léxico inglês. O texto do cliente era traduzido via API para o inglês, analisado, e a polaridade mapeada para as 5 estrelas.

## Resultados e Análises

O Transformers superou de forma brilhante os demais modelos. Enquanto o TextBlob sofria com nuances de tradução e o LeIA esbarrava em contextos mais complexos, o Transformer (auxiliado pelas nossas listas de palavras positivas/negativas) conseguiu capturar a essência do consumidor brasileiro com muita precisão.

Para comprovar e documentar esses resultados, geramos as seguintes análises visuais:

- Distribuição de Notas (Gráficos de Barras): Para verificar se a IA acompanhava a curva de distribuição real do cliente.

- Matrizes de Correlação (Pearson e Spearman): Para medir matematicamente o alinhamento entre a nota real e a calculada.

- Matrizes de Confusão: Fundamentais para analisar não apenas o quanto o Transformer acertou, mas como ele errou, validando que nossos erros residuais eram aceitáveis (ex: prever 4 quando a nota era 5) e não críticos.

## Como Executar o Projeto

1- Clone este repositório.

2- Suba o notebook (.ipynb) no Google Colab.

3- Ative a Aceleração por Hardware: Ambiente de Execução > Alterar tipo de ambiente de execução > GPU T4.

4- Instale as bibliotecas necessárias listadas no início do notebook (transformers, textblob, etc.).

5- Execute as células sequencialmente para ver a limpeza, as regras heurísticas e a geração dos gráficos de comparação.

Linguagens e Ferramentas: Python, Pandas, Scikit-Learn, Transformers (HuggingFace), Google Colab, GPU T4, Seaborn, Matplotlib.

