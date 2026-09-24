# QualiAuto AI — Fase 1: Planejamento e Definição do Problema

## 1. Visão geral

O **QualiAuto AI** é um projeto de Ciência de Dados e Inteligência Artificial voltado à análise de reclamações de consumidores sobre veículos.

O projeto utiliza como fonte inicial de dados o **NHTSA Customer Complaints**, que contém registros de reclamações automotivas, incluindo descrições textuais dos problemas relatados pelos consumidores e informações relacionadas aos veículos e aos componentes envolvidos.

A proposta do QualiAuto AI não se limita à criação de um classificador de textos. O projeto pretende combinar **NLP (Natural Language Processing), Machine Learning, Deep Learning e análise de dados** para transformar reclamações individuais em informações capazes de apoiar análises de qualidade automotiva.

O sistema será desenvolvido como uma ferramenta de **apoio à análise e à tomada de decisão**, e não como um mecanismo de diagnóstico automático de defeitos.

---

## 2. Problema de negócio

Organizações do setor automotivo podem lidar com grandes volumes de reclamações de consumidores, muitas delas registradas na forma de texto livre.

A análise manual desses relatos pode dificultar:

* a classificação das reclamações;
* a identificação dos componentes ou sistemas envolvidos;
* o acompanhamento da evolução dos problemas ao longo do tempo;
* a identificação de concentrações ou aumentos incomuns de determinados tipos de reclamação;
* a priorização de situações que merecem investigação técnica.

Diante desse cenário, o problema de negócio definido para o projeto é:

> **Como utilizar dados e técnicas de Inteligência Artificial para analisar automaticamente reclamações automotivas e transformá-las em informações úteis para apoiar a identificação e investigação de padrões relacionados à qualidade dos veículos?**

O QualiAuto AI pretende atuar em duas frentes complementares:

1. **Classificação automática das reclamações**, utilizando o texto relatado pelo consumidor.
2. **Inteligência de qualidade**, utilizando as reclamações classificadas e outras informações disponíveis no dataset para investigar padrões e tendências.

---

## 3. Objetivo geral

Desenvolver uma solução de inteligência de qualidade automotiva capaz de analisar reclamações de consumidores, utilizando técnicas de NLP e Machine Learning para classificar automaticamente os relatos por componente ou sistema do veículo e apoiar a identificação de padrões, tendências e possíveis anomalias nas reclamações.

---

## 4. Objetivos específicos

1. **Explorar e compreender** os dados de reclamações automotivas da NHTSA, identificando características, qualidade dos dados, distribuição das categorias e possíveis limitações.

2. **Desenvolver um modelo de classificação de textos** que utilize a descrição da reclamação (`CDESCR`) para identificar o componente ou sistema relacionado, inicialmente representado por `COMPDESC`.

3. **Comparar o modelo desenvolvido em TensorFlow com um baseline**, utilizando métricas como accuracy, precision, recall e F1-score.

4. **Analisar padrões e tendências nas reclamações**, considerando dimensões como componente, período, fabricante, modelo e ano do veículo, quando os dados permitirem.

5. **Construir um protótipo do QualiAuto AI** que integre o modelo de classificação e as análises de qualidade em uma solução demonstrável.

---

## 5. Usuários do sistema

### 5.1 Usuário principal

O principal usuário considerado para o QualiAuto AI será o **analista de qualidade automotiva**.

Esse profissional poderá utilizar o sistema para acompanhar reclamações e investigar possíveis padrões relacionados à qualidade dos veículos.

### 5.2 Usuários secundários

Como usuários secundários, são considerados:

* engenheiros de qualidade;
* engenheiros de produto;
* gestores responsáveis pelo acompanhamento de indicadores de qualidade.

### 5.3 Decisões apoiadas

O QualiAuto AI deverá fornecer informações que auxiliem esses profissionais a:

* identificar componentes com maior concentração de reclamações;
* identificar componentes apresentando crescimento no número de relatos;
* investigar padrões relacionados a fabricantes, modelos e anos;
* acompanhar a evolução temporal das reclamações;
* identificar situações que mereçam análise técnica mais aprofundada;
* consultar a provável classificação de uma nova reclamação.

O sistema será uma ferramenta de **apoio à decisão**.

Uma concentração ou aumento de reclamações não deverá ser interpretado automaticamente como evidência da existência de um defeito.

---

## 6. Perguntas de negócio

As análises do projeto serão orientadas inicialmente pelas seguintes perguntas.

### 6.1 Volume e concentração

1. Quais componentes ou sistemas concentram o maior número de reclamações?

2. Quais fabricantes, modelos e anos concentram mais reclamações?

3. Existem combinações de veículo e componente com concentração particularmente elevada de reclamações?

> **Limitação importante:** quantidade absoluta de reclamações não representa necessariamente taxa de defeito. Caso o dataset não forneça informações sobre a quantidade de veículos vendidos ou em circulação, não será possível calcular diretamente a incidência relativa de problemas.

### 6.2 Evolução temporal

