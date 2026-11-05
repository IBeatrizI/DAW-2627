# Cartão 1.2 — Diagrama de Casos de Uso e Especificações UML

**Projeto:** Ferramenta de Gestão de Presenças em Contexto Letivo  
**Unidade curricular:** Desenvolvimento de Aplicações Web  
**Fase:** Análise e Desenho  
**Estado:** Sincronizado com o relatório entregue e os protótipos finais

---

## 1. Objetivo

Este documento especifica os cinco casos de uso do sistema de Gestão de Presenças em Contexto Letivo: quatro do domínio do problema (UC1 a UC4) e um de *data analytics* (UC5). As especificações integram as regras de negócio (RN) e os requisitos não funcionais (RNF) definidos no Cartão 1.1.

## 2. Diagrama de casos de uso (UML)

O diagrama UML representa **os cinco casos de uso e os respetivos atores com interação direta numa única fronteira de sistema**. O Aluno é uma entidade do domínio e um interveniente indireto, mas não inicia operações na aplicação nesta fase; por isso não é ligado artificialmente aos casos de uso no diagrama UML. Diretor de escola e Presidência são dois perfis de Dirigente, ambos associados ao UC4.

![Diagrama UML dos cinco casos de uso](../../diagrams/casos-de-uso.png)

**Nota de notação:** as linhas contínuas representam associações ator–caso de uso. O encadeamento entre UC1–UC4 é uma dependência **dos dados produzidos**, explicada na secção 2.1, e não uma relação UML `<<include>>`/`<<extend>>`. O UC5 utiliza registos de atividade recolhidos automaticamente ao utilizar a aplicação e não depende do encerramento semanal.

### 2.1. Encadeamento dos casos de uso

| UC | Designação | Ator principal | Entrada | Resultado |
|---|---|---|---|---|
| UC1 | Criação da pauta de presenças | Docente | UC, turma, ano letivo e alunos inscritos | Pauta com 15 semanas inicialmente sem aulas; aulas adicionadas depois |
| UC2 | Registo de presenças na pauta | Docente | Pauta criada no UC1 | Presenças por aula |
| UC3 | Encerramento e histórico semanal | Docente | Presenças registadas no UC2 | Histórico semanal de assiduidade |
| UC4 | Consulta e análise da assiduidade | Docente, Técnico do Gabinete de Qualidade e Dirigente | Históricos semanais do UC3 | Indicadores numéricos e gráficos |
| UC5 | Análise da utilização do sistema (*data analytics*) | Técnico do Gabinete de Qualidade | Registos de atividade dos utilizadores | Estatísticas e painel de controlo |

## 3. Especificação detalhada dos casos de uso

### UC1: Criação da pauta de presenças

| Campo | Especificação |
|:--|:--|
| **Ator principal** | Docente. O Aluno é apenas interveniente indireto. |
| **Objetivo** | Criar uma pauta para uma turma atribuída ao docente e permitir o planeamento das aulas ao longo das 15 semanas. |
| **Pré-condições** | O docente está autenticado; a UC, turma, ano letivo, alunos, inscrições e atribuições docentes existem como dados académicos previamente importados. |
| **Fluxo principal** | 1. Aceder a «Gestão de pautas» e selecionar «Nova pauta».<br>2. Abrir o modal de criação.<br>3. Selecionar UC, ano letivo e turma já importados.<br>4. Validar e criar a pauta com **15 semanas inicialmente sem aulas**.<br>5. Abrir a pauta no calendário semanal.<br>6. Selecionar «Adicionar aula» e preencher data, horário, tipo e sala.<br>7. Validar e adicionar a aula ao calendário. |
| **Fluxos alternativos** | **3a.** Já existe uma pauta para a turma: impedir a duplicação.<br>**6a.** Conflito de horário ou sala: apresentar aviso no modal e **preservar os campos preenchidos**.<br>**6b.** A semana está encerrada: impedir o planeamento. |
| **Pós-condições** | A pauta está disponível para consulta e planeamento, com 15 semanas e as aulas que tenham sido adicionadas. |

---

### UC2: Registo de presenças na pauta

