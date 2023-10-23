# Projeto de Conclusão da Disciplina "Big Data" do MBA em Data Science
<p align="right">Outubro/2023</p>

---

## Índice

<!--ts-->
  * [Descrição do Projeto](https://github.com/adriana-takahagui/mba-big-data#descrição-do-projeto)
  * [Descrição do Problema de Negócio](https://github.com/adriana-takahagui/mba-big-data#descrição-do-problema-de-negócio)
  * [Dicionário de Variáveis](https://github.com/adriana-takahagui/mba-big-data#dicionário-de-variáveis)
  * [Metodologia de Desenvolvimento](https://github.com/adriana-takahagui/mba-big-data#metodologia-de-desenvolvimento)
  * [Próximos Passos](https://github.com/adriana-takahagui/mba-big-data#próximos-passos)
  * [Fontes e Referências](https://github.com/adriana-takahagui/mba-big-data#fontes-e-referências)
<!--te-->

---

## Descrição do Projeto

**Disciplina**: Big Data

**Requisitos**:

- [X] Processar e analisar dados utilizando tecnologias de Big Data.
- [X] Com base nos dados de sua escolha, elabore um desenho claro de qual o problema de negócio e como a sua solução analítica resolve o problema.
- [X] Responder cada uma das questões abaixo e entregar as respostas juntamente com o notebook, contendo o código da análise executada.
  - Descreva o problema ou a dor de negócio que você quer explorar na sua análise.
  - Quais dados você tem disponível para a análise?
  - Que hipóteses você pretende validar?
  - O que você pode concluir de cada uma das análises?
- [ ] [Opcional] Caso opte por construir uma solução de Machine Learning utilizando PySpark, seguem mais algumas perguntas para auxiliar:
  - Como o modelo será utilizado pelo negócio?
  - Como você avaliou a eficácia do seu modelo?
  - Como você avaliará os benefícios do modelo depois que ele for implantado?

---

## Descrição do Problema de Negócio

Esta seção aborda a descrição do problema de negócio escolhido para desenvolver o projeto da disciplina "Big Data".

**Tema**: Títulos IMDB: Análise de Avaliação pelo Público 

**Objetivo**:  

- O objetivo deste projeto é analisar a avaliação de um título, seja um filme, uma série, um documentário, ou um vídeo game para entender o quão bem esse título está sendo recebido pelo público ou não. Tudo isso utilizando tecnologias de Big Data, no caso, foi utilizado o PySpark para conectar e tratar os dados, gerar as análises e responder às perguntas. 

**Problema de Negócio**: 

- A indústria de entretenimentos como filmes, séries, documentários, jogos, assim como qualquer empresa, precisa lidar com a satisfação ou não do seu público, principalmente para planejamento de projetos futuros e levantamento de orçamento, patrocinadores, entre outros. 
- Pensando nisso, este projeto tem como intuito auxiliar nessa dor, não só de diretores, produtores, mas também de artistas de modo geral, que é entender e talvez prever a aceitação e satisfação do público em relação a uma produção, que normalmente requer um investimento na casa dos milhares de dólares. 

**Fontes de Dados**:

- Foram utilizados dados de um conjunto de dados público localizado no site do IMDB. Os dados se referem a títulos de filmes, séries, documentários, vídeo games, entre outros, assim como dados de avaliação desses títulos. 
- Segue link do IMDB: https://datasets.imdbws.com/ [^1]
- O conjunto de dados em questão é formado pelos arquivos abaixo (OBS: a lista abaixo consta apenas os arquivos utilizados neste projeto): 
  - title.basics.tsv.gz: dados básicos dos títulos disponibilizados
  - title.ratings.tsv.gz: dados com avaliações por título
  - title.akas.tsv.gz: dados regionais de cada título 

**Link do Notebook**: 

---

## Dicionário de Variáveis

Esta seção descreve as tabelas e as variáveis utilizadas no projeto e no problema proposto.[^2]

**Descrição das variáveis com origem em: title.basics.tsv.gz**

| N | Variável       | Tipo do dado | Descrição PT                                                            | Valores Permitidos                                                                                     |
|:-:|----------------|:------------:|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| 1 | tconst         |    String    | Identificador alfanumérico único do título                              | Não enumerado                                                                                          |
| 2 | titleType      |    String    | Tipo ou formato do título                                               | tvEpisode, movie, short, tvSeries, tvMovie, video, tvMiniSeries, videoGame, tvSpecial, tvShort         |
| 3 | primaryTitle   |    String    | Título mais popular / Título utilizado nos materiais promocionais       | Não enumerado                                                                                          |
| 4 | originalTitle  |    String    | Título original no idioma original                                      | Não enumerado                                                                                          |
| 5 | isAdult        |   Booleano   | Indicador se o filme possui conteúdo adulto ou não                      | 0 - Não adulto; 1 - Adulto                                                                             |
| 6 | startYear      |    Inteiro   | Ano de lançamento do título. No caso de "TV Series", é o ano de estréia | Ano no formato de 4 dígitos                                                                            |
| 7 | endYear        |    Inteiro   | Ano de conclusão da "TV Series"                                         | Para "TV Series", contém o ano de conclusão no formato de 4 dígitos. Para os demais tipos, contém '\N' |
| 8 | runtimeMinutes |    Inteiro   | Duração do título (em minutos)                                          | Não enumerado                                                                                          |
| 9 | genres         |     Array    | Gêneros associados ao título                                            | Não enumerado. Contém até 3 gêneros por título                                                         |

**Descrição das variáveis com origem em: title.ratings.tsv.gz**

| N | Variável      | Tipo do dado | Descrição PT                                                    | Valores Permitidos |
|:-:|---------------|:------------:|-----------------------------------------------------------------|--------------------|
| 1 | tconst        |    String    | Identificados alfanumérico único do título                      | Não enumerado      |
| 2 | averageRating |    Decimal   | Média ponderada de todas as avaliações individuais dos usuários | Não enumerado      |
| 3 | numVotes      |    Inteiro   | Número de votos que o título recebeu                            | Não enumerado      |

**Descrição das variáveis com origem em: title.akas.tsv.gz**

| N | Variável        | Tipo do dado | Descrição PT                                                    | Valores Permitidos                                                                                                                                                   |
|:-:|-----------------|:------------:|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 | titleId         |    String    | Identificador alfanumérico único do título                      | Não enumerado                                                                                                                                                        |
| 2 | ordering        |    Inteiro   | Númeor que identifica unicamente as linhas para um dado titleId | Não enumerado                                                                                                                                                        |
| 3 | title           |    String    | Nome local do título                                            | Não enumerado                                                                                                                                                        |
| 4 | region          |    String    | Região da versão do título                                      | Não enumerado                                                                                                                                                        |
| 5 | language        |    String    | Idioma do título                                                | Não enumerado                                                                                                                                                        |
| 6 | types           |     Array    | Conjunto enumerável de atributos alternativos para o título     | Algumas possibilidades: "alternative", "dvd", "festival", "tv", "video", "working", "original", "imdbDisplay". Novos itens podem ser adicionados no futuro sem aviso |
| 7 | attributes      |     Array    | Termos adicionais para descrever o título de forma alternativa  | Não enumerado                                                                                                                                                        |
| 8 | isOriginalTitle |   Booleano   | Indicador se o título é um título original                      | 0 - título não original; 1 - título original                                                                                                                         |

---

## Metodologia de Desenvolvimento


---

## Próximos Passos

- Criar um modelo de Machine Learning para prever notas (avaliações) e classificar filmes, séries e outras produções de acordo com essas avaliações para auxiliar a planejar novos projetos e levantar orçamento.
- Adicionar outros conjuntos de dados relacionados para explorar como as demais variáveis influenciam ou não as notas dadas pelo público.

---

## Fontes e Referências

[^1]: Fonte dos dados: https://datasets.imdbws.com/
[^2]: Fonte para o dicionário de variáveis: https://developer.imdb.com/non-commercial-datasets/