4. Como o volume de reclamações evolui ao longo do tempo?

5. Existem componentes, fabricantes ou modelos apresentando crescimento incomum no número de reclamações?

6. É possível identificar períodos com aumentos anormais de determinados tipos de reclamação?

### 6.3 Gravidade dos relatos

7. Quais componentes estão mais frequentemente associados a relatos envolvendo acidentes, incêndios, feridos ou outros indicadores de gravidade disponíveis no dataset?

8. Existem fabricantes, modelos ou componentes com padrões relevantes quando consideramos simultaneamente volume e gravidade dos relatos?

### 6.4 Classificação automática

9. É possível utilizar o texto de uma reclamação (`CDESCR`) para identificar automaticamente o componente ou sistema relacionado?

10. Com que nível de desempenho essa classificação pode ser realizada?

11. Quais componentes são mais difíceis de distinguir automaticamente?

12. Em quais tipos de reclamação o modelo apresenta mais erros?

Essas perguntas poderão ser modificadas, eliminadas ou complementadas durante a EDA conforme as características efetivamente encontradas nos dados.

---

## 7. Hipóteses iniciais

### 7.1 H1 — Classificação de reclamações

É possível utilizar o conteúdo textual das reclamações (`CDESCR`) para identificar automaticamente o componente ou sistema automotivo associado ao relato, utilizando `COMPDESC` como variável-alvo candidata.

Inicialmente:

```text id="3h9o31"
CDESCR
   │
   │ X — texto da reclamação
   ▼
Modelo de NLP
   │
   │ previsão
   ▼
COMPDESC
   y — componente/sistema
```

A hipótese deverá ser validada durante a análise exploratória e posteriormente por meio da construção de um baseline e dos modelos de NLP.

A EDA deverá verificar:

* valores ausentes;
* quantidade de categorias;
* distribuição das classes;
* granularidade das categorias;
* duplicidades;
* qualidade dos textos;
* relação entre reclamações e componentes;
* possíveis riscos de vazamento de informação;
* necessidade de agrupamento das categorias.

Dependendo dos resultados, `COMPDESC` poderá ser mantida, transformada ou substituída como variável-alvo.

### 7.2 H2 — Inteligência de qualidade

A organização e análise das reclamações considerando componentes, fabricantes, modelos, períodos e indicadores de gravidade poderá revelar padrões e variações relevantes para apoiar a priorização de investigações de qualidade automotiva.

A relação conceitual entre as duas hipóteses é:

```text id="6h23qy"
Reclamações
     │
     ▼
Classificação NLP
     │
     ▼
Componentes/sistemas
     │
     ├── Fabricante
     ├── Modelo
     ├── Ano
     ├── Tempo
     └── Indicadores de gravidade
              │
              ▼
      Análise de padrões
              │
              ▼
   Inteligência de qualidade
```

---

## 8. Critérios de sucesso

Os critérios de sucesso serão avaliados em três dimensões.

### 8.1 Sucesso do modelo

Antes do desenvolvimento do modelo em TensorFlow, será construído um **baseline** que servirá como referência.

Os modelos deverão ser avaliados utilizando, pelo menos:

* accuracy;
* precision;
* recall;
* F1-score;
* matriz de confusão;
* análise qualitativa dos erros.

Não será definida nesta etapa uma meta arbitrária de desempenho.

As metas quantitativas poderão ser estabelecidas após a EDA, quando forem conhecidas características como número de classes, desbalanceamento e complexidade do problema.

O desempenho do TensorFlow será comparado ao baseline.

O projeto não pressupõe que um modelo de Deep Learning necessariamente apresentará desempenho superior a uma abordagem mais simples.

### 8.2 Sucesso analítico

A solução deverá possibilitar a investigação das principais perguntas de negócio relacionadas a:

* componentes;
* fabricantes;
* modelos;
* anos;
* evolução temporal;
* indicadores de gravidade.

As conclusões deverão respeitar as limitações existentes no dataset.

O sistema deverá identificar **sinais que mereçam investigação**, e não declarar automaticamente a existência de defeitos nos veículos.

### 8.3 Sucesso do produto

O resultado final deverá ser um protótipo demonstrável do QualiAuto AI.

A solução deverá integrar, quando tecnicamente viável:

```text id="18x38m"
             QualiAuto AI
                  │
        ┌─────────┴─────────┐
        │                   │
        ▼                   ▼
Classificação           Inteligência
de reclamações          de qualidade
        │                   │
        ▼                   ▼
Componente           Indicadores
provável             Tendências
                     Padrões
                     Possíveis anomalias
        │                   │
        └─────────┬─────────┘
                  ▼
          Apoio à análise
            de qualidade
```

O protótipo deverá permitir demonstrar o fluxo do projeto desde os dados originais até a utilização dos resultados.

---

## 9. Formulação inicial do problema de Machine Learning

O problema de Machine Learning será tratado inicialmente como uma tarefa de **classificação supervisionada de textos**.

### Entrada (`X`)

`CDESCR`

Descrição textual da reclamação realizada pelo consumidor.

