# DAW-2627

# Ferramenta de Gestão de Presenças em Contexto Letivo

Projeto desenvolvido no âmbito da unidade curricular de **Desenvolvimento de Aplicações Web (DAW)** do Instituto Politécnico de Beja (Ano Letivo 2026/2027).

## 📌 Descrição do Projeto

Este projeto consiste no desenvolvimento de um sistema web centralizado para a gestão da assiduidade dos alunos. A solução visa resolver a morosidade e falta de fiabilidade dos registos manuais em papel ou ficheiros dispersos, oferecendo uma plataforma tecnológica onde os docentes podem gerir pautas e registar presenças, enquanto técnicos e dirigentes consultam indicadores agregados. 

O sistema assenta numa arquitetura com duas componentes principais: uma **API REST** (responsável pelos dados e regras de negócio) e uma **Aplicação Web MVC** (responsável pelas vistas do frontend e interação com o utilizador). O projeto integra ainda funcionalidades de *Data Analytics* para acompanhar estatísticas de atividade na plataforma.

## 🎯 Objetivos

* Desenvolver uma solução **multicurso, multiUC e preparada para vários anos curriculares**.
* Disponibilizar uma interface web **responsiva**, adaptada a computadores de secretária, tablets e smartphones (essencial para o uso do docente em sala de aula).
* Implementar acesso seguro e condicionado para os quatro atores principais: Docentes, Técnicos do Gabinete de Qualidade, Dirigentes e Alunos (indireto).
* Desenhar 5 casos de uso estruturais encadeados (onde o *output* de uma ação serve de *input* para a seguinte).
* Aplicar metodologias rigorosas de Engenharia de Software, abrangendo a modelação UML, desenho de base de dados e prototipagem de interfaces (Fase 1), seguidas da implementação (Fase 2).

## 📂 Estrutura do Repositório

O repositório encontra-se organizado para separar a documentação analítica, os diagramas estruturais e os protótipos de interface:

```text
gestao-presencas/
├── README.md                 # Este documento de apresentação do repositório
├── docs/                     # Documentação textual detalhada do projeto
│   ├── fase1/                # Elementos de Análise e Desenho (Entrega 1)
│   │   ├── 01-atores-requisitos.md  # Caracterização dos atores e levantamento de requisitos
│   │   ├── 02-casos-de-uso.md       # Tabelas de especificação UML detalhadas (UC1 a UC5)
│   │   ├── 03-base-de-dados.md      # Dicionário de dados, entidades e relações
│   │   └── 04-decisoes-projeto.md   # Justificações sobre arquitetura e stack tecnológica
│   └── fase2/                # Espaço reservado para documentação técnica da Implementação
├── diagrams/                 # Diagramas técnicos em formato código ou texto
│   ├── casos-de-uso.puml     # Diagrama de Casos de Uso (PlantUML)
│   ├── modelo-er.puml        # Modelo Entidade-Relacionamento (PlantUML)
│   └── modelo-relacional.md  # Especificação do Modelo Lógico Relacional (tabelas e chaves)
├── prototypes/               # Desenho de UI/UX
│   ├── wireframes/           # Esboços de baixa/média fidelidade dos ecrãs (Desktop/Mobile)
│   └── storyboards/          # Esquemas do fluxo de navegação entre os ecrãs
├── report/                   # Compilação dos documentos para o formato final
│   └── README.md             # Notas ou links para o relatório oficial (ex: Overleaf/LaTeX)
└── .gitignore                # Ficheiros temporários e pastas a serem ignorados pelo Git
```

## 👥 Equipa

* **Beatriz Caixeiro** (nº 21198)
* **Eduardo Madeira** (nº 26889)
