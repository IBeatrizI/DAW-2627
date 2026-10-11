# Cartão 1.1 — Caracterização dos Atores e Revisão de Requisitos

**Projeto:** Ferramenta de Gestão de Presenças em Contexto Letivo  
**Unidade curricular:** Desenvolvimento de Aplicações Web  
**Fase:** Análise e Desenho  
**Estado:** Validado

---

## 1. Objetivo

Esta secção caracteriza os quatro atores identificados na proposta do projeto e reúne os requisitos não funcionais relevantes para a aplicação. A caracterização distingue os objetivos, as permissões previstas e as interações diretas ou indiretas de cada ator.


## 2. Caracterização dos atores

### 2.1. Docente

**Tipo:** Ator principal  
**Casos de uso:** UC1, UC2 e UC3

**Descrição:**  
Docente responsável por uma ou mais unidades curriculares (UC), encarregado de criar as pautas de presenças, registar a assiduidade dos alunos e encerrar os registos semanais.

**Objetivos**
- Criar pautas para as unidades curriculares pelas quais é responsável.
- Organizar as aulas das 15 semanas letivas e associar as respetivas salas.
- Registar a situação de cada aluno em cada aula, incluindo presença, ausência ou falta justificada.
- Rever os registos e encerrar cada semana letiva.
- Produzir históricos semanais de assiduidade.

**Permissões previstas**
- Consultar as unidades curriculares pelas quais é responsável.
- Criar e consultar as respetivas pautas.
- Registar e corrigir presenças enquanto a semana estiver aberta.
- Rever e confirmar os registos antes do encerramento semanal.

**Restrições propostas**
- Gerir apenas as pautas das unidades curriculares que lhe estão atribuídas.
- Não alterar normalmente os registos de uma semana encerrada.
- Não aceder a funcionalidades reservadas a outros perfis, salvo se forem definidas permissões adicionais.

**Interações**
- **Diretas:** criação de pautas (UC1), registo de presenças (UC2) e encerramento e criação do histórico semanal (UC3).
- **Indiretas:** os históricos semanais produzidos servem de base à consulta e análise de assiduidade no UC4.

### 2.2. Técnico do Gabinete de Qualidade

**Tipo:** Ator principal  
**Casos de uso:** UC4 e UC5

**Descrição:**  
Utilizador responsável pela consulta e análise dos dados de assiduidade, bem como pela análise das estatísticas de utilização da plataforma, permitindo acompanhar o funcionamento do sistema e apoiar a melhoria dos processos académicos.

**Objetivos**
- Consultar os históricos de assiduidade.
- Analisar a evolução das presenças ao longo das 15 semanas letivas.
- Comparar indicadores entre escolas, cursos e unidades curriculares.
- Consultar estatísticas de utilização da aplicação.
- Identificar padrões de utilização e oportunidades de melhoria.

**Permissões previstas**
- Consultar indicadores de assiduidade em formato numérico e gráfico.
- Filtrar os resultados por escola, curso, unidade curricular, ano curricular e ano letivo.
- Consultar páginas visualizadas, duração das visitas, utilizadores ativos por perfil e funcionalidades mais utilizadas.
- Aceder ao painel de controlo de *Data Analytics*.

**Restrições propostas**
- Não alterar os registos de presenças efetuados pelos docentes.
- Os indicadores de assiduidade devem basear-se nos históricos semanais produzidos pelo UC3.
- O acesso aos dados deve respeitar as permissões atribuídas ao seu perfil.
- **O acesso aos dados restringe-se exclusivamente aos cursos da escola à qual o técnico está vinculado (não tem acesso global ao politécnico), assim como exclusivamente ao estabelecimento de ensino (escola, IP ou universidade) pelo qual é responsável.**

**Interações**
- **Diretas:** consulta e análise dos registos de assiduidade (UC4) e análise dos dados de utilização do sistema (UC5).
- **Indiretas:** utiliza os históricos semanais gerados no UC3 e os dados de atividade recolhidos automaticamente pela aplicação.

### 2.3. Dirigente

**Tipo:** Ator de consulta  
**Caso de uso:** UC4