### Variável-alvo candidata (`y`)

`COMPDESC`

Descrição do componente ou sistema automotivo associado à reclamação.

### Formulação inicial

```text id="11c4e2"
f(CDESCR) → COMPDESC
```

A formulação não será considerada definitiva até a conclusão da análise exploratória dos dados.

---

## 10. Diretrizes técnicas já estabelecidas para o projeto

Além das decisões específicas desta fase, o projeto QualiAuto AI já possui algumas diretrizes técnicas estabelecidas para orientar as etapas posteriores:

* compreender os dados antes de modelar;
* preservar os dados brutos;
* documentar a procedência e as limitações do dataset;
* utilizar `uv` para gerenciamento do projeto e das dependências Python;
* evitar vazamento de dados;
* construir um baseline antes do TensorFlow;
* não avaliar modelos somente por accuracy;
* utilizar também precision, recall e F1-score;
* analisar os erros do modelo;
* distinguir concentração de reclamações de evidência de defeito;
* utilizar Machine Learning como apoio à análise, e não como substituto automático da decisão humana;
* documentar decisões técnicas e limitações;
* priorizar reprodutibilidade;
* construir um produto demonstrável ao final do projeto.

---

## 11. Fluxo inicial do QualiAuto AI

```text id="hig6lu"
NHTSA Customer Complaints
            │
            ▼
    Auditoria dos dados
            │
            ▼
            EDA
            │
            ▼
 Preparação dos dados
            │
            ▼
     Baseline de NLP
            │
            ▼
   TensorFlow / Keras
            │
            ▼
   Avaliação e erros
            │
            ▼
    Modelo selecionado
            │
            ▼
 ┌──────────┴───────────┐
 │                      │
 ▼                      ▼
Inferência        Análise de qualidade
 │                      │
 └──────────┬───────────┘
            ▼
       QualiAuto AI
```

---

## 12. Decisões consolidadas da Fase 1

Ao final da etapa de planejamento e definição do problema, foram estabelecidas as seguintes decisões:

* **Escopo do projeto:** classificação automática de reclamações + inteligência de qualidade automotiva.
* **Problema inicial de Machine Learning:** classificação supervisionada de textos.
* **Variável de entrada candidata (`X`):** `CDESCR`.
* **Variável-alvo candidata (`y`):** `COMPDESC`.
* **Usuário principal:** analista de qualidade automotiva.
* **Usuários secundários:** engenheiros de qualidade, engenheiros de produto e gestores de qualidade.
* **Papel do sistema:** apoio à análise e à decisão, e não diagnóstico automático de defeitos.
* **Estratégia de modelagem:** construir um baseline antes do modelo TensorFlow.
* **Avaliação:** utilizar accuracy, precision, recall, F1-score, matriz de confusão e análise dos erros.
* **Validação do target:** a adequação de `COMPDESC` será investigada durante a EDA.
* **Inteligência de qualidade:** investigar padrões envolvendo componentes, fabricantes, modelos, tempo e indicadores de gravidade.
* **Produto esperado:** protótipo integrado e demonstrável do QualiAuto AI.

Essas decisões constituem o ponto de partida do projeto e poderão ser revisadas quando novas evidências forem encontradas durante a exploração dos dados.

---

## 13. Próxima etapa

A etapa de ambiente e estrutura do projeto já foi parcialmente executada.

Entre os itens já preparados estão a inicialização do projeto com `uv`, definição da versão do Python, inicialização do Git, criação do `.gitignore` e README inicial.

Antes de avançar integralmente para a análise exploratória dos dados, deverão ser concluídas as pendências restantes dessa etapa, especialmente:

* revisar e adicionar as dependências necessárias utilizando `uv`;
* verificar/criar a estrutura de diretórios planejada para o projeto.

Após a conclusão dessas pendências, o projeto avançará para a etapa de **Dados, Compreensão e EDA**, na qual as hipóteses estabelecidas nesta documentação serão confrontadas com as características reais do NHTSA Customer Complaints.

A partir das evidências encontradas na EDA, decisões como a utilização definitiva de `COMPDESC` como variável-alvo, a granularidade das classes e eventuais transformações necessárias poderão ser revistas.

## 3.1 Origem e proveniência dos dados

O projeto **QualiAuto AI** utiliza como conjunto de dados inicial a base **NHTSA Complaints**, composta por registros de reclamações de consumidores relacionadas a veículos automotores.

### Fonte original

Os dados têm como fonte original a **National Highway Traffic Safety Administration (NHTSA)**, órgão do Department of Transportation dos Estados Unidos responsável, entre outras atribuições, pela coleta e análise de informações relacionadas à segurança de veículos.

A base de reclamações de consumidores é utilizada pela NHTSA como uma das fontes de informação para identificação e investigação de possíveis problemas relacionados à segurança veicular.

### Fonte utilizada para obtenção do dataset

Para o desenvolvimento do QualiAuto AI, o conjunto de dados foi obtido por meio do **Kaggle**, no dataset:

**NHTSA Complaints**