| Campo | Especificação |
| :---- | :---- |
| **Identificador e nome** | **UC2** — Registo de presenças na pauta |
| **Atores** | Principal: Docente. Indireto: Aluno (a sua situação é registada pelo docente). |
| **Descrição** | Em cada aula, o docente abre a pauta e regista a situação de cada aluno (presente, ausente ou falta justificada) numa interface simples, responsiva e compatível com os navegadores modernos. Os registos podem ser corrigidos enquanto a semana estiver aberta. |
| **Requisitos associados** | RN03, RN05, RN09, RNF01, RNF02, RNF05, RNF07, RNF08, RNF09 |
| **Pré-condições** | 1. O docente tem sessão ativa e está atribuído à UC **no ano letivo da pauta**.<br>2. A pauta foi criada no UC1.<br>3. A semana da aula está no estado "Aberta". |
| **Pós-condições** | A situação de cada aluno em cada aula fica guardada, pronta a ser consolidada no UC3. |
| **Fluxo principal** | 1. O docente abre uma pauta.<br>2. Seleciona a semana letiva e a aula.<br>3. O sistema apresenta a lista de alunos numa grelha adaptada a ecrãs pequenos, com a situação já registada (se existir).<br>4. O docente define a situação de cada aluno.<br>5. O docente seleciona "Guardar registos".<br>6. O sistema grava os registos e apresenta uma confirmação visual. |
| **Fluxos alternativos e exceções** | **2a. A semana está encerrada:** a grelha é apresentada apenas em modo de leitura e a API rejeita qualquer gravação (RN05).<br>**4a. O docente corrige um registo já guardado:** o sistema atualiza a situação do aluno, desde que a semana continue aberta.<br>**4b. A aula ainda não ocorreu (data futura):** o sistema não permite registar presenças e informa o docente.<br>**6a. A sessão expira antes de guardar:** o sistema pede nova autenticação e preserva os registos preenchidos, evitando a sua perda (RNF09).<br>**6b. Falha de comunicação com a API:** o sistema informa o docente de que os registos não foram guardados e permite tentar novamente. |

---

### UC3: Encerramento e criação do histórico semanal

| Campo | Especificação |
| :---- | :---- |
| **Identificador e nome** | **UC3** — Encerramento e criação do histórico semanal |
| **Atores** | Principal: Docente. |
| **Descrição** | No final de cada semana, o docente revê os registos e encerra a semana. A operação é irreversível e gera o histórico semanal com o número de presenças, de faltas e de faltas justificadas e a taxa de frequência da UC (RN04). |
| **Requisitos associados** | RN04, RN05, RN09, RNF03, RNF05, RNF09, RNF13 |
| **Pré-condições** | 1. O docente tem sessão ativa e está atribuído à UC **no ano letivo da pauta**.<br>2. A semana está no estado "Aberta".<br>3. Todas as aulas da semana têm situação registada para todos os alunos (UC2). |
| **Pós-condições** | 1. A semana passa irreversivelmente ao estado "Encerrada" e os seus registos ficam bloqueados.<br>2. É gerado o histórico semanal, que serve de entrada ao UC4.<br>3. O encerramento fica registado (utilizador, data e hora). |
| **Fluxo principal** | 1. O docente abre a pauta e seleciona "Encerrar semana".<br>2. O sistema apresenta um resumo com os totais de presenças, ausências, faltas justificadas e a taxa de frequência.<br>3. O sistema avisa que o encerramento é definitivo e pede a reintrodução da palavra-passe.<br>4. O docente confirma o encerramento e introduz a palavra-passe.<br>5. O sistema valida a palavra-passe, encerra a semana, grava o histórico numa única transação e apresenta uma mensagem de sucesso. |
| **Fluxos alternativos e exceções** | **1a. Existem aulas ou alunos sem situação registada:** o sistema lista as lacunas e não permite o encerramento até estarem preenchidas (RN05).<br>**2a. O docente deteta incoerências no resumo:** cancela a operação, a semana mantém-se aberta e regressa ao UC2 para corrigir.<br>**4a. A palavra-passe está incorreta:** o sistema recusa o encerramento e regista a tentativa falhada.<br>**5a. Falha durante a gravação:** a transação é anulada, a semana mantém-se aberta e o docente é informado. |

---

### UC4: Consulta e análise da assiduidade

