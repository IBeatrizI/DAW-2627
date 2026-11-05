# Perfis e permissões — justificação da modelação

O diagrama UML distingue os atores **Docente**, **Técnico do Gabinete de Qualidade** e **Dirigente**; este último é especializado em **Diretor de escola** e **Presidência**. O **Aluno** é um interveniente indireto nesta fase.

Na base de dados, os profissionais autenticados partilham a tabela `utilizador` e são diferenciados através de `utilizador.id_perfil` → `perfil.id_perfil`. O modelo evita a duplicação de campos como nome, email, palavra-passe e estado da conta em tabelas de profissão separadas.

| Perfil no sistema | Código esperado em `perfil.codigo` | Âmbito e funcionalidades |
|---|---|---|
| Docente | `docente` | UC1, UC2, UC3 e UC4, nas UC e anos letivos atribuídos |
| Técnico | `tecnico_qualidade` | UC4 e UC5, no âmbito da respetiva escola |
| Diretor de escola | `diretor_escola` | UC4, limitado à escola dirigida |
| Presidência | `presidencia` | UC4, para as escolas da instituição |

O vínculo dos docentes às unidades curriculares e aos anos letivos é representado por `atribuicao_uc`. A relação `atribuicao_uc.id_docente` → `utilizador.id_utilizador` **não** garante automaticamente que a conta é de um Docente: cabe à aplicação validar o perfil e as atribuições antes de permitir operações. O âmbito deve igualmente ser verificado no servidor, mesmo quando o menu já oculta funcionalidades não autorizadas.

Esta solução é adequada ao âmbito atual, que prevê **um perfil por utilizador**. Se, numa fase futura, uma pessoa precisar de vários perfis em simultâneo, poderá ser necessário representar uma relação N:M entre utilizadores e perfis.

**Referências internas:** [01 — Atores e requisitos](01-atores-requisitos.md), [02 — Casos de uso](02-casos-de-uso.md), [03 — Modelo de dados](03-base-de-dados.md).