* **Plataforma:** Kaggle
* **Publicador no Kaggle:** `alshival`
* **Dataset:** `NHTSA Complaints`
* **URL:** `https://www.kaggle.com/datasets/alshival/nhtsa-complaints`
* **Data do download:** 19/09/2026
* **Fonte original dos dados:** National Highway Traffic Safety Administration (NHTSA)

### Uso dos dados no QualiAuto AI

O dataset será utilizado inicialmente para:

* análise exploratória das reclamações automotivas;
* investigação da qualidade e estrutura dos dados;
* análise da distribuição dos componentes e sistemas automotivos;
* análise de fabricantes, modelos, anos e evolução temporal;
* investigação de indicadores relacionados à gravidade dos relatos;
* desenvolvimento de modelos de classificação de texto;
* investigação de padrões e tendências relacionados às reclamações.

A hipótese inicial de Machine Learning definida na Fase 1 considera:

```text
CDESCR
   │
   │ texto da reclamação
   ▼
Modelo de NLP
   │
   ▼
COMPDESC
   │
   └── componente/sistema associado
```

Nesse cenário, `CDESCR` será investigado como variável de entrada (`X`) e `COMPDESC` como variável-alvo candidata (`y`).

A adequação dessa formulação ainda deverá ser validada durante a análise exploratória dos dados.

### Versionamento e reprodutibilidade

A versão utilizada neste projeto corresponde ao conjunto de dados disponível no Kaggle e baixado em **19 de setembro de 2026**.

A data de obtenção do dataset deve ser considerada parte do versionamento dos dados do projeto.

Os arquivos originais serão preservados sem alterações na área destinada aos **dados brutos (`raw`)**, enquanto eventuais tratamentos e transformações deverão gerar novos arquivos ou conjuntos de dados derivados.

Essa estratégia permite:

* preservar a fonte utilizada originalmente;
* reproduzir as análises;
* rastrear as transformações realizadas;
* comparar futuramente os resultados com versões mais recentes da base.

### Limitações relacionadas à fonte

Embora o dataset tenha sido obtido pelo Kaggle, a fonte original das informações é a NHTSA.

A versão disponibilizada no Kaggle não deve ser automaticamente considerada idêntica à versão mais recente disponível diretamente pela NHTSA.

Além disso, a base de reclamações representa **relatos de consumidores**. Portanto, a existência ou concentração de reclamações não deve ser interpretada isoladamente como comprovação da existência de defeito em determinado veículo, fabricante ou componente.

Da mesma forma, o número absoluto de reclamações não representa necessariamente uma **taxa de incidência**, pois esse tipo de análise exigiria um denominador adequado, como quantidade de veículos vendidos ou em circulação.

Essas limitações deverão ser consideradas durante a interpretação dos resultados do QualiAuto AI.

## 3.2 Leitura inicial dos conjuntos de dados

Após registrar a origem e a proveniência dos dados, foi realizada uma primeira inspeção dos cinco conjuntos que compõem o projeto QualiAuto AI.

O objetivo desta etapa não é realizar limpeza ou integração, mas compreender:

- o que cada dataset representa;
- qual é a unidade aproximada de observação;
- quais informações estão disponíveis;
- quais campos parecem relacionar as bases;
- quais cuidados deverão ser considerados durante a EDA.

---

### 3.2.1 Visão geral das cinco fontes

Os datasets representam diferentes perspectivas sobre segurança e qualidade automotiva.

```text
                         QUALIAUTO AI
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
   COMPLAINTS          INVESTIGATIONS            RECALLS
   Reclamações          Investigações           Campanhas
   de consumidores      da NHTSA                de recall
        │                     │                     │
        │                     │                     │
        └──────────────┬──────┴──────────────┬──────┘
                       │                     │
                       ▼                     ▼
                    RATINGS              CAR MODELS
                  Avaliações de          Referência de
                    segurança          ano/marca/modelo
```

Cada base responde a uma pergunta diferente:

| Dataset | Pergunta principal |
|---|---|
| `complaints.csv` | O que os consumidores estão relatando? |
| `investigations.csv` | O que a NHTSA decidiu investigar? |
| `recalls.csv` | Quais problemas estão associados a campanhas de recall? |
| `ratings.csv` | Como os veículos foram avaliados em segurança? |
| `car_models.csv` | Quais combinações de ano, marca e modelo estão registradas? |

---

# 3.3 Complaints — reclamações dos consumidores

O `complaints.csv` contém registros de problemas relatados por consumidores.

### Estrutura inicial

```text
284.745 registros
15 variáveis
28,8 MB

Tipos:
├── 9 str
├── 4 int64
└── 2 bool
```

### Principais variáveis

