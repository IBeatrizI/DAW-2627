# Cartão 1.1 — Caracterização dos Atores, Regras de Negócio e Requisitos

**Projeto:** Ferramenta de Gestão de Presenças em Contexto Letivo  
**Unidade curricular:** Desenvolvimento de Aplicações Web  
**Fase:** Análise e Desenho  
**Estado:** Revisto (v2.1) — a validar pelo grupo

---

## 1. Objetivo

Este documento caracteriza os quatro atores do sistema, define as regras de negócio que condicionam os casos de uso e reúne os requisitos não funcionais da aplicação. A caracterização distingue os objetivos, as permissões, as restrições e as interações diretas ou indiretas de cada ator.

## 2. Caracterização dos atores

### 2.1. Docente

**Tipo:** Ator principal  
**Casos de uso:** UC1, UC2, UC3 e UC4 (este último limitado às suas unidades curriculares)

**Descrição:**  
Docente responsável por uma ou mais unidades curriculares (UC), encarregado de criar as pautas de presenças, registar a assiduidade dos alunos e encerrar os registos semanais. Pode ainda analisar a assiduidade das UC pelas quais é responsável, em formato numérico e gráfico.

**Objetivos**
- Criar pautas para as UC pelas quais é responsável.
- Organizar as aulas das 15 semanas letivas e associar as respetivas salas.
- Registar a situação de cada aluno em cada aula (presente, ausente ou falta justificada).
- Rever os registos e encerrar cada semana letiva.
- Consultar a evolução da assiduidade das suas UC ao longo das 15 semanas.

**Permissões**
- Consultar as UC pelas quais é responsável.
- Criar e consultar as respetivas pautas.
- Registar e corrigir presenças enquanto a semana estiver aberta.
- Rever e confirmar os registos antes do encerramento semanal.
- Consultar indicadores de assiduidade (UC4) exclusivamente das UC que lhe estão atribuídas.

**Restrições**
- Só gere as pautas das UC que lhe estão atribuídas.
- Não pode alterar os registos de uma semana encerrada (RN05).
- Não acede a funcionalidades reservadas a outros perfis, nomeadamente ao painel de *Data Analytics* (UC5).

**Interações**
- **Diretas:** criação de pautas (UC1), registo de presenças (UC2), encerramento e criação do histórico semanal (UC3) e consulta da assiduidade das suas UC (UC4).
- **Indiretas:** os históricos semanais que produz alimentam a análise realizada por outros perfis no UC4.

### 2.2. Técnico do Gabinete de Qualidade

**Tipo:** Ator principal  
**Casos de uso:** UC4 e UC5

**Descrição:**  
Utilizador responsável pela consulta e análise dos dados de assiduidade da escola a que está vinculado, bem como pela análise das estatísticas de utilização da plataforma, apoiando a melhoria dos processos académicos.

**Objetivos**
- Consultar os históricos de assiduidade da sua escola.
- Analisar a evolução das presenças ao longo das 15 semanas letivas.
- Comparar indicadores entre cursos e unidades curriculares da sua escola.
- Consultar estatísticas de utilização da aplicação.
- Identificar padrões de utilização e oportunidades de melhoria.

**Permissões**
- Consultar indicadores de assiduidade em formato numérico e gráfico.
- Filtrar os resultados por curso, UC, ano curricular e ano letivo.
- Consultar páginas visualizadas, duração das visitas, utilizadores ativos por perfil e funcionalidades mais utilizadas.
- Aceder ao painel de controlo de *Data Analytics*.

**Restrições**
- Não altera os registos de presenças efetuados pelos docentes.
- Os indicadores de assiduidade baseiam-se exclusivamente nos históricos semanais produzidos pelo UC3.
- O acesso aos dados limita-se à escola a que o técnico está vinculado (RN06 e RNF04).

**Interações**
- **Diretas:** consulta e análise dos registos de assiduidade (UC4) e análise dos dados de utilização do sistema (UC5).
- **Indiretas:** utiliza os históricos semanais gerados no UC3 e os dados de atividade recolhidos automaticamente pela aplicação.

### 2.3. Dirigente

**Tipo:** Ator de consulta  
**Caso de uso:** UC4

**Descrição:**  
Diretor de uma escola ou membro da Presidência, que utiliza os indicadores de assiduidade para apoiar decisões de gestão académica e de planeamento da oferta formativa. O âmbito de acesso depende do cargo (RN06):
- **Diretor de escola:** acede apenas aos dados da escola pela qual é responsável.
- **Membro da Presidência:** acede aos dados de todas as escolas.

**Objetivos**
- Consultar indicadores de assiduidade dos alunos.
- Comparar a assiduidade entre cursos e unidades curriculares (e, no caso da Presidência, entre escolas).
- Acompanhar a evolução das taxas de frequência ao longo das semanas letivas.
- Apoiar decisões relacionadas com o número de turmas.
- Analisar a relação entre assiduidade e sucesso académico.