| Campo | Especificação |
| :---- | :---- |
| **Identificador e nome** | **UC4** — Consulta e análise da assiduidade |
| **Atores** | Principais: Docente (UC **e anos letivos** atribuídos), Técnico do Gabinete de Qualidade (a sua escola) e Dirigente (diretor de escola: a sua escola; Presidência: todas as escolas). |
| **Descrição** | O utilizador consulta os históricos semanais em tabelas e gráficos, com filtros por escola (apenas Presidência), curso, UC, ano curricular e ano letivo. Permite analisar a evolução da taxa de frequência ao longo das 15 semanas, comparar UC e relacionar a assiduidade com o sucesso académico (RN08). |
| **Requisitos associados** | RN04, RN06, RN08, RN09, RNF01, RNF04, RNF06, RNF08, RNF10, RNF13 |
| **Pré-condições** | 1. O utilizador tem sessão ativa.<br>2. Existem históricos semanais gerados (UC3) dentro do âmbito do utilizador. |
| **Pós-condições** | Os indicadores ficam apresentados em formato numérico e gráfico, dentro do âmbito de acesso do utilizador. |
| **Fluxo principal** | 1. O utilizador acede a "Indicadores de Assiduidade".<br>2. O sistema determina o âmbito de acesso a partir do perfil e dos dados da sessão (RN06).<br>3. O utilizador define os filtros disponíveis dentro desse âmbito.<br>4. O sistema consulta a API e apresenta tabelas numéricas e gráficos, incluindo a evolução semanal da taxa de frequência e a comparação entre UC.<br>5. Para a análise do sucesso académico, o sistema cruza as presenças individuais das semanas encerradas com os resultados importados das inscrições (RN08), sem misturar dados de semanas ainda abertas. |
| **Fluxos alternativos e exceções** | **3a. Os filtros não produzem resultados:** o sistema apresenta uma mensagem informativa e sugere alterar os filtros.<br>**3b. O utilizador tenta aceder, por URL ou pela API, a dados fora do seu âmbito:** o servidor recusa o pedido com erro HTTP 403 e regista a tentativa (RNF04 e RNF13).<br>**4a. Falha na obtenção dos dados:** o sistema informa que os indicadores não estão disponíveis e permite tentar novamente. |

---

### UC5: Análise da utilização do sistema (*data analytics*)

| Campo | Especificação |
| :---- | :---- |
| **Identificador e nome** | **UC5** — Análise da utilização do sistema (*data analytics*) |
| **Atores** | Principal: Técnico do Gabinete de Qualidade. |
| **Descrição** | O sistema recolhe automaticamente dados de atividade dos utilizadores e o técnico analisa-os num painel de controlo: páginas visualizadas, duração das visitas, utilizadores ativos por perfil e período e funcionalidades mais utilizadas. Os dados limitam-se à escola do técnico. |
| **Requisitos associados** | RN06, RNF03, RNF04, RNF08, RNF11 |
| **Pré-condições** | 1. O técnico tem sessão ativa.<br>2. O sistema já recolheu registos de atividade (fluxo automático descrito abaixo). |
| **Pós-condições** | O painel de controlo apresenta as estatísticas de utilização atualizadas da escola do técnico. |
| **Fluxo automático de recolha** | Em cada navegação autenticada, o sistema inicia um registo da página e funcionalidade com instante de entrada; a duração só é estimada após mudança de página, saída ou sinal de atividade da sessão (com limite de inatividade). Uma requisição HTTP isolada não permite conhecer, por si só, o tempo de permanência (RNF11). |
| **Fluxo principal** | 1. O técnico acede a "Data Analytics — Utilização do Sistema".<br>2. Seleciona o período de análise (por exemplo, dia, semana ou mês).<br>3. O sistema filtra os registos de atividade pela escola do técnico (RN06).<br>4. O sistema apresenta as páginas mais visualizadas, a duração média das visitas, o número de utilizadores ativos por perfil e as funcionalidades mais utilizadas, em tabelas e gráficos. |
| **Fluxos alternativos e exceções** | **3a. Não existem registos no período selecionado:** o sistema apresenta uma mensagem informativa.<br>**4a. Falha na obtenção dos registos de atividade:** o sistema informa que as métricas não estão disponíveis e regista a falha. |


## 4. Adaptação aos wireframes finais (05/11/2026)

Os artefactos finais dos [cinco UC](04-prototipos.md) permitem observar, além dos fluxos normais, estados e validações: gravação de presenças e confirmação no UC2, edição de aula como operação opcional e eliminação bloqueada; resumo e confirmação do encerramento no UC3; diferentes âmbitos de consulta no UC4; consulta mensal, mudança do período e ausência de dados no UC5.

**Nota de rastreabilidade:** as imagens são uma revisão visual da fase de desenho. Não demonstram uma aplicação funcional. O modelo de dados correspondente está documentado em [03 — Base de dados](03-base-de-dados.md), e os perfis em [05 — Perfis e permissões](05-perfis-permissoes.md).
