# 🚗 QualiAuto AI

Projeto de Ciência de Dados e Inteligência Artificial para explorar reclamações automotivas e investigar padrões relacionados à qualidade de veículos.

> **Status:** fase inicial de análise exploratória (EDA). Ainda não há modelo de Machine Learning treinado nem aplicação de inferência.

## 📖 Sobre o projeto

O QualiAuto AI utiliza o dataset **NHTSA Complaints**, disponibilizado no Kaggle, para analisar reclamações de consumidores por componente, fabricante, modelo, ano e indicadores de gravidade. O planejamento prevê uma futura classificação do texto das reclamações e análises de inteligência de qualidade.

O sistema é concebido como apoio à análise e à tomada de decisão. A concentração de reclamações não constitui, isoladamente, prova de defeito ou taxa de incidência.

## 🎯 Objetivos

- compreender a estrutura e a qualidade dos dados;
- explorar reclamações, veículos, recalls, investigações e avaliações;
- investigar a classificação de `CDESCR` por `COMPDESC` em etapas futuras;
- comparar um baseline com um modelo TensorFlow;
- identificar padrões e tendências que mereçam investigação técnica.

Esses são objetivos de planejamento; no estado atual, a implementação disponível é a exploração inicial dos dados.

## ✨ Implementação atual

- Cinco notebooks de EDA com leitura dos CSVs, dimensões, colunas, tipos e valores ausentes.
- Dados brutos organizados em `data/raw`.
- Projeto Python configurado com `pyproject.toml`, `uv.lock` e Python 3.11.
- Script de console `projeto-qualiai`, atualmente com uma mensagem de teste.

## 🏗️ Estrutura do projeto

```text
projeto-QualiAI/
├── data/raw/
│   ├── car_models.csv
│   ├── complaints.csv
│   ├── investigations.csv
│   ├── ratings.csv
│   └── recalls.csv
├── models/                 # reservado para modelos
├── notebooks/
│   ├── 01_eda_complaints.ipynb
│   ├── 02_eda_car_models.ipynb
│   ├── 03_eda_recalls.ipynb
│   ├── 04_eda_investigations.ipynb
│   └── 05_eda_ratings.ipynb
├── reports/                # reservado para relatórios
├── src/projeto_qualiai/
│   └── __init__.py
├── tests/                  # reservado para testes
├── analise-do-problema.md
├── pyproject.toml
├── uv.lock
└── README.md
```

Os CSVs contêm dados de modelos, reclamações, investigações, avaliações de segurança e recalls. Entre os campos estão fabricante, modelo, ano, componente, resumo, datas e indicadores de acidentes, incêndios, ferimentos e mortes.

## 🛠️ Tecnologias e dependências

- Python `>=3.11`;
- `uv`;
- Pandas, NumPy e Matplotlib para análise;
- Scikit-learn e TensorFlow, declarados para etapas futuras de Machine Learning;
- Jupyter Notebook para EDA.

As dependências e versões mínimas estão em `pyproject.toml`; a resolução completa está em `uv.lock`.

## 📋 Pré-requisitos

- Python 3.11 ou superior;
- `uv` para o fluxo recomendado;
- Jupyter instalado separadamente caso os notebooks sejam executados;
- espaço em disco para os arquivos brutos, incluindo CSVs grandes.

Não foram encontrados Dockerfiles, CI/CD, banco de dados, arquivos `.env` ou variáveis de ambiente necessárias.

## 📦 Instalação

### ⚡ Com uv

```bash
uv sync
```

### 🐍 Com pip

```bash
python -m venv .venv
```

Windows PowerShell:

```powershell
.venv\Scripts\Activate.ps1
```

Linux/macOS:

```bash
source .venv/bin/activate
```

Depois, instale o projeto pelo `pyproject.toml`:

```bash
python -m pip install .
```

Não existe `requirements.txt` no repositório.

O `pyproject.toml` não declara Jupyter como dependência do pacote; instale-o separadamente se necessário, por exemplo com `python -m pip install jupyter`.

## ▶️ Como executar

O script configurado no projeto pode ser executado com:

```bash
uv run projeto-qualiai
```

No estado atual, ele imprime `Hello from projeto-qualiai!`.

Para abrir os notebooks, execute a partir de `notebooks`, pois eles usam caminhos relativos para `../data/raw`:

```bash
cd notebooks
jupyter notebook
```

Os notebooks carregam os dados com `pandas.read_csv` e realizam inspeções iniciais como `head`, `shape`, `columns`, `info` e valores ausentes.

## 🧪 Testes

Não há testes automatizados implementados no diretório `tests`.

## 📊 Dados e limitações

Segundo `analise-do-problema.md`, os dados foram obtidos do dataset **NHTSA Complaints**, publicado por `alshival` no Kaggle, cuja fonte original é a National Highway Traffic Safety Administration (NHTSA). O download documentado ocorreu em 19/09/2026.

Os dados representam relatos de consumidores. A quantidade absoluta de reclamações não permite, sem um denominador como veículos vendidos ou em circulação, calcular diretamente uma taxa de incidência. A documentação também prevê preservar os arquivos brutos e validar a variável-alvo antes da modelagem.

## 🚀 Próximos passos

- concluir a auditoria e a EDA;
- documentar resultados e limitações;
- validar `CDESCR` e `COMPDESC`;
- construir um baseline antes do TensorFlow;
- avaliar modelos com accuracy, precision, recall, F1-score, matriz de confusão e análise de erros;
- adicionar testes, pipeline e interface quando forem implementados.

## 👨‍💻 Autor

**Robert Melo**

🔗 LinkedIn: [linkedin.com/in/robertdemelo](https://www.linkedin.com/in/robertdemelo/)

🐍 Python | Pandas | NumPy | Matplotlib | Machine Learning | Análise Exploratória de Dados
