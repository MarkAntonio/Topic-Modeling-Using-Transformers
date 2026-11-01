# Topic Modeling Using Transformers

Projeto desenvolvido durante o minicurso "Topic Modeling Using Transformers", ministrado no JATI 2023 pelo Prof. Dr. Michael Cruz.

## Visão geral

Este repositório contém um notebook em Python para explorar a modelagem de tópicos em textos de avaliações de restaurantes. O objetivo principal é transformar um conjunto de reviews em representações numéricas, identificar temas recorrentes e visualizar esses tópicos de forma interpretável.

Embora o nome do repositório mencione "Transformers", a implementação prática realizada no notebook usa uma abordagem clássica e muito comum em processamento de linguagem natural: limpeza textual + tokenização + remoção de stopwords + lematização + modelagem de tópicos com LDA (Latent Dirichlet Allocation) via Gensim, acompanhada de visualização com pyLDAvis.

Em outras palavras, o projeto mostra um fluxo completo de topic modeling aplicado a reviews de restaurantes, com foco em descoberta de padrões semânticos em textos do mundo real.

## Objetivo do projeto

O notebook busca responder perguntas como:

- Quais temas recorrentes aparecem nas avaliações?
- Existe uma estrutura temática clara nos comentários?
- Como transformar textos em uma representação útil para análise de tópicos?
- Como visualizar e interpretar tópicos gerados automaticamente?

A proposta é didática e prática: partir de dados reais, aplicar técnicas de pré-processamento e usar algoritmos probabilísticos para descobrir agrupamentos de palavras que representam tópicos coerentes.

## Base de dados

A base utilizada é um dataset de avaliações de restaurante em formato TSV, com duas colunas principais:

- Review: texto da avaliação
- Liked: rótulo binário indicando se a avaliação foi positiva ou negativa

A estrutura do arquivo mostra exemplos como:

- "Wow... Loved this place."
- "Crust is not good."
- "Not tasty and the texture was just nasty."

O conjunto possui cerca de 1.000 registros, sendo adequado para um estudo introdutório em processamento de linguagem natural e mineração de tópicos.

## Bibliotecas e ferramentas utilizadas

O notebook utiliza um conjunto de bibliotecas bastante relevante para NLP e análise de tópicos:

- Python
- pandas: manipulação e leitura do dataset
- re: limpeza e normalização textual
- nltk
  - stopwords
  - word_tokenize
- spaCy: lematização e processamento linguístico avançado
- unidecode: remoção/normalização de caracteres acentuados
- Gensim: criação de dicionário, corpus e modelagem de tópicos com LDA
- pyLDAvis: visualização interativa dos tópicos
- pickle: persistência de artefatos, quando necessário
- Google Colab / Google Drive: ambiente de execução e armazenamento do dataset

Além disso, o notebook também instala e usa o modelo spaCy `en_core_web_lg`, um modelo de língua inglesa com vetores de palavras e recursos linguísticos mais robustos.

## Fluxo do projeto

### 1. Importação e configuração inicial

O notebook inicia com a instalação de dependências e a importação das bibliotecas necessárias. Em ambiente Colab, isso inclui a montagem do Google Drive para acessar o dataset localmente.

### 2. Leitura do dataset

O arquivo CSV/TSV é carregado com pandas, e as avaliações são armazenadas em uma coluna chamada `Review`.

### 3. Limpeza textual

A limpeza dos textos inclui ações como:

- remoção de caracteres especiais
- conversão para minúsculo
- remoção de números
- normalização de espaços em branco
- eliminação de pontuação e outros elementos que não agregam semântica

O notebook define funções como:

- `remove_special_tokens(text)`
- `remove_space(text)`
- `remove_numbers(text)`

Essas etapas ajudam a reduzir ruído no texto e melhorar a qualidade dos tópicos extraídos.

### 4. Tokenização

Cada review é separada em tokens (palavras), convertendo o texto em uma sequência de termos úteis para análise.

A função `tokenize_text(text)` faz essa transformação usando `nltk.tokenize.word_tokenize`.

### 5. Remoção de stopwords

Palavras muito frequentes e pouco informativas, como "the", "is", "and", "a", "of", etc., são removidas. Isso reduz o peso de termos irrelevantes e permite que os tópicos reflitam melhor os assuntos principais.