**Permissões**
- Consultar tabelas e gráficos de assiduidade dentro do seu âmbito de acesso.
- Aplicar filtros por escola (apenas a Presidência), curso, UC, ano curricular e ano letivo.
- Consultar indicadores consolidados a partir dos históricos semanais.

**Restrições**
- Não cria pautas nem regista ou altera presenças.
- Não encerra semanas letivas.
- Não acede ao painel de *Data Analytics*, uma vez que o UC5 é atribuído ao Técnico do Gabinete de Qualidade.

**Interações**
- **Diretas:** consulta e análise dos registos de assiduidade (UC4).
- **Indiretas:** consulta indicadores produzidos a partir dos históricos semanais gerados no UC3.

### 2.4. Aluno

**Tipo:** Ator indireto  
**Interação associada:** UC1 e UC2, sem casos de uso próprios nesta fase

**Descrição:**  
Aluno inscrito numa UC num determinado ano letivo, cujos dados de inscrição permitem a inclusão na pauta de presenças e cujos registos de assiduidade são efetuados pelo docente.

**Objetivos**
- Estar corretamente identificado na pauta da UC em que está inscrito.
- Ter a sua situação de assiduidade registada corretamente.

**Permissões**
- A proposta não define permissões de interação direta para o aluno.
- Os dados da inscrição são utilizados na criação das pautas.
- A situação de assiduidade é registada pelo docente.

**Restrições**
- Não cria nem altera pautas.
- Não regista nem modifica diretamente as presenças.
- Não encerra semanas letivas.
- Não dispõe de casos de uso próprios nesta fase do projeto.

**Interações**
- **Indiretas:** inclusão na pauta durante o UC1 e registo da situação de assiduidade pelo docente durante o UC2.

> Funcionalidades como consultar as próprias faltas, justificar ausências ou receber notificações não estão previstas na proposta e não são incluídas como requisitos.

## 3. Resumo dos atores

| Ator | Casos de uso | Responsabilidade principal | Âmbito de dados | Interação |
|---|---|---|---|---|
| Docente | UC1, UC2, UC3, UC4 | Criar pautas, registar presenças, encerrar semanas e analisar as suas UC | Suas UC | Direta |
| Técnico do Gabinete de Qualidade | UC4, UC5 | Analisar assiduidade e utilização do sistema | Sua escola | Direta |
| Dirigente | UC4 | Consultar indicadores para apoio à decisão | Sua escola (diretor) ou todas (Presidência) | Direta |
| Aluno | UC1 e UC2 (associado) | Ser incluído na pauta e ter a assiduidade registada | — | Indireta |

## 4. Regras de negócio

As regras seguintes são transversais aos casos de uso e são referenciadas nas respetivas especificações.

| ID | Regra | Descrição |
|---|---|---|
| RN01 | Estrutura da pauta | Cada pauta está associada a uma turma, que identifica a UC e o ano letivo (o ano curricular decorre da UC). Só pode existir uma pauta por turma. |
| RN02 | Estrutura das aulas | Uma pauta tem 15 semanas letivas. Cada semana tem uma ou mais aulas, definidas por data, hora de início, hora de fim, tipo (T, TP ou PL) e sala. |
| RN03 | Situações de assiduidade | Em cada aula, cada aluno tem uma de três situações: presente, ausente ou falta justificada. |
| RN04 | Taxa de frequência | Taxa de frequência da semana = presenças ÷ total de registos (presenças + ausências + faltas justificadas) × 100. A falta justificada conta no total como falta, mas é contabilizada separadamente no histórico. |
| RN05 | Encerramento semanal | Uma semana só pode ser encerrada se todas as aulas dessa semana tiverem situação registada para todos os alunos. O encerramento é absoluto e irreversível: não existem correções excecionais. |
| RN06 | Âmbito de acesso | Docente: apenas as suas UC. Técnico do Gabinete de Qualidade e diretor de escola: apenas a sua escola. Membro da Presidência: todas as escolas. O âmbito é verificado no servidor (API) em todos os pedidos. |
| RN07 | Dados mestre | Escolas, cursos, UC, turmas, salas, alunos, inscrições, resultados finais e contas de utilizador são carregados previamente (importação ou *seed*). A sua gestão está fora do âmbito desta fase. |
| RN08 | Sucesso académico | O resultado final de cada inscrição (nota ou aprovação) é um dado mestre importado e é usado no UC4 para relacionar a taxa de frequência com o sucesso académico. |

## 5. Requisitos não funcionais

