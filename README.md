# CineMatch: Sistema Inteligente de Recomendação de Filmes

## 💡 Introdução

**CineMatch** é um sistema de recomendação de filmes desenvolvido com técnicas de **Machine Learning** e **Ciência de Dados**.  
Em um cenário onde o catálogo das plataformas de streaming cresce constantemente, encontrar algo que combine com o seu gosto pode ser um desafio. Este projeto busca **facilitar a descoberta de novos títulos** por meio de algoritmos inteligentes que aprendem com as preferências do usuário.

Além da modelagem, o sistema foi integrado a uma **interface interativa**, proporcionando uma experiência prática e intuitiva para qualquer usuário, mesmo sem conhecimentos técnicos.

---

## 🧠 Por que usar sistemas de recomendação?

Com milhares de filmes disponíveis, o tempo que o usuário leva para escolher o que assistir pode ser longo. Os **sistemas de recomendação reduzem essa fricção**, aprendendo sobre os gostos do usuário com base em escolhas anteriores ou informações contextuais dos filmes.

Esses sistemas são **usados extensivamente por plataformas como Netflix, Amazon Prime, e Spotify**, e aplicá-los nesse projeto ajuda a entender na prática como **algoritmos inteligentes ajudam a melhorar a experiência do usuário**.

---

## 🗂️ Fonte dos Dados

Este projeto utiliza o dataset **"The Movies Dataset"**, disponível publicamente no Kaggle, com mais de **1 milhão de registros** de filmes da **The Movie Database (TMDB)**.

📍 A base pode ser acessada aqui:  
🔗 [TMDB - The Movies Dataset no Kaggle](https://www.kaggle.com/datasets/asaniczka/tmdb-movies-dataset-2023-930k-movies)

Após o download, os dados passaram por **limpeza e transformação**, com foco nas colunas mais relevantes para análise textual e construção dos perfis de conteúdo.

---

## 🔍 Escolha das Features

Para construir o perfil de um filme e encontrar os mais semelhantes entre si, foram combinadas colunas que representam **conteúdo descritivo** do filme:

```python
features = ['genres', 'overview', 'tagline', 'production_companies', 'keywords']
```

Essas colunas foram escolhidas por carregarem **informações sobre o tema, estilo, tom e enredo dos filmes**.  
Por exemplo:

- `genres`: drama, ação, comédia etc.
- `overview` e `tagline`: resumo da história
- `production_companies`: estúdios influenciam o estilo e produção
- `keywords`: temas centrais do filme

Ao combinar essas colunas em uma única string para cada filme, conseguimos gerar um **perfil textual unificado** que resume bem o conteúdo.

---

## 🧾 Vetorização com TF-IDF

Para transformar o conteúdo textual em algo que o algoritmo consiga entender, utilizamos a técnica de **TF-IDF (Term Frequency-Inverse Document Frequency)**.  

Essa técnica converte o texto em um vetor numérico, onde cada termo tem um peso calculado com base na sua frequência em um filme e na raridade no conjunto todo. Ou seja:

- Palavras muito comuns em todos os filmes recebem **menos peso**
- Palavras específicas de um filme recebem **mais peso**

Esse processo cria uma **representação vetorial única para cada filme**, refletindo sua identidade textual.

---

## 📐 Similaridade do Cosseno

Após vetorização, precisamos medir **quão parecidos** dois filmes são com base nos seus vetores. Para isso, usamos a **Similaridade do Cosseno**.

### Por que Cosine Similarity?

- Ela mede o **ângulo** entre dois vetores, e não a diferença absoluta (como distância Euclidiana).
- Ideal para **dados textuais**, onde a quantidade de palavras pode variar.
- Resulta em um valor entre **0 e 1**, onde 1 significa que os filmes são muito similares.

---

## 🤖 Tipos de Recomendação

### 1. Filtragem baseada em conteúdo (*Content-Based Filtering*)

Recomenda filmes com base em **características do conteúdo** que o usuário demonstrou interesse.  
Por exemplo: se alguém gosta de um filme de ação com viagem no tempo, o sistema busca filmes com temas e palavras semelhantes.

> ✅ Vantagem: personalização baseada no conteúdo real do filme  
> ⚠️ Limitação: depende da qualidade das informações textuais

---

### 2. Recomendação baseada em popularidade (*Popularity-Based*)

Sugere os filmes mais **bem avaliados ou assistidos** por todos os usuários, independentemente do perfil individual.

> ✅ Vantagem: simples e confiável para novos usuários (*cold start*)  
> ⚠️ Limitação: não considera gostos específicos

---

## ⚙️ Pipeline do Modelo

A seguir, o passo a passo do funcionamento do sistema:

1. 📥 **Carregamento dos dados**  
2. 🧩 **Seleção e concatenação das colunas descritivas**  
3. 🧹 **Limpeza e tratamento de valores nulos**  
4. 📊 **Vetorização dos textos com TF-IDF**  
5. 📐 **Cálculo da similaridade com Cosine Similarity**  
6. 🔎 **Busca por correspondência com o input do usuário**  
7. 🎯 **Retorno dos filmes mais semelhantes como recomendação**

---

## 🧪 Como o sistema entende qual é o “melhor” filme?

O sistema parte de um filme informado pelo usuário e calcula a **similaridade com todos os outros**.  
Em seguida, retorna uma **lista ordenada por proximidade vetorial**, ou seja, pelos filmes mais parecidos com o escolhido.

Esse resultado é interpretado como:  
> *“Se você gostou deste filme, provavelmente vai gostar desses outros com conteúdo semelhante.”*

Para abordagens populares, o sistema retorna filmes com **maior nota média (`vote_average`) e mais votos (`vote_count`)**.

---

## 🚀 Próximos passos

- Incluir recomendações personalizadas com base em histórico do usuário (modelo colaborativo)
- Implementar sistema híbrido com pesos ajustáveis entre conteúdo e popularidade
- Adicionar imagens dos pôsteres e trailers na interface com Streamlit
- Deploy na nuvem com link público para acesso rápido

---

Desenvolvido por **Arthur Sehnem**