A função `remove_stop_words(example_sent)` realiza essa etapa com base no conjunto de stopwords do NLTK.

### 6. Lematização

A lematização reduz palavras para sua forma base ou lemma, agrupando variações como:

- "eating", "ate", "eaten" -> "eat"
- "friends", "friend" -> "friend"

No notebook, isso é feito com o auxílio de spaCy via `nlp(doc)` e `token.lemma_`.

Essa etapa ajuda a unificar termos semânticamente semelhantes e aumentar a coerência dos tópicos.

### 7. Construção do corpus para Gensim

Após a limpeza e normalização, os textos são convertidos em uma representação adequada para modelagem de tópicos.

O Gensim utiliza:

- `Dictionary`: mapeia palavras para identificadores numéricos
- `corpus`: representação bag-of-words dos documentos

Essa etapa é fundamental para que o algoritmo LDA receba entradas numéricas e descubra tópicos latentes.

### 8. Modelagem de tópicos com LDA

O modelo LDA (Latent Dirichlet Allocation) é treinado sobre o corpus de textos. O LDA assume que cada documento é uma mistura de tópicos e que cada tópico é uma distribuição de palavras.

Dessa forma, os tópicos gerados tendem a capturar assuntos recorrentes como:

- qualidade da comida
- demora no atendimento
- custo-benefício
- sabor e textura
- ambiente e experiência geral

### 9. Visualização dos tópicos

Ao final, o projeto usa `pyLDAvis` para visualizar os tópicos de forma interativa, mostrando:

- termos mais relevantes por tópico
- distância entre tópicos
- distribuição de palavras em cada tema

Essa visualização facilita a interpretação dos resultados e ajuda a avaliar a qualidade do modelo.

## Técnicas principais aplicadas

Este notebook reúne várias técnicas importantes do campo de NLP e topic modeling:

- Pré-processamento de texto
- Normalização textual
- Remoção de ruído lexical
- Tokenização
- Stopword removal
- Lematização
- Representação bag-of-words
- Modelagem de tópicos por LDA
- Visualização de tópicos
- Exploração de padrões semânticos em textos de avaliações

## Observações importantes

- O notebook foi executado em ambiente Colab, o que explica o uso de `drive.mount()`.
- O nome do repositório menciona "Transformers", mas a solução implementada no notebook é baseada em técnicas clássicas de NLP e LDA.
- O modelo de linguagem spaCy `en_core_web_lg` pode exigir download inicial e consumo de memória, então o ambiente deve ter recursos suficientes.
- O projeto é ótimo como base pedagógica para aprender topic modeling e análise de textos em Python.

## Como executar

Recomenda-se abrir o notebook em Google Colab ou Jupyter Notebook e rodar as células na ordem.

Instalações típicas:

```bash
pip install pandas
pip install nltk
pip install spacy
pip install gensim
pip install pyLDAvis
pip install unidecode
python -m spacy download en_core_web_lg
```

Em seguida:

1. monte seu Google Drive (se estiver usando Colab)
2. carregue o dataset
3. execute as etapas de limpeza e tokenização
4. treine o modelo LDA
5. visualize os tópicos com pyLDAvis

## Conclusão

Este repositório ilustra, de maneira prática e didática, como aplicar técnicas de topic modeling em avaliações textuais. O projeto combina conceitos fundamentais de NLP com uma abordagem de modelagem probabilística para extrair temas ocultos do corpus.

É uma ótima referência para quem está começando a estudar:

- processamento de linguagem natural
- análise de texto
- mineração de opinião
- modelagem de tópicos
- visualização interpretável de modelos

## Créditos

- Projeto desenvolvido no minicurso "Topic Modeling Using Transformers"
- Ministrado por: Prof. Dr. Michael Cruz
- Evento: JATI 2023

## Repositório

Este notebook está disponível em:

- GitHub: https://github.com/MarkAntonio/Topic-Modeling-Using-Transformers

Se quiser, posso também criar uma versão mais "profissional" deste README em inglês, ou transformar este README em uma documentação mais estruturada com seções como "Instalação", "Metodologia", "Resultados esperados" e "Conclusão".