| ID | Categoria | Requisito | Origem |
|---|---|---|---|
| RNF01 | Responsividade | A interface deve adaptar-se a computadores de secretária, portáteis, tablets e smartphones. | Enunciado |
| RNF02 | Usabilidade | O registo de presenças deve ser simples e prático durante as aulas, incluindo em ecrãs pequenos. | Grupo |
| RNF03 | Segurança | O sistema deve autenticar os utilizadores, guardar as palavras-passe com *hashing* seguro e terminar automaticamente as sessões após 30 minutos de inatividade. | Grupo |
| RNF04 | Controlo de acesso | O acesso aos dados é condicionado pelo perfil e pelo âmbito definido na RN06, com verificação no servidor. Pedidos fora do âmbito devolvem erro HTTP 403. | Grupo |
| RNF05 | Integridade dos dados | O encerramento semanal aplica um bloqueio absoluto e irreversível aos registos de assiduidade e é executado numa única transação. | Grupo |
| RNF06 | Suporte a múltiplos contextos | A aplicação deve suportar várias escolas, cursos, UC, turmas, anos curriculares e anos letivos. | Enunciado |
| RNF07 | Compatibilidade | O *frontend* (HTML/CSS) deve funcionar nos navegadores modernos (Chrome, Firefox, Safari e Edge). | Grupo |
| RNF08 | Desempenho | O tempo de resposta da API não deve exceder 500 ms e as vistas e tabelas devem ser apresentadas em menos de 2 segundos. | Grupo |
| RNF09 | Fiabilidade | O sistema deve reduzir o risco de perda de dados durante a criação, edição e encerramento das pautas, nomeadamente em caso de expiração de sessão. | Grupo |
| RNF10 | Privacidade | O acesso aos dados pessoais e académicos deve limitar-se às necessidades e permissões de cada perfil. | Grupo |
| RNF11 | Recolha de métricas | O sistema deve recolher automaticamente dados de utilização (páginas visualizadas, duração das visitas, utilizador e funcionalidade utilizada, de que decorrem o perfil e a escola) para suportar o UC5. | Enunciado |
| RNF12 | Arquitetura e manutenibilidade | A solução deve seguir a arquitetura MVC e disponibilizar uma API REST para os dados e regras de negócio. | Enunciado |
| RNF13 | Rastreabilidade | O sistema deve registar as operações críticas (encerramento de semanas, tentativas de acesso fora do âmbito e autenticações falhadas), indicando o utilizador, a data e a hora. | Grupo |

## 6. Decisões de projeto

| N.º | Decisão | Justificação |
|---|---|---|
| D1 | O diretor de escola e o técnico do gabinete de qualidade acedem apenas aos dados da sua escola; a Presidência acede a todas as escolas. | O enunciado inclui a Presidência entre os dirigentes, que não pertence a uma única escola. A separação por escola protege a privacidade (RN06). |
| D2 | O docente pode consultar a assiduidade das suas UC (UC4). | O enunciado indica que docentes e técnicos podem visualizar e analisar as presenças em modo numérico ou gráfico. |
| D3 | O encerramento semanal é absoluto e irreversível. | Garante a integridade do histórico que alimenta o UC4 (RN05). |
| D4 | A falta justificada conta como falta no cálculo da taxa de frequência, mas é registada separadamente. | Mantém a taxa como medida de presença efetiva e preserva a informação sobre justificações (RN04). |
| D5 | Introduz-se a entidade turma. | Permite apoiar a decisão sobre o número de turmas, objetivo indicado no enunciado (RN01). |
| D6 | O resultado final das inscrições é um dado importado. | Permite analisar a relação entre assiduidade e sucesso académico sem acrescentar casos de uso (RN08). |
| D7 | Limites de desempenho: 500 ms na API e 2 s nas vistas. | Requisitos mensuráveis e verificáveis na fase de implementação (RNF08). |
| D8 | Palavras-passe com *hashing*, sessões com *timeout* de 30 minutos e registo de operações críticas. | Responde ao risco do bloqueio irreversível e à rastreabilidade prometida na proposta (RNF03 e RNF13). |
| D9 | Compatibilidade com Chrome, Firefox, Safari e Edge. | Cobre os navegadores modernos mais usados em computadores e dispositivos móveis (RNF07). |
| D10 | Os dados mestre e as contas de utilizador são carregados previamente. | Mantém o foco nos quatro casos de uso do domínio e no UC5 (RN07). |

## 7. Texto de síntese

A ferramenta de gestão de presenças em contexto letivo contempla quatro atores: Docente, Técnico do Gabinete de Qualidade, Dirigente e Aluno. Cada ator desempenha um papel específico, de acordo com as suas responsabilidades e com o âmbito de dados que lhe está atribuído.

O Docente é responsável pela criação das pautas, pelo registo da assiduidade dos alunos e pelo encerramento semanal dos registos, podendo também analisar a assiduidade das suas unidades curriculares. O Técnico do Gabinete de Qualidade consulta e analisa os históricos de assiduidade da sua escola e acompanha as estatísticas de utilização da plataforma. O Dirigente, seja diretor de escola ou membro da Presidência, consulta os indicadores de assiduidade para apoiar decisões de gestão académica, nomeadamente o planeamento do número de turmas. O Aluno participa indiretamente no sistema, através da sua inclusão nas pautas e do registo da respetiva situação de assiduidade pelo docente.

A aplicação disponibiliza uma interface responsiva, adequada a computadores, tablets e smartphones, assegura a autenticação dos utilizadores, limita o acesso aos dados de acordo com o perfil e suporta múltiplas escolas, cursos, unidades curriculares, turmas, anos curriculares e anos letivos. Mantém ainda a integridade e a rastreabilidade dos registos e recolhe dados de utilização para a componente de *Data Analytics*.