| Variável | Papel inicial |
|---|---|
| `odiNumber` | Identificador do registro |
| `manufacturer` | Fabricante |
| `make` | Marca |
| `model` | Modelo |
| `modelYear` | Ano-modelo |
| `crash` | Indicação de acidente |
| `fire` | Indicação de incêndio |
| `numberOfInjuries` | Número de feridos |
| `numberOfDeaths` | Número de mortes |
| `dateOfIncident` | Data do incidente |
| `dateComplaintFiled` | Data de registro da reclamação |
| `vin` | Identificação do veículo |
| `components` | Componente(s) associado(s) |
| `summary` | Relato textual da reclamação |
| `products` | Informações sobre o produto associado ao registro |

### Relação central para NLP

A inspeção dos primeiros registros mostrou que `summary` contém o relato do problema, enquanto `components` informa o componente relacionado.

```text
             RECLAMAÇÃO
                 │
                 ▼
             summary
        "O que aconteceu?"
                 │
                 ▼
        ┌─────────────────┐
        │ Modelo de NLP ? │
        └─────────────────┘
                 │
                 ▼
            components
      "Qual sistema/componente?"
```

Isso mantém uma hipótese importante para o projeto:

`summary → components`

Entretanto, foram encontrados registros como:

```text
SEAT BELTS,SEATS
```

Logo, uma reclamação pode estar associada a mais de um componente.

```text
                    summary
                       │
                       ▼
                  reclamação
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
        SEAT BELTS             SEATS
```

Isso deverá ser investigado antes de definir se o problema de ML será multiclasse, multirrótulo ou terá outra formulação.

---

# 3.4 Recalls — campanhas de recall

O `recalls.csv` contém informações sobre campanhas relacionadas a problemas ou defeitos identificados em veículos e componentes.

### Principais variáveis

| Variável | Papel inicial |
|---|---|
| `Manufacturer` | Fabricante responsável |
| `NHTSACampaignNumber` | Identificador da campanha de recall |
| `parkIt` | Indicador relacionado à recomendação de não utilização do veículo |
| `parkOutSide` | Indicador relacionado à recomendação de estacionar o veículo externamente |
| `ReportReceivedDate` | Data de recebimento/registro do relatório |
| `Component` | Componente ou sistema relacionado ao recall |
| `Summary` | Descrição do problema ou defeito |
| `Consequence` | Possíveis consequências do defeito |
| `Remedy` | Procedimento ou solução para correção |
| `Notes` | Informações adicionais sobre a campanha |
| `ModelYear` | Ano-modelo |
| `Make` | Marca |
| `Model` | Modelo |
| `NHTSAActionNumber` | Número de ação associado na NHTSA |
| `overTheAirUpdate` | Indicador relacionado à possibilidade de atualização remota |

### Estrutura conceitual

Algumas variáveis formam uma sequência particularmente interessante para inteligência de qualidade:

```text
Component
    │
    ▼
Qual componente apresenta o problema?
    │
    ▼
Summary
    │
    ▼
Qual defeito/problema foi identificado?
    │
    ▼
Consequence
    │
    ▼
O que pode acontecer?
    │
    ▼
Remedy
    │
    ▼
Como o problema será corrigido?
```

Podemos resumir essa estrutura como:

```text
COMPONENTE
    │
    ▼
  DEFEITO
    │
    ▼
CONSEQUÊNCIA
    │
    ▼
 CORREÇÃO
```

### Uma campanha pode envolver vários modelos

Na inspeção inicial foi observado:

```text
Campanha 14V798000
│
├── BLUE BIRD
│   └── ALL AMERICAN — 2016
│
└── BLUE BIRD
    └── VISION — 2016
```

Portanto:

> **Número de registros não é necessariamente igual ao número de campanhas de recall.**

Uma campanha pode aparecer em vários registros porque pode abranger diferentes modelos e/ou anos-modelo.

### Componentes possuem diferentes níveis de detalhe

Foram encontrados exemplos como:

```text
PARKING BRAKE
```

e:

```text
PARKING BRAKE:DRIVELINE:HYDRAULIC:ACTUATOR
```

ou:

```text
ENGINE AND ENGINE COOLING:EXHAUST SYSTEM
```

Isso indica diferentes níveis de especificidade na descrição dos componentes.

```text
PARKING BRAKE
      │
      ▼
  DRIVELINE
      │
      ▼
  HYDRAULIC
      │
      ▼
   ACTUATOR
```

Essa granularidade deverá ser investigada antes de qualquer padronização.

---

# 3.5 Investigations — investigações da NHTSA

O `investigations.csv` contém informações associadas às investigações conduzidas pela NHTSA.

### Estrutura inicial

```text
154.380 registros
11 variáveis
13 MB

5.348 valores distintos de
NHTSA ACTION NUMBER
```

### Principais variáveis

| Variável | Papel inicial |
|---|---|
| `NHTSA ACTION NUMBER` | Identificador da ação/investigação |
| `MAKE` | Marca |
| `MODEL` | Modelo |
| `YEAR` | Ano-modelo |
| `COMPNAME` | Componente ou sistema investigado |
| `MFR_NAME` | Fabricante |
| `ODATE` | Data associada à abertura da investigação |
| `CDATE` | Data associada ao encerramento da investigação |
| `CAMPNO` | Número de campanha associado ao registro |
| `SUBJECT` | Assunto ou título da investigação |
| `SUMMARY` | Descrição textual da investigação |

