# Projeto de Conclusão da Disciplina "Big Data" do MBA em Data Science da Famesp em parceria com a FLAI
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

**Tema**: Títulos IMDb: Análise da Avaliação pelo Público e Sucesso do Título

**Objetivo**:  

- O objetivo deste projeto é analisar a avaliação de um título, seja um filme, uma série, um documentário, ou um vídeo game para entender quais variáveis possam indicar o quão bem esse título está sendo recebido pelo público ou não. Tudo isso utilizando tecnologias de Big Data, no caso, foi utilizado o PySpark para tratar os dados, gerar as análises e responder às perguntas. 

**Problema de Negócio**: 

- A indústria de entretenimentos como filmes, séries, documentários, jogos, assim como qualquer negócio, precisa lidar com a satisfação ou não do seu público, principalmente para planejamento de projetos futuros e levantamento de orçamento, patrocinadores, entre outros. 
- O Internet Movie Database (IMDb), um dos sites mais acessados no mundo, abriga a maior coleção digital de metadados sobre filmes, séries de TV, documentários, vídeo games, entre outras produções. Semelhante à Wikipedia, o conteúdo do site do IMDb é atualizado por usuários não remunerados. Além de aceitar informações fornecidas pelos usuários, o IMDb também permite que os usuários expressem sua opinião sobre a qualidade dos títulos por meio de avaliações, cuja escala varia de 1 (péssimo) a 10 (o melhor).
- Pensando nisso, este projeto tem como intuito auxiliar nessa dor, não só de diretores, produtores, escritores, mas também de artistas de modo geral, que é entender e talvez prever a aceitação e satisfação do público em relação a uma produção, que normalmente requer um investimento na casa dos milhares de dólares.

**Fontes de Dados**:

- Foram utilizados dados de um conjunto de dados público localizado no site do IMDb. Os dados se referem a títulos de filmes, séries, documentários, vídeo games, entre outros, assim como dados de avaliação desses títulos. 
- Segue link do IMDb: https://datasets.imdbws.com/ [^1]
- Detalhes desse conjunto de dados: Ele contém muitos conjuntos de dados diferentes, que incluem dados reais. Cada conjunto de dados está contido em um arquivo comprimido (gzip) com valores separados por tabulação (TSV) no formato UTF-8. A primeira linha de cada arquivo contém cabeçalhos que descrevem o que há em cada coluna. '\N' é utilizado para indicar que um campo específico está ausente ou nulo.
- O conjunto de dados em questão é formado pelos arquivos abaixo (OBS: a lista abaixo consta apenas os arquivos utilizados neste projeto):
  - title.basics.tsv.gz: dados básicos dos títulos disponibilizados
  - title.ratings.tsv.gz: dados com avaliações por título 
  - title.akas.tsv.gz: dados regionais de cada título 
  - title.crew.tsv.gz: dados de diretores e escritores de cada título

**Link do Notebook**: https://github.com/adriana-takahagui/mba-big-data/blob/main/Titulos_IMDb_Big_Data.ipynb

---

## Dicionário de Variáveis

Esta seção descreve as tabelas e as variáveis utilizadas no projeto e no problema proposto.[^2]

**Descrição das variáveis com origem em: title.basics.tsv.gz**

| N | Variável       | Tipo do dado | Descrição                                                               | Valores Permitidos                                                                                     |
|:-:|----------------|:------------:|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------|
| 1 | tconst         |    String    | Identificador alfanumérico único do título                              | Não enumerado                                                                                          |
| 2 | titleType      |    String    | Tipo ou formato do título                                               | tvEpisode, movie, short, tvSeries, tvMovie, video, tvMiniSeries, videoGame, tvSpecial, tvShort         |
| 3 | primaryTitle   |    String    | Título mais popular / Título utilizado nos materiais promocionais       | Não enumerado                                                                                          |
| 4 | originalTitle  |    String    | Título original no idioma original                                      | Não enumerado                                                                                          |
| 5 | isAdult        |   Booleano   | Indicador se o filme possui conteúdo adulto ou não                      | 0 - Não adulto; 1 - Adulto                                                                             |
| 6 | startYear      |    Inteiro   | Ano de lançamento do título. No caso de "TV Series", é o ano de estréia | Ano no formato de 4 dígitos                                                                            |
| 7 | endYear        |    Inteiro   | Ano de conclusão da "TV Series"                                         | Para "TV Series", contém o ano de conclusão no formato de 4 dígitos. Para os demais tipos, contém '\N' |
| 8 | runtimeMinutes |    Inteiro   | Duração do título (em minutos)                                          | Não enumerado                                                                                          |
| 9 | genres         |     Array    | Lista de Gênero(s) associado(s) ao título                               | Não enumerado. Contém até 3 gêneros por título                                                         |

**Descrição das variáveis com origem em: title.ratings.tsv.gz**

| N | Variável      | Tipo do dado | Descrição                                                       | Valores Permitidos |
|:-:|---------------|:------------:|-----------------------------------------------------------------|--------------------|
| 1 | tconst        |    String    | Identificados alfanumérico único do título                      | Não enumerado      |
| 2 | averageRating |    Decimal   | Média ponderada de todas as avaliações individuais dos usuários | Não enumerado      |
| 3 | numVotes      |    Inteiro   | Número de votos que o título recebeu                            | Não enumerado      |

