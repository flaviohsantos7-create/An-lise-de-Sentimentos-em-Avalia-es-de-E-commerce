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

