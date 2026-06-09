# Análise de Sentimentos em Avaliações de E-commerce

Este projeto foi desenvolvido de forma colaborativa por uma equipe de 4 pessoas com o objetivo de aplicar técnicas avançadas de Processamento de Linguagem Natural (PLN) e Machine Learning em dados reais do varejo brasileiro.


## Objetivo do Projeto

O objetivo principal deste projeto é prever a satisfação de clientes de e-commerce (notas de 1 a 5 estrelas) baseando-se unicamente no texto de suas avaliações (título e mensagem). Desde o início, nosso foco principal foi implementar um modelo de Deep Learning robusto (Transformers), utilizando outras abordagens clássicas de PLN apenas como base de comparação (baselines).

## Ambiente e Infraestrutura

Todo o desenvolvimento, treinamento e processamento dos dados foi realizado na nuvem utilizando o Google Colab.
Para viabilizar e acelerar o processamento do nosso modelo principal (que exige alto poder computacional), utilizamos a aceleração de hardware via GPU T4 disponibilizada pelo Colab. Isso reduziu drasticamente o tempo de inferência nas milhares de avaliações da base.

## Preparação dos Dados

Dados reais da internet são ruidosos, cheios de gírias e ironias. Para que a Inteligência Artificial não fosse "enganada" pelos clientes, nós criamos um motor de regras customizadas que roda junto com os modelos:

    Limpeza e Padronização: Remoção de avaliações vazias, conversão para minúsculas e tratamento de espaçamentos.

    Tradução de "Internetês": Criação de um dicionário para expandir abreviações comuns no Brasil (ex: vc, pq, blz, fdp).

    Listas de Palavras Boas e Ruins: Mapeamos termos chaves de alta polaridade (ex: perfeito, amei vs lixo, quebrado). A inclusão dessa lista aumentou significativamente a performance do nosso modelo principal!

    Detecção de Sarcasmo: Criamos regras que cruzam "risadas" (kkk, rsrs) com palavras negativas para identificar ironia (ex: "kkkk péssimo produto"), forçando a nota para baixo.

    Níveis de Penalização (Confiança): Implementamos uma lógica de ajuste fino onde, se o modelo estivesse inseguro (baixa confiança estatística na previsão), a nota era "penalizada" ou puxada para o centro (neutro), evitando extremos errados.


  