### Uma investigação pode possuir vários registros

A inspeção mostrou:

```text
154.380 registros
        │
        ▼
5.348 NHTSA ACTION NUMBER distintos
        │
        ▼
uma investigação pode gerar
vários registros no dataset
```

Por exemplo:

```text
Investigação AQ08001
│
├── PACE AMERICAN — TRAILER — 2003
├── PACE AMERICAN — TRAILER — 2004
└── PACE AMERICAN — TRAILER — 2005
```

Portanto:

> **Número de registros não representa diretamente o número de investigações.**

### Representação das datas

Foram encontrados valores como:

```text
ODATE = 20080618
CDATE = 20081029
```

que apresentam estrutura:

```text
AAAAMMDD

20080618
   ↓
18/06/2008

20081029
   ↓
29/10/2008
```

Os significados exatos e as regras de preenchimento dessas variáveis deverão ser confirmados antes do tratamento.

### Relação entre investigação e recall

Uma das descobertas mais importantes da inspeção foi:

```text
Investigação AQ09001
│
├── CAMPNO 05E069000
├── CAMPNO 06E027000
├── CAMPNO 06E066000
├── CAMPNO 06E080000
├── CAMPNO 06E099000
├── CAMPNO 07E020000
└── ...
```

Uma investigação pode, portanto, aparecer associada a diferentes números de campanha.

No dataset de recalls existe:

```text
NHTSACampaignNumber
```

enquanto em investigations existe:

```text
CAMPNO
```

Isso sugere uma relação a ser posteriormente validada:

```text
       INVESTIGATIONS                       RECALLS

┌─────────────────────────┐         ┌─────────────────────────┐
│ NHTSA ACTION NUMBER     │         │ NHTSACampaignNumber     │
│ CAMPNO                  │────────▶│                         │
│ COMPNAME                │         │ Component               │
│ SUMMARY                 │         │ Summary                 │
└─────────────────────────┘         └─────────────────────────┘

              CAMPNO  ↔  NHTSACampaignNumber
```

Essa é, até o momento, uma das relações mais explícitas encontradas entre as bases.

---

# 3.6 Ratings — avaliações de segurança

O `ratings.csv` contém informações relacionadas às avaliações de segurança dos veículos.

### Estrutura inicial

```text
2.469 registros
25 variáveis
482,4 KB

Tipos:
├── 21 str
├── 2 float64
└── 2 int64
```

### Principais variáveis

| Variável | Papel inicial |
|---|---|
| `OverallRating` | Avaliação geral de segurança |
| `OverallFrontCrashRating` | Avaliação geral em colisão frontal |
| `FrontCrashDriversideRating` | Avaliação frontal do lado do motorista |
| `FrontCrashPassengersideRating` | Avaliação frontal do lado do passageiro |
| `OverallSideCrashRating` | Avaliação geral em colisão lateral |
| `SideCrashDriversideRating` | Avaliação lateral do lado do motorista |
| `SideCrashPassengersideRating` | Avaliação lateral do lado do passageiro |
| `combinedSideBarrierAndPoleRating-Front` | Avaliação combinada de barreira lateral e poste na região dianteira |
| `combinedSideBarrierAndPoleRating-Rear` | Avaliação combinada de barreira lateral e poste na região traseira |
| `sideBarrierRating-Overall` | Avaliação geral no teste de barreira lateral |
| `RolloverRating` | Avaliação relacionada a capotamento |
| `RolloverRating2` | Segunda variável de avaliação relacionada a capotamento |
| `RolloverPossibility` | Possibilidade/probabilidade registrada de capotamento |
| `RolloverPossibility2` | Segunda variável relacionada à possibilidade de capotamento |
| `dynamicTipResult` | Resultado do teste dinâmico relacionado a capotamento |
| `SidePoleCrashRating` | Avaliação de colisão lateral contra poste |
| `NHTSAElectronicStabilityControl` | Informação sobre controle eletrônico de estabilidade |
| `NHTSAForwardCollisionWarning` | Informação sobre alerta de colisão frontal |
| `NHTSALaneDepartureWarning` | Informação sobre alerta de saída de faixa |
| `ModelYear` | Ano-modelo |
| `Make` | Marca |
| `Model` | Modelo |
| `VehicleDescription` | Descrição da configuração do veículo |
| `VehicleId` | Identificador do veículo/configuração |
| `rating_updated_on` | Data/hora de atualização do registro de avaliação |

> **Observação:** o significado exato das variáveis com sufixo `2` deverá ser confirmado na documentação antes de qualquer interpretação analítica.

### Dimensões das avaliações

O dataset oferece diferentes perspectivas de segurança:

```text
                         VEÍCULO
                            │
             ┌──────────────┼──────────────┐
             │              │              │
             ▼              ▼              ▼
        FRONT CRASH     SIDE CRASH      ROLLOVER
             │              │              │
        motorista       motorista       possibilidade
        passageiro      passageiro      de capotamento
```

