# Regressão Linear
## Análise dos Dados
No arquivo `train.csv` possui 588091 linhas com 37 colunas.

Entre essas colunas, 23 tem dados faltantes:

| Campo                                             | Qtd   |
|---------------------------------------------------|-------|
| scrape_id                                         | 1     |
| name                                              | 1120  |
| summary                                           | 29650 |
| space                                             | 232272|
| description                                       | 13524 |
| neighborhood_overview                             | 271159|
| host_is_superhost                                 | 294   |
| host_listings_count                               | 294   |
| bathrooms                                         | 1126  |
| bedrooms                                          | 592   |
| beds                                              | 1759  |
| instant_bookable                                  | 1     |
| cancellation_policy                               | 1     |
| minimum_minimum_nights                            | 136970|
| maximum_minimum_nights                            | 136970|
| minimum_maximum_nights                            | 136970|
| maximum_maximum_nights                            | 136970|
| minimum_nights_avg_ntm                            | 136970|
| maximum_nights_avg_ntm                            | 136970|
| number_of_reviews_ltm                             | 136970|
| calculated_host_listings_count_entire_homes       | 136970|
| calculated_host_listings_count_private_rooms      | 136970|
| calculated_host_listings_count_shared_rooms       | 136970|

Nas colunas `minimum_minimum_nights`, `maximum_minimum_nights`, `minimum_maximum_nights`, `maximum_maximum_nights`, `minimum_nights_avg_ntm`, `maximum_nights_avg_ntm`, `number_of_reviews_ltm`, `calculated_host_listings_count_entire_homes`, `calculated_host_listings_count_private_rooms` e `calculated_host_listings_count_shared_rooms`, sob minha análise, são dados faltantes do tipo MCAR, ou seja sua falta se dá ao acaso, pelo dataset de treino ser um dataset gerado a partir provavelmente de um web scraping essas informações podem ter sidos perdidas na raspagem de dados.
A partir dessa conclusão, escolhi preencher esses campos com a mediana dos valores não faltantes como o campo é numérico e por ser uma abordagem simples.
Nos campos `bathrooms`, `bedrooms` e `beds` também foi usada a mesma lógica, tive o cuidado de observar se as colunas tinham uma relação de dependência entre si mas a quantidade de camas não é proprocional a quantidade de pessoas que acomoda e a quantidade de banheiros muitas vezes está entre 1 e 2, como pode ser observado na imagem a seguir:

![image.png]()
<br>

As demais colunas são do tipo nominal e não possuem uma proximidade entre os valores ou alguma característica que eu possa definir o padrão. No entanto, observei uma certa incidência de uso do mesmo que foi escrito em `summary` na `description`, a partir disso escolhi verificar se um está vazio e o outro não então ambos terão o mesmo valor partindo dessa conclusão e orientada pelo fato de dados faltantes em summary ser superior ao que temos em description.

<br>

No caso particular de `space` e `neighborhood_overview` vi diversas vezes respostas simples e pouco explicativas, escolhi então criar uma lista com valores genéricos em português e inglês, verficar a língua que foi escrito o anúncio e escolher um valor aleatório da lista para ser inserido.

Com todos esses métodos usados pra mitigar a quantidade de dados ausentes, ao fim ficaram essas quantidades de dados faltantes:

| Campo                    | Qtd    |
|--------------------------|--------|
| scrape_id                | 1      |
| name                     | 1120   |
| summary                  | 13524  |
| space                    | 94057  |
| description              | 13524  |
| neighborhood_overview    | 110407 |
| host_is_superhost        | 294    |
| host_listings_count      | 294    |
| instant_bookable         | 1      |
| cancellation_policy      | 1      |


Com essa quantidade menor de dados faltantes, retirei as linhas que tivessem qualquer dado faltante e fiquei com 457821 linhas.
Tive uma perca de aproximadamente 22%.


