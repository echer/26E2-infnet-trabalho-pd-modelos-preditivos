# 26E2 - INFNET - Trabalho PD modelos preditivos utilizando KNIME

## Author: Alan C. Echer

## Etapa 1 – Coleta e Preparação dos Dados

### 1. Coleta dos dados

![dataset-kaggle](assets/dataset-kaggle.png)

Para este trabalho utilizarei a base de dados do kaggle: https://www.kaggle.com/datasets/sunil123kumar/social-media-impact-on-mental-health

A base foi escolhida por abordar um problema atual e de grande relevância social: a relação entre o uso de redes sociais e indicadores de saúde mental em adolescentes. Além disso, apresenta variáveis numéricas e categóricas, sendo adequada para aplicação de diferentes algoritmos de classificação estudados na disciplina.

A base possui 1200 registros válidos e nenhuma variável apresenta valores ausentes, ela contém dados da utilização de redes sociais por adolescentes, seus hábitos, performance escolar e indicadores mentais.

A base reúne informações sobre:

* idade;
* gênero;
* tempo diário de uso das redes sociais;
* plataforma utilizada;
* horas de sono;
* tempo de tela antes de dormir;
* desempenho escolar;
* atividade física;
* interação social;
* níveis de estresse;
* ansiedade;
* dependência de redes sociais;
* indicador de depressão.

### 2. Preparação dos dados

#### Valores ausentes

Foi identificado que não existem valores faltantes em nenhuma das 13 variáveis.

Portanto, não foi necessária nenhuma técnica de imputação.

#### Tipos de dados

Foi realizada a identificação das variáveis numéricas e categóricas.

As variáveis categóricas serão posteriormente convertidas utilizando One-Hot Encoding, permitindo sua utilização pelos algoritmos de Machine Learning.

#### Classe alvo

Inicialmente a variável alvo considerada foi Depression Label.

Entretanto, observou-se um forte desbalanceamento entre as classes, com aproximadamente 97,4% dos registros pertencentes à classe "não deprimido" e apenas 2,6% à classe "deprimido".

Nas etapas de modelagem serão avaliadas técnicas para lidar com esse desbalanceamento, como SMOTE ou Oversampling, conforme discutido na disciplina.

## Etapa 2 – Exploração dos Dados (EDA)

Realizou-se uma análise exploratória dos dados utilizando os componentes Statistics e Data Explorer do KNIME. O objetivo foi compreender a distribuição das variáveis, identificar possíveis inconsistências e conhecer as características da base antes da construção dos modelos preditivos.

* As variáveis numéricas apresentam distribuição relativamente homogênea.
* As variáveis categóricas possuem poucas categorias e são adequadas para codificação por One-Hot Encoding.
* A variável Gender apresenta distribuição equilibrada entre masculino e feminino.
* A variável Platform Usage possui três categorias (Instagram, TikTok e Both).
* A variável Depression Label apresenta forte desbalanceamento.

#### Coluna: Age - Idade do estudante (Numérica discreta)

As idades variam de 13 a 19 anos, sua média é de 15.9 e o desvio padrão é de 2.02. Os dados estão bem distribuidos.

![column_age.png](assets/column_age.png)

#### Coluna: Gender - Gênero do estudante (Categórica nominal)

O genero só possui dois tipos male e female e estão muito bem distribuidos em 51% e 49%

![column_gender](./assets/column_gender.png)

#### Coluna: Daily Social Media Hours - Horas gastas por dia em redes sociais (Numérica contínua)

As horas gastas por dias em redes sociais estão também bem distribuidas variando de 1 a 8 horas, média de 4.54 e desvio padrão de 2.03.

![column_daily_social_media_hours](./assets/column_daily_social_media_hours.png)

#### Coluna: Platform Usage - Uso de plataforma sociais (Categórica nominal)

A variável possui três categorias (Instagram, TikTok e Both), sendo que "Both" representa estudantes que utilizam ambas as plataformas. Como trata-se de uma variável categórica nominal, posteriormente será transformada por meio de One-Hot Encoding para utilização pelos algoritmos de classificação.

![column_platform_usage](./assets/column_platform_usage.png)

#### Coluna: Sleep Hours - Horas de sono (Numérica contínua)

A coluna horas de sono varia de 4 a 9 e tem dados bem distribuidos com uma média de 6.45 e um desvio padrao de 1.44.

![sleep_hours](./assets/column_sleep_hours.png)

#### Coluna: Screen Time Before Sleep - Tempo de tela antes de dormir (Numérica contínua)

A coluna tempo de tela antes de dormir possui dados variando de 0.5 até 2.4 horas com uma média de 1.74 e uma variação de 0.72, os dados são bem distribuidos.

![column_screen_time_before_sleep](./assets/column_screen_time_before_sleep.png)

#### Coluna: Academic Performance - Performance escolar (Numérica contínua)

A coluna performance escolar tem dados bem distribuidos variando de 2 a 4 com média de 2.99 e variação de 0.58.

![column_academic_performance](./assets/column_academic_performance.png)

#### Coluna: Physical Activity - Atividade fisica (Numérica contínua)

A coluna apresenta maior concentração em determinados níveis de atividade física, porém sem indícios de inconsistências, com alguns picos com valores variando de 0 a 2, média de 1.01 e desvio de 0.58.

![column_physical_activity](./assets/column_physical_activity.png)

#### Column: Social Interaction Level - Nível de interação social (Categórica ordinal)

A coluna nivel de interação social possui 3 valores: high 31%, medium 35%, low 35%, até que bem distribuidos.

![column_social_interaction_level](./assets/column_social_interaction_level.png)

#### Column: Stress Level - Nível de estresse (Numérica discreta)

A coluna nivel de estresse possui valores até que bem distribuidos variando de 1 a 10, com média de 5.45 e desvio de 2.9.

![column_stress_level](./assets/column_stress_level.png)

#### Column: Anxiety Level - Nível de ansiedade (Numérica discreta)

A coluna nivel de ansiedade também de valores bem distribuidos variando de 1 a 10, com média de 5.65 e desvio de 2.86.

![column_anxiety_level](./assets/column_anxiety_level.png)

#### Column: Addiction Level - Nível de dependência (Numérica discreta)

A coluna nível de dependência também tem dados bem distribuidos variando de 1 a 10, com média de 5.57 e desvio de 2.83.

![column_addiction_level](./assets/column_addiction_level.png)

#### Column: Depression Label - Rótulo de depressão (Categórica binária)

A coluna depression label é a coluna explicativa do nosso dataset e ela define se o estudante possui depressão ou não, se 0 = não tem depressão, se 1 = tem depressão. A variável alvo apresenta forte desbalanceamento, com aproximadamente 97,4% dos registros pertencentes à classe "não deprimido" e apenas 2,6% à classe "deprimido". Esse desbalanceamento pode prejudicar o treinamento dos modelos, favorecendo a classe majoritária. Para minimizar esse problema poderão ser utilizadas técnicas como SMOTE ou Oversampling durante o pré-processamento.

![column_depression_label](./assets/column_depression_label.png)