**Descrição:**  
Diretor de uma escola ou membro da Presidência, que utiliza os indicadores de assiduidade para apoiar decisões de gestão académica e de planeamento da oferta formativa.

**Objetivos**
- Consultar indicadores de assiduidade dos alunos.
- Comparar a assiduidade entre cursos e unidades curriculares.
- Acompanhar a evolução das taxas de frequência ao longo das semanas letivas.
- Apoiar decisões relacionadas com o número de turmas.
- Analisar possíveis relações entre assiduidade e sucesso académico.

**Permissões previstas**
- Consultar tabelas e gráficos de assiduidade referentes à escola pela qual é responsável.
- Aplicar filtros de consulta por escola, curso, unidade curricular, ano curricular e ano letivo, de acordo com o âmbito de acesso atribuído.
- Consultar indicadores consolidados a partir dos históricos semanais.

**Restrições propostas**
- Não deve criar pautas nem registar ou alterar presenças.
- Não deve encerrar semanas letivas.
- Não necessita de acesso ao painel de Data Analytics, uma vez que a proposta atribui o UC5 ao Técnico do Gabinete de Qualidade.
- **O acesso é limitado apenas à escola pela qual é responsável.**

**Interações**
- **Diretas:** consulta e análise dos registos de assiduidade (UC4).
- **Indiretas:** consulta dos indicadores produzidos a partir dos históricos semanais gerados no UC3.

### 2.4. Aluno

**Tipo:** Ator indireto  
**Interação associada:** UC1 e UC2, sem casos de uso próprios nesta fase

**Descrição:**  
Aluno inscrito numa unidade curricular num determinado ano letivo, cujos dados de inscrição permitem a inclusão na pauta de presenças e cujos registos de assiduidade são efetuados pelo docente.

**Objetivos**
- Estar corretamente identificado na pauta da unidade curricular em que está inscrito.
- Ter a sua situação de assiduidade registada corretamente.

**Permissões**
- A proposta atual não define permissões de interação direta para o aluno.
- Os dados da inscrição são utilizados na criação das pautas.
- A situação de assiduidade é registada pelo docente.

**Restrições**
- Não cria nem altera pautas.
- Não regista nem modifica diretamente as presenças.
- Não encerra semanas letivas.
- Não dispõe de casos de uso próprios nesta fase do projeto.

**Interações**
- **Indiretas:** inclusão na pauta durante o UC1 e registo da situação de assiduidade pelo docente durante o UC2.

> Funcionalidades como consultar as próprias faltas, justificar ausências ou receber notificações não estão previstas na proposta atual e não são incluídas como requisitos.

## 3. Resumo dos atores

| Ator | Casos de uso | Responsabilidade principal | Interação |
|---|---|---|---|
| Docente | UC1, UC2, UC3 | Criar pautas, registar presenças e encerrar semanas | Direta |
| Técnico do Gabinete de Qualidade | UC4, UC5 | Analisar assiduidade e utilização do sistema | Direta |
| Dirigente | UC4 | Consultar indicadores para apoio à decisão | Direta |
| Aluno | Participação associada ao UC1 e UC2 | Ser incluído na pauta e ter a assiduidade registada | Indireta |

## 4. Requisitos não funcionais

A tabela distingue requisitos que decorrem diretamente da proposta/enunciado de requisitos propostos para validação pelo grupo.