Além disso:

```text
VEÍCULO
   │
   ├── Electronic Stability Control
   ├── Forward Collision Warning
   └── Lane Departure Warning
```

### `Not Rated` não significa nota zero

Foi observado:

```text
OverallRating

5
Not Rated
5
Not Rated
...
```

Portanto:

```text
Not Rated
    ≠
Nota 0
```

Para o pandas, `"Not Rated"` é um valor textual existente. Semanticamente, entretanto, representa uma avaliação não disponível.

```text
df.info()
    │
    ▼
não identifica NaN
    │
    ▼
"Not Rated"
    │
    ▼
informação de avaliação indisponível
```

### Diferentes configurações do mesmo modelo

Também foi observado:

```text
2024 ACURA MDX
│
├── SUV FWD → VehicleId 18963
│
└── SUV AWD → VehicleId 18964
```

Isso demonstra que:

```text
Make + Model + ModelYear
```

não necessariamente identifica uma configuração específica dentro do dataset de ratings.

---

# 3.7 Car Models — referência de veículos

O `car_models.csv` possui a estrutura mais simples entre os cinco conjuntos.

### Estrutura inicial

```text
6.665 registros
3 variáveis
156,3 KB

Tipos:
├── 1 int64
└── 2 str
```

### Principais variáveis

| Variável | Papel inicial |
|---|---|
| `modelYear` | Ano-modelo |
| `make` | Marca |
| `model` | Modelo |

Sua estrutura básica é:

```text
modelYear
    +
make
    +
model
```

Exemplos:

```text
2020 + BMW       + Z4
2018 + CHEVROLET + BOLT EV
2022 + GENESIS   + G90
2018 + FERRARI   + 488 SPIDER
2023 + AUDI      + A4
```

A inspeção inicial sugere que essa base pode funcionar como uma referência das combinações de ano, marca e modelo.

Entretanto, ainda será necessário verificar se:

```text
modelYear + make + model
```

é realmente uma combinação única.

---

# 3.8 Como os cinco datasets começam a se conectar

A inspeção inicial permite construir o primeiro mapa conceitual do QualiAuto AI.

```text
                    ┌────────────────────┐
                    │     CAR MODELS     │
                    │ ano / marca/modelo │
                    └─────────┬──────────┘
                              │
                              │ referência do veículo
                              ▼
                    ┌────────────────────┐
                    │      VEÍCULO       │
                    └─────────┬──────────┘
                              │
          ┌───────────────────┼───────────────────┐
          │                   │                   │
          ▼                   ▼                   ▼
┌──────────────────┐ ┌──────────────────┐ ┌──────────────────┐
│    COMPLAINTS    │ │     RATINGS      │ │     RECALLS      │
│                  │ │                  │ │                  │
│ problemas        │ │ avaliação de     │ │ defeitos e       │
│ relatados        │ │ segurança        │ │ campanhas        │
└────────┬─────────┘ └──────────────────┘ └────────▲─────────┘
         │                                         │
         │ possíveis padrões                       │ CAMPNO
         │                                         │
         ▼                                         │
┌──────────────────────────────────────────────────┴─┐
│                  INVESTIGATIONS                     │
│                                                    │
│           problemas investigados pela NHTSA        │
└────────────────────────────────────────────────────┘
```

Uma interpretação conceitual possível é:

```text
CONSUMIDOR
    │
    ▼
COMPLAINT
"Estou observando este problema."
    │
    ▼
possível padrão de segurança
    │
    ▼
INVESTIGATION
"A NHTSA está investigando este problema."
    │
    ▼
possível campanha
    │
    ▼
RECALL
"Existe uma ação formal relacionada ao defeito."
```

Esse fluxo é apenas conceitual.

Ele **não implica que toda reclamação gere uma investigação nem que toda investigação resulte em recall**.

O dataset `ratings` acrescenta outra perspectiva:

```text
                VEÍCULO
                   │
       ┌───────────┴───────────┐
       │                       │
       ▼                       ▼
problemas observados      desempenho de
no mundo real             segurança avaliado
       │                       │
       ▼                       ▼
complaints / recalls          ratings
/ investigations
```

---

# 3.9 Campos potencialmente relacionados

As bases apresentam diferentes nomes para conceitos semelhantes.

| Conceito | Complaints | Recalls | Investigations | Ratings | Car Models |
|---|---|---|---|---|---|
| Ano-modelo | `modelYear` | `ModelYear` | `YEAR` | `ModelYear` | `modelYear` |
| Marca | `make` | `Make` | `MAKE` | `Make` | `make` |
| Modelo | `model` | `Model` | `MODEL` | `Model` | `model` |
| Fabricante | `manufacturer` | `Manufacturer` | `MFR_NAME` | — | — |
| Componente | `components` | `Component` | `COMPNAME` | — | — |
| Texto relacionado ao problema | `summary` | `Summary` | `SUMMARY` | — | — |
| Campanha | — | `NHTSACampaignNumber` | `CAMPNO` | — | — |

