![Header](https://capsule-render.vercel.app/api?type=rect&color=0:0f172a,100:0052cc&height=250&section=header&text=CAIO%20MELO%20BORGES&fontSize=50&fontColor=ffffff&textAlignY=40&desc=Computer%20Vision%20%C2%B7%20Deep%20Learning%20%C2%B7%20Medical%20Imaging&descAlignY=65&descSize=20)

<p align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&pause=1000&color=2196F3&center=true&vCenter=true&width=460&lines=Computer+Vision;Deep+Learning;Medical+Imaging+AI;Applied+Scientific+Research)](https://git.io/typing-svg)

</p>

<div align="center">

[English](#english-version) | [Português](#versão-em-português)

</div>

---

## English Version

Software Engineering student at the **University of Brasília (UnB)** and researcher in **computer vision for medical imaging**.

I own the computational core of a funded undergraduate research project (PIBIC) building a **Computer-Aided Diagnosis (CAD)** system for opportunistic osteoporosis screening from dental panoramic radiographs — a **two-stage CNN cascade** validated against DXA bone densitometry as the gold standard. I care about the part most portfolios skip: diagnosing *why* a model underperforms, and designing augmentation policies that respect the anatomy instead of copying defaults from natural-image benchmarks.

**Currently:**
- **Researcher (PIBIC)** — CAD system for osteoporosis screening, UnB × UNICEPLAC. Paper in preparation.
- **Innovation Fellow @ Ford Motor Company / IEL** — back-end and data architecture
- **Data Engineer @ Lab Livre / Gov Hub BR** — public policy evaluation data warehouse (Brazilian Ministry of Culture)
- Open to **remote international** and **Brazilian MedTech / AgTech** roles in CV and Deep Learning

---

### Tech Stack

**Deep Learning & Computer Vision**

<p align="center">

![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)
![TensorFlow](https://img.shields.io/badge/TensorFlow-FF6F00?style=for-the-badge&logo=tensorflow&logoColor=white)
![Keras](https://img.shields.io/badge/Keras-D00000?style=for-the-badge&logo=keras&logoColor=white)
![YOLOv8](https://img.shields.io/badge/Ultralytics%20YOLOv8-0B2E4F?style=for-the-badge)
![OpenCV](https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)

</p>

**Data & Infrastructure**

<p align="center">

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![PostgreSQL](https://img.shields.io/badge/postgresql-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Apache Airflow](https://img.shields.io/badge/Apache%20Airflow-017CEE?style=for-the-badge&logo=Apache%20Airflow&logoColor=white)
![dbt](https://img.shields.io/badge/dbt-FF694B?style=for-the-badge&logo=dbt&logoColor=white)
![Google BigQuery](https://img.shields.io/badge/BigQuery-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white)
![Docker](https://img.shields.io/badge/docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white)

</p>

---

### Featured Research

#### AI for Opportunistic Osteoporosis Screening on Panoramic Radiographs

**Undergraduate Research Fellowship (PIBIC) · UnB × UNICEPLAC School of Dentistry · 2024 – present**

Osteoporosis affects over **200 million people** and stays asymptomatic until the first fragility fracture. DXA — the gold standard — is expensive and almost never ordered for a patient without symptoms. Because the disease is systemic, it also erodes the mandibular cortex, which turns the **routine dental panoramic radiograph** into a viable opportunistic screening instrument.

**Two-stage CNN cascade:**

```
Panoramic radiograph → [De-identification] → Stage 1: YOLOv8 ROI detection
    → [Letterboxed 256×256 ROI extraction] → Stage 2: CNN → MCI class (C1/C2/C3)
```

**What I built and what came out of it:**

- **Designed and implemented** the full two-stage pipeline in PyTorch/Ultralytics and TensorFlow/Keras, grading mandibular cortical morphology (Mandibular Cortical Index) over a cohort of **1,030 radiographs** labeled by a specialist in Oral Radiology, with femoral-neck **DXA as the validation gold standard**
- **Trained a YOLOv8s detector** reaching **0.552 mAP@50** — disabling `mosaic`/`mixup` and enforcing `rect=True` as domain-specific augmentation choices, because composite and rescaled images destroy the craniofacial topographic reference the model needs
- **Diagnosed detector overfitting quantitatively**, tracing the root cause to a **parameter-to-sample ratio of ≈ 15,600:1** — which redefined the training strategy instead of triggering another blind round of hyperparameter tuning
- **Built the ROI extraction module** that auto-selects the best run by validation F1 and letterboxes crops to 256×256, **preserving 100% of the aspect ratio** — a resize would systematically distort the very cortical thickness being measured
- **Implemented the baseline classification CNN** at **71.8% validation accuracy** over 589 ROIs, and quantified the **7.2:1 class imbalance** as the limiting factor on the clinically decisive class
- **Engineered the LGPD-compliant de-identification pipeline** (footer cropping, EXIF/DICOM stripping, randomized renaming, encrypted offline key table), enabling **fully local, air-gapped training** on Apple Silicon GPU with zero patient-data exposure

**Next:** EfficientNet-B0 / ResNet-50 fine-tuning · stratified k-fold · blind test (n=30) · DXA correlation · Grad-CAM explainability · manuscript submission

`PyTorch` `TensorFlow` `YOLOv8` `Transfer Learning` `Medical Imaging` `OpenCV` `scikit-learn`

---

### Featured Experience

#### Data Engineer @ Lab Livre / Gov Hub BR — Brazilian Ministry of Culture

Analytical data warehouse supporting the evaluation of two national cultural funding policies.

- Built ingestion and modeling pipelines (**Airflow, dbt, PostgreSQL, Trino**) over legacy federal systems, consolidating **1,054,823 funding events and 255,337 cultural agents** into a 1993–2026 historical series
- Diagnosed and fixed an extraction-key defect that silently hid half the bank accounts per action plan — recovering **R$2.7 billion in transactions and 70,733 beneficiaries** invisible to the warehouse
- Applied **unidirectional-bias reasoning** to publish the indicator as an auditable **upper bound** before source completeness, unblocking delivery without compromising validity
- Implemented sensitive personal data handling under **LGPD** with deterministic hash anonymization

#### Innovation Fellow @ Ford Motor Company / IEL — Inova Talentos

Back-end and data architecture for an internal commercial services platform.

- Modeled the data domain from scratch in **Python/Django** (11 business models, 9 controlled enums), including a **16-state finite state machine** whose transition graph I validated by breadth-first search
- Designed the analytics layer on **BigQuery + dbt** (`raw → staging → marts → metrics`) with 8 KPIs canonically defined in SQL and idempotent incremental loads
- Specified the cost anomaly engine on **robust statistics (per-cohort median/MAD)** rather than generative inference — numerical reproducibility is non-negotiable in an auditable financial domain

---

### Other Projects

**DF em Obras — Public Infrastructure Transparency Pipeline**
Lead Data Engineer. Fault-tolerant ETL over unstable government APIs, modular dbt transformations, automated daily ingestion with Python and GitHub Actions.
→ [github.com/unb-mds/DFemObras](https://github.com/unb-mds/DFemObras)

---

## Versão em Português

Estudante de Engenharia de Software na **Universidade de Brasília (UnB)** e pesquisador em **Visão Computacional aplicada à imagem médica**.

Sou responsável pelo núcleo computacional de um projeto de Iniciação Científica (PIBIC) que desenvolve um sistema **CAD** (*Computer-Aided Diagnosis*) para triagem oportunística de osteoporose em radiografias panorâmicas odontológicas — um **pipeline em cascata de CNNs** validado contra densitometria óssea (DXA) como padrão-ouro. Meu interesse está justamente na parte que a maioria dos portfólios pula: diagnosticar *por que* um modelo não performa, e desenhar políticas de aumento de dados que respeitem a anatomia em vez de copiar defaults de benchmarks de imagens naturais.

**Atualmente:**
- **Pesquisador (PIBIC)** — sistema CAD para triagem de osteoporose, UnB × UNICEPLAC. Artigo em preparação.
- **Bolsista de Inovação @ Ford Motor Company / IEL** — back-end e arquitetura de dados
- **Engenheiro de Dados @ Lab Livre / Gov Hub BR** — data warehouse de avaliação de políticas públicas (Ministério da Cultura)
- Aberto a posições **remotas internacionais** e a **MedTechs / AgTechs** no Brasil em Visão Computacional e Deep Learning

---

### Pesquisa em Destaque

#### IA para Triagem Oportunística de Osteoporose em Radiografias Panorâmicas

**Iniciação Científica (PIBIC) · UnB × Odontologia UNICEPLAC · 2024 – presente**

A osteoporose afeta mais de **200 milhões de pessoas** e permanece assintomática até a primeira fratura por fragilidade. A DXA — padrão-ouro — é cara e praticamente nunca é solicitada para quem ainda não tem sintomas. Por ser sistêmica, a doença também corrói a cortical mandibular, o que transforma a **radiografia panorâmica de rotina** em um instrumento viável de triagem oportunística.

**Pipeline em cascata de dois estágios:**

```
Radiografia panorâmica → [Anonimização] → Estágio 1: detecção de ROI com YOLOv8
    → [Extração de ROI 256×256 por letterboxing] → Estágio 2: CNN → classe do ICM (C1/C2/C3)
```

**O que construí e o que resultou disso:**

- **Projetei e implementei** o pipeline completo de dois estágios em PyTorch/Ultralytics e TensorFlow/Keras, classificando a morfologia da cortical mandibular (Índice Cortical Mandibular) sobre amostra de **1.030 radiografias** rotuladas por especialista em Imaginologia Oral, com **DXA de colo do fêmur como padrão-ouro** de validação
- **Treinei um detector YOLOv8s** atingindo **mAP@50 de 0,552** — com `mosaic`/`mixup` desativados e `rect=True`, decisões de augmentação específicas do domínio médico, porque imagens compostas e redimensionadas destroem o referencial topográfico craniofacial de que o modelo precisa
- **Diagnostiquei quantitativamente o overfitting** do detector, isolando a causa-raiz na **razão parâmetros/amostras de ≈ 15.600:1** — o que redefiniu a estratégia de treino em vez de disparar mais uma rodada cega de ajuste de hiperparâmetros
- **Desenvolvi o módulo de extração de ROIs** que seleciona automaticamente a melhor execução por F1 de validação e centraliza os recortes em canvas 256×256 por letterboxing, **preservando 100% da razão de aspecto** — um resize distorceria sistematicamente a própria espessura cortical que está sendo medida
- **Implementei a CNN de classificação baseline** com **71,8% de acurácia de validação** sobre 589 ROIs, e quantifiquei o **desbalanceamento de 7,2:1** como fator limitante na classe clinicamente decisiva
- **Estruturei o pipeline de anonimização em conformidade com a LGPD** (recorte de rodapé, remoção de metadados EXIF/DICOM, renomeação aleatória, tabela de chaves criptografada offline), viabilizando treinamento **100% local e offline** em GPU Apple Silicon, sem exposição de dado de paciente

**Próximas etapas:** fine-tuning de EfficientNet-B0 / ResNet-50 · validação cruzada k-fold estratificada · teste cego (n=30) · correlação com DXA · explicabilidade por Grad-CAM · submissão do artigo

`PyTorch` `TensorFlow` `YOLOv8` `Transfer Learning` `Imagem Médica` `OpenCV` `scikit-learn`

---

### Experiência em Destaque

#### Engenheiro de Dados @ Lab Livre / Gov Hub BR — Ministério da Cultura

Data warehouse analítico que sustenta a avaliação de duas políticas nacionais de fomento cultural.

- Construí pipelines de ingestão e modelagem (**Airflow, dbt, PostgreSQL, Trino**) sobre sistemas legados de governo, consolidando **1.054.823 eventos de fomento e 255.337 agentes culturais** em série histórica de 1993 a 2026
- Diagnostiquei e corrigi uma falha de chave de extração que ocultava metade das contas bancárias por plano de ação — recuperando **R$ 2,7 bilhões em movimentação e 70.733 beneficiários** invisíveis no warehouse
- Apliquei **raciocínio de viés unidirecional** para publicar o indicador como **limite superior auditável** antes da completude das fontes, destravando a entrega sem comprometer a validade
- Implementei tratamento de dado pessoal sensível sob **LGPD**, com anonimização por hash determinístico

#### Bolsista de Inovação @ Ford Motor Company / IEL — Inova Talentos

Back-end e arquitetura de dados de uma plataforma interna de serviços comerciais.

- Modelei o domínio de dados do zero em **Python/Django** (11 modelos, 9 enumerações controladas), incluindo uma **máquina de estados de 16 estados** cujo grafo de transições validei por busca em largura
- Desenhei a camada analítica em **BigQuery + dbt** (`raw → staging → marts → metrics`) com 8 KPIs definidos canonicamente em SQL e cargas idempotentes e incrementais
- Especifiquei o motor de detecção de anomalias sobre **estatística robusta (mediana/MAD por coorte)** em vez de inferência generativa — reprodutibilidade numérica não é negociável em domínio financeiro auditável

---

### Outros Projetos

**DF em Obras — Pipeline de Transparência de Obras Públicas**
Lead Data Engineer. ETL tolerante a falhas sobre APIs governamentais instáveis, transformações modulares em dbt e ingestão diária automatizada com Python e GitHub Actions.
→ [github.com/unb-mds/DFemObras](https://github.com/unb-mds/DFemObras)

---

### Contato

<p align="center">

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/caio-melo-borges/)
[![Email](https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white)](mailto:caioborges250802@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/CaioMelo25)

</p>

---