| ID | Categoria | Requisito | Origem/estado |
|---|---|---|---|
| RNF01 | Responsividade | A interface deve adaptar-se a computadores de secretária, portáteis, tablets e smartphones. | Explícito no enunciado |
| RNF02 | Usabilidade | O registo de presenças deve ser simples e prático durante as aulas, incluindo em ecrãs pequenos. | Validado |
| RNF03 | Segurança | O sistema deve autenticar os utilizadores, utilizar *hashing* seguro para palavras-passe e gerir a expiração automática de sessões inativas. | Validado (Atualizado) |
| RNF04 | Controlo de acesso | O Dirigente e o Técnico de Qualidade têm o seu acesso estritamente limitado aos dados da Escola à qual pertencem. | Validado (Atualizado) |
| RNF05 | Integridade dos dados | O encerramento semanal aplica um bloqueio absoluto e irreversível aos registos de assiduidade. | Validado (Atualizado) |
| RNF06 | Suporte a múltiplos contextos | A aplicação deve suportar várias escolas, cursos, unidades curriculares, anos curriculares e anos letivos. | Explícito no enunciado |
| RNF07 | Compatibilidade | A aplicação (*frontend* HTML/CSS) deve ser *cross-browser*, garantindo total compatibilidade com os navegadores modernos. | Validado (Atualizado) |
| RNF08 | Desempenho | O tempo de resposta da API não deve exceder 500ms e as vistas/tabelas devem ser renderizadas em menos de 2 segundos. | Validado (Atualizado) |
| RNF09 | Fiabilidade | O sistema deve reduzir o risco de perda de dados durante a criação, edição e encerramento das pautas. | Validado |
| RNF10 | Privacidade | O acesso aos dados pessoais e académicos deve limitar-se às necessidades e permissões de cada perfil. | Validado |
| RNF11 | Recolha de métricas | O sistema deve recolher dados de utilização, incluindo páginas visualizadas e duração das visitas, para suportar o UC5. | Explícito no enunciado |
| RNF12 | Arquitetura e manutenibilidade | A solução deve seguir a arquitetura MVC e disponibilizar uma API REST para os dados e regras de negócio. | Explícito no enunciado |

## 5. Decisões de Projeto (Validadas)


1. **Âmbito de acesso do Dirigente:** pode consultar dados de todas as escolas ou apenas da escola pela qual é responsável?
2. **Âmbito de acesso do Técnico de Qualidade:** terá acesso global aos dados de todas as escolas e cursos?
- O Dirigente e o Técnico de Qualidade apenas visualizam os dados e cursos pertencentes à sua respetiva escola.
3. **Semanas encerradas:** o bloqueio é absoluto ou existe um procedimento autorizado para corrigir erros excecionais?
- O bloqueio da semana no UC3 é absoluto e irreversível (não há edições excecionais).
4. **Requisitos de desempenho:** será necessário definir limites mensuráveis para o tempo de resposta?
- Definido limite máximo de 500ms para a resposta dos *endpoints* da API.
5. **Segurança:** serão definidos requisitos adicionais para palavras-passe, sessões e registo de operações críticas?
- A aplicação exigirá o processamento seguro de palavras-passe (*hashing*) e *timeouts* para sessões inativas.
6. **Compatibilidade:** quais os navegadores que serão considerados no âmbito do projeto?
- A compatibilidade focada nos padrões HTML/CSS abrangendo todos os navegadores web modernos (Chrome, Firefox, Safari, Edge).

## 6. Texto de síntese

A ferramenta de gestão de presenças em contexto letivo contempla quatro atores: Docente, Técnico do Gabinete de Qualidade, Dirigente e Aluno. Cada ator desempenha um papel específico, de acordo com as suas responsabilidades e necessidades de acesso à informação.

O Docente é responsável pela criação das pautas, pelo registo da assiduidade dos alunos e pelo encerramento semanal dos registos. O Técnico do Gabinete de Qualidade consulta e analisa os históricos de assiduidade e acompanha as estatísticas de utilização da plataforma. O Dirigente consulta os indicadores de assiduidade para apoiar decisões de gestão académica, nomeadamente o planeamento do número de turmas. O Aluno participa indiretamente no sistema, através da sua inclusão nas pautas e do registo da respetiva situação de assiduidade pelo docente.

A aplicação deverá apresentar uma interface responsiva, adequada à utilização em computadores, tablets e smartphones, assegurar a autenticação dos utilizadores e suportar múltiplas escolas, cursos, unidades curriculares, anos curriculares e anos letivos. Deverá ainda manter a integridade dos registos e recolher dados de utilização para a componente de *Data Analytics*. As permissões detalhadas, os requisitos de desempenho e outros aspetos de segurança deverão ser validados pelo grupo antes da conclusão da fase de análise e desenho.