**Descrição das variáveis com origem em: title.akas.tsv.gz**

| N | Variável        | Tipo do dado | Descrição                                                       | Valores Permitidos                                                                                                                                                   |
|:-:|-----------------|:------------:|-----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1 | titleId         |    String    | Identificador alfanumérico único do título                      | Não enumerado                                                                                                                                                        |
| 2 | ordering        |    Inteiro   | Número que identifica unicamente as linhas para um dado titleId | Não enumerado                                                                                                                                                        |
| 3 | title           |    String    | Nome local do título                                            | Não enumerado                                                                                                                                                        |
| 4 | region          |    String    | Região da versão do título                                      | Não enumerado                                                                                                                                                        |
| 5 | language        |    String    | Idioma do título                                                | Não enumerado                                                                                                                                                        |
| 6 | types           |     Array    | Conjunto enumerável de atributos alternativos para o título     | Algumas possibilidades: "alternative", "dvd", "festival", "tv", "video", "working", "original", "imdbDisplay". Novos itens podem ser adicionados no futuro sem aviso |
| 7 | attributes      |     Array    | Termos adicionais para descrever o título de forma alternativa  | Não enumerado                                                                                                                                                        |
| 8 | isOriginalTitle |   Booleano   | Indicador se o título é um título original                      | 0 - título não original; 1 - título original                                                                                                                         |

**Descrição das variáveis com origem em: title.crew.tsv.gz**

| N | Variável  | Tipo do dado | Descrição                                                                  | Valores Permitidos |
|:-:|-----------|:------------:|----------------------------------------------------------------------------|--------------------|
| 1 | tconst    |    String    | Identificados alfanumérico único do título                                 | Não enumerado      |
| 2 | directors |     Array    | Lista de Diretor(es) associado(s) ao título (formado pela chave 'nconst')  | Não enumerado      |
| 3 | writers   |     Array    | Lista de Escritor(es) associado(s) ao título (formado pela chave 'nconst') | Não enumerado      |

---

## Metodologia de Desenvolvimento

**1. Entendimento do negócio** <br/>
**Qual a necessidade ou dor do negócio a ser explorada na análise?**
- Como qualquer negócio, a indústria de entretenimento como a produção de filmes, séries de TV, documentários, vídeo games, entre outros, precisa realizar planejamentos de orçamento e uma das variáveis que pode ser explorada nesse contexto para ter uma ideia se uma produção em específico vai ser bem aceita pelo público ou não é a avaliação do próprio público. 
- Portanto, o principal objetivo deste projeto é analisar quais variáveis influenciam a avaliação dada pelo usuário a um título, seja um filme, uma série de TV, ou qualquer produção disponível no IMDb como apresentado no item “Descrição do Problema de Negócio”. 

**2. Entendimento dos dados** <br/>
**Quais dados estão presentes / são necessários? Os dados estão disponíveis, preparados e tratados?**
- Foram utilizados dados disponibilizados pelo IMDb através do link: https://developer.imdb.com/non-commercial-datasets/. 
- Maiores informações foram apresentadas no item “Descrição do Problema de Negócio”. 
- Os dados já estão previamente preparados para uso. 

**3. Preparação dos dados** <br/>
**Como os dados foram tratados e preparados para a análise?**
- Como o dataset do IMDb é formado por várias tabelas, para o problema proposto, foram utilizadas apenas 04 tabelas e estas foram unidas em uma única tabela para facilitar as análises, assim como foram tratadas conforme a necessidade das análises. 
- Toda a preparação dos dados pode ser conferida no notebook, clicando [aqui](https://github.com/adriana-takahagui/mba-big-data/blob/main/Titulos_IMDb_Big_Data.ipynb). 

**4. Análises e Conclusão** <br/>
**Quais perguntas podem ser feitas para explorar os dados e responder o problema proposto? O que se pode concluir com as análises?**
- As análises foram realizadas para entender as variáveis que possam influenciar a avaliação dada pelo usuário. 
- Focou-se na análise do gênero, tipo do título (filme, série, ...), e criaram-se outras variáveis como quantidade de regiões, quantidade de gêneros, quantidade de diretores, quantidade de escritores e avaliou-se se eles influenciam ou não a nota dada a um título. 
- Toda a análise exploratória pode ser conferida no notebook, assim como a conclusão das análises, clicando [aqui](https://github.com/adriana-takahagui/mba-big-data/blob/main/Titulos_IMDb_Big_Data.ipynb). 

---

## Próximos Passos

- Criar um modelo de Machine Learning para prever notas (avaliações) e classificar filmes, séries e outras produções de acordo com essas avaliações para auxiliar a planejar novos projetos e levantar orçamento.
- Adicionar outros conjuntos de dados relacionados ao tema para explorar como as demais variáveis influenciam ou não as notas dadas pelo público.
- Como por exemplo, dados de bilheteria. Entender a correlação entre o faturamento de uma produção como filmes e a avaliação dada pelo público. 

---

## Fontes e Referências

[^1]: Fonte dos dados: https://datasets.imdbws.com/
[^2]: Fonte para o dicionário de variáveis: https://developer.imdb.com/non-commercial-datasets/

