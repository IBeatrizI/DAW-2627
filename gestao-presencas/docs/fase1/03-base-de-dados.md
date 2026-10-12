# Cartão 1.3 - Modelação da Base de Dados (E/R e Lógico Relacional)

**Projeto:** Ferramenta de Gestão de Presenças em Contexto Letivo  
**Unidade curricular:** Desenvolvimento de Aplicações Web  
**Fase:** Análise e Desenho  
**Estado:** Rascunho para revisão do grupo

---

## 1. Objetivo

Este documento serve para detalhar as futuras tabelas para a criação da estrutura da Base de Dados a desenvolver. Serão também especificados os atributos de cada tabela, assim como as ligações entre as mesmas e as suas cardinalidades.

## 2. Definição das tabelas
### 2.1. Entidades

Abaixo está a lista de todas as possíveis entidades, definidas com base nos requisitos e casos de uso previamente estabelecidos nos cartões 1.1 e 1.2:

- **Utilizador\*:** Consiste num ator (docente, técnico de qualidade, dirigente/membro da presidência ou aluno) que pode interagir com a aplicação seja de que forma for, associado a um **perfil** e pertencente a uma **escola**.
- **Escola:** Representa uma escola de uma instituição que oferece vários **cursos**.
- **Curso:** Consiste numa licenciatura, mestrado ou qualquer outra oferta formativa por parte da **escola**. É composto por várias **UCs**.
- **Unidade Curricular (`UnidadeCurricular`):** Um conjunto de disciplinas lecionadas num ano letivo. Existem várias dentro de um **curso** e tem um **docente** e uma ou mais **turmas** (logo **pautas**) associadas.
- **Turma:** Conjunto de **alunos** associados a uma **UC** e a um ano letivo. Tem também associada uma única **pauta** (RN01).
- **Aluno:** Representa um estudante inscrito numa **turma** e, consequentemente, em **UCs**.
- **Sala:** Representa um espaço físico (como uma sala de aula, anfiteatro ou laboratório) com **aulas** associadas.
- **Pauta:** Estrutura de controlo da assiduidade associada a uma **UC** e uma **turma**. É composta por 15 **semanas letivas** (RN02).
- **Semana Letiva (`SemanaLetiva`):** Consiste num conjunto de (no máximo) 7 dias, sendo a peça de compõe uma pauta. Tem associadas várias **aulas**, que futuramente dá origem ao histórico semanal (RN04 e RN05).
- **Aula:** Pequenos períodos de tempo definidos por data, hora de início e fim, tipo e **sala**. Tem associadas as **presenças** de cada **aluno**.
- **Presença:** Consiste num único registo da situação de um aluno perante certa **aula** (presente, ausente, falta justificada) (RN03).
- **Histórico Semanal (`HistoricoSemanal`):** Dados consolidados com origem numa **semana letiva**, sendo composto por totais de presenças, faltas, faltas justificadas e taxa de frequência (RN04).
- **Registo de Atividades (`RegistoAtividades`):** Registo automático das atividades dos utilizadores que será utilizado para alimentar a secção de *Data Analytics* da aplicação a desenvolver.

\*Pode ser dividida em várias outras tabelas futuramente caso necessário.

### 2.2. Relações entre entidades

Com base nas entidades referidas acima, é possível criar uma "rede" composta por ligações entre as mesmas, assim como determinar as suas cardinalidades:

| Entidade 1 | Cardinalidade | Multiplicidade | Entidade 2 |
| :--- | :---: | :---: | :--- |
| `Escola`            | **1:N** | 1..\* | `Curso` |
| `Curso`             | **1:N** | 1..\* | `UnidadeCurricular` |
| `Docente`           | **N:M** | \*..\* | `UnidadeCurricular` |
| `UnidadeCurricular` | **1:N** | 1..\* | `Turma` |
| `Turma`             | **1:1** | 1..1| `Pauta` |
| `Pauta`             | **1:N** | 1..15 | `SemanaLetiva` |
| `SemanaLetiva`      | **1:N** | 0..\* | `Aula` |
| `Sala`              | **1:N** | 1..\* | `Aula` |
| `Aula`              | **1:N** | 1..\* | `Presenca` |
| `Aluno`             | **N:M** | \*..\* | `Turma` |
| `Escola`            | **1:N** | 1..\* | `Utilizador` |
| `Utilizador`        | **1:N** | 1..\* | `RegistoAtividade` |

#### 2.2.1. Breve explicação

- Numa `Escola`, podem ser lecionados um ou mais `Curso`, nos quais estão presentes uma ou mais `UnidadeCurricular`, cada uma lecionada por um ou mais `Docente`.
- Uma `UnidadeCurricular` pode ter uma ou mais `Turma` associadas. Cada `Turma` tem associada uma única `Pauta`, composta por no máximo 15 `SemanaLetiva`.
- Uma `SemanaLetiva` é composta por zero ou mais `Aula`, com uma ou mais `Presenca`.
- Mais do que uma `Aula` pode ser lecionada na mesma `Sala`.  
- Uma `Escola` tem zero ou mais `Utilizador` associados, cada um com um ou mais `RegistoAtividade`. 