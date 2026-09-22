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
