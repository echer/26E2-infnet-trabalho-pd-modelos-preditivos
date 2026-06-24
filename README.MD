# 26E2 - INFNET - Trabalho PD modelos preditivos utilizando KNIME

## Author: Alan C. Echer

### Escolha da base de dados

![dataset-kaggle](assets/dataset-kaggle.png)

Para este trabalho utilizarei a base de dados do kaggle: https://www.kaggle.com/datasets/sunil123kumar/social-media-impact-on-mental-health

A base de dados contém 1.200 linhas e contém dados da utilização de redes sociais por adolescentes, seus hábitos, performance escolar e indicadores mentais e não possui dados faltantes.

A base de dados possui inicialmente 13 colunas:

#### Coluna: Age - Idade do estudante

As idades variam de 13 a 19 anos, sua média é de 15.9 e o desvio padrão é de 2.02. Os dados estão bem distribuidos.

![column_age.png](assets/column_age.png)

#### Coluna: Gender - Gênero do estudante

O genero só possui dois tipos male e female e estão muito bem distribuidos em 51% e 49%

![column_gender](./assets/column_gender.png)

#### Coluna: Hours Spent Daily - Horas gastas por dia em redes sociais

As horas gastas por dias em redes sociais estão também bem distribuidas variando de 1 a 8 horas, média de 4.54 e desvio padrão de 2.03.

![column_daily_social_media_hours](./assets/column_daily_social_media_hours.png)

#### Coluna: Platform Usage - Uso de plataforma sociais

A coluna uso de plataforma sociais tem apenas 3 valores: Instagram, TikTok e Both (que representa os dois juntos), a distribuição ficou meio afetada já que o terceiro valor representa ambas talvez seja necessario transformar Both em Instagram e TikTok ai teremos praticamente um balanceamento bem similar já que olhando somente Instagram e TikTok temos praticamente a mesma distribuição 34% e 33%, então se dividissemos os outros 33% de Both para Instagram e TikTok teriamos algo em torno de 50.5% para Instagram e 49.5% para TikTok, seria interessante para não confundir o modelo e ele pensar que Both seja uma outra dimensão.

![column_platform_usage](./assets/column_platform_usage.png)

#### Coluna: Sleep Hours - Horas de sono

A coluna horas de sono varia de 4 a 9 e tem dados bem distribuidos com uma média de 6.45 e um desvio padrao de 1.44.

![sleep_hours](./assets/column_sleep_hours.png)

#### Coluna: Screen Time Before Sleep - Tempo de tela antes de dormir

A coluna tempo de tela antes de dormir possui dados variando de 0.5 até 2.4 horas com uma média de 1.74 e uma variação de 0.72, os dados são bem distribuidos.

![column_screen_time_before_sleep](./assets/column_screen_time_before_sleep.png)

#### Coluna: Academic Performance - Performance escolar

A coluna performance escolar tem dados bem distribuidos variando de 2 a 4 com média de 2.99 e variação de 0.58.

![column_academic_performance](./assets/column_academic_performance.png)

#### Coluna: Physical Activity - Atividade fisica

A coluna atividade fisica tem dados não tão bem distribuidos assim, com alguns picos com valores variando de 0 a 2, média de 1.01 e desvio de 0.58.

![column_physical_activity](./assets/column_physical_activity.png)

#### Column: Social Interaction Level - Nível de interação social

A coluna nivel de interação social possui 3 valores: high 31%, medium 35%, low 35%, até que bem distribuidos.

![column_social_interaction_level](./assets/column_social_interaction_level.png)

#### Column: Stress Level - Nível de estresse

A coluna nivel de estresse possui valores até que bem distribuidos variando de 1 a 10, com média de 5.45 e desvio de 2.9.

![column_stress_level](./assets/column_stress_level.png)

#### Column: Anxiety Level - Nível de ansiedade

A coluna nivel de ansiedade também de valores bem distribuidos variando de 1 a 10, com média de 5.65 e desvio de 2.86.

![column_anxiety_level](./assets/column_anxiety_level.png)

#### Column: Addiction Level - Nível de dependência

A coluna nível de dependência também tem dados bem distribuidos variando de 1 a 10, com média de 5.57 e desvio de 2.83.

![column_addiction_level](./assets/column_addiction_level.png)

#### Column: Depression Label - Rótulo de depressão

A coluna depression label é a coluna explicativa do nosso dataset e ela define se o estudante possui depressão ou não, se 0 = não tem depressão, se 1 = tem depressão. O problema é que está totalmente desbalanceado, temos 1.169 registros sem depressão e apenas 31 registros com depressão, o que é bem preocupante e dificil de montar um model capaz de através dessa representatividade acertar com eficiência as variáveis que explicam o estudante ter depressão, portanto ao invés de utilizar técnicas para balancear os dados ou aprender mais sobre a classe minoritária, vamos mudar o foco e transformar uma outra coluna mais balanceada a fim de explicar outro aspecto dos nossos dados.

![column_depression_label](./assets/column_depression_label.png)