### Possível dimensão comum do veículo

```text
                   IDENTIFICAÇÃO DO VEÍCULO

 complaints       recalls       investigations      ratings       car_models
     │               │                │                │               │
 modelYear       ModelYear           YEAR          ModelYear       modelYear
     │               │                │                │               │
    make            Make             MAKE             Make            make
     │               │                │                │               │
   model            Model            MODEL            Model           model
     │               │                │                │               │
     └───────────────┴────────────────┴────────────────┴───────────────┘
                                      │
                                      ▼
                            possível dimensão comum
                                do veículo
```

### Informações textuais e componentes

```text
             TEXTO                         COMPONENTE

complaints   summary        ───────────▶   components

recalls      Summary        ───────────▶   Component
               │
               ├───────────▶ Consequence
               └───────────▶ Remedy

investig.    SUMMARY        ───────────▶   COMPNAME
```

Isso mostra que **complaints, recalls e investigations possuem informação textual associada a componentes automotivos**, algo potencialmente importante para futuras análises de NLP.

---

# 3.10 Hipótese de evolução do QualiAuto AI

A hipótese inicial de aprendizado de máquina permanece:

```text
summary
   │
   ▼
MODELO NLP
   │
   ▼
components
```

Porém, a inspeção das demais fontes mostra que o projeto poderá futuramente explorar uma estrutura mais ampla:

```text
                   NOVA RECLAMAÇÃO
                         │
                         ▼
                    texto/summary
                         │
                         ▼
                 ┌────────────────┐
                 │   MODELO NLP   │
                 └───────┬────────┘
                         │
                         ▼
               componente provável
                         │
                         ▼
              INTELIGÊNCIA DE QUALIDADE
                         │
          ┌──────────────┼───────────────┐
          │              │               │
          ▼              ▼               ▼
     reclamações    investigações      recalls
      similares       relacionadas    relacionados
          │              │               │
          └──────────────┼───────────────┘
                         │
                         ▼
                      ratings
                         │
                         ▼
                contexto de segurança
```

Essa arquitetura ainda é apenas uma **hipótese de evolução do projeto**.

A EDA deverá determinar quais relações são realmente suportadas pelos dados antes da definição da arquitetura final.

---

# 3.11 Pontos de atenção para as próximas etapas

A inspeção inicial revelou questões que deverão ser investigadas antes de qualquer integração ou modelagem:

1. **Registro não significa necessariamente entidade única.**  
   Uma campanha ou investigação pode aparecer em várias linhas.

2. **Componentes possuem diferentes granularidades.**  
   Existem componentes simples, hierárquicos e registros com múltiplos componentes.

3. **As bases utilizam diferentes convenções de nomenclatura.**  
   Exemplos: `make`, `Make` e `MAKE`.

4. **Datas possuem diferentes representações.**  
   Algumas estão armazenadas como texto e outras como números.

5. **Ausência semântica nem sempre aparece como `NaN`.**  
   `Not Rated`, por exemplo, representa uma avaliação indisponível.

6. **Marca + modelo + ano não deve ser assumido imediatamente como chave única.**

7. **`CAMPNO ↔ NHTSACampaignNumber` é uma relação candidata que precisa ser validada.**

8. **As variáveis textuais `summary`, `Summary` e `SUMMARY` possuem papéis semelhantes, mas pertencem a contextos diferentes e não devem ser tratadas automaticamente como equivalentes.**

9. **Nenhum `merge` entre os datasets deverá ser realizado antes da análise de qualidade, granularidade e compatibilidade das possíveis chaves.**

---

# 3.12 Síntese da leitura inicial

A inspeção dos cinco datasets mostra que o QualiAuto AI possui fontes complementares de informação.

```text
             QUALIDADE E SEGURANÇA AUTOMOTIVA

                    ┌─────────────┐
                    │   VEÍCULO   │
                    └──────┬──────┘
                           │
        ┌──────────────────┼───────────────────┐
        │                  │                   │
        ▼                  ▼                   ▼
   EXPERIÊNCIA         AVALIAÇÃO           AÇÕES DE
   DO USUÁRIO          DE SEGURANÇA        SEGURANÇA
        │                  │                   │
        ▼                  ▼             ┌─────┴─────┐
   COMPLAINTS           RATINGS           ▼           ▼
                                  INVESTIGATIONS   RECALLS
```

Assim, as bases permitem observar o mesmo domínio por diferentes perspectivas:

```text
COMPLAINTS
    ↓
problemas relatados pelos consumidores

INVESTIGATIONS
    ↓
problemas investigados pela NHTSA

RECALLS
    ↓
campanhas associadas a defeitos

RATINGS
    ↓
avaliações e características de segurança

CAR MODELS
    ↓
referência de ano, marca e modelo
```

Essa visão será utilizada como referência durante as próximas etapas da análise exploratória.

O próximo objetivo será aprofundar a compreensão das variáveis, investigar qualidade, valores ausentes, duplicidades, categorias e granularidade antes de decidir como os dados serão preparados e integrados.