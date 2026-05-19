# 🏢 GAC - Gestão de Ativos do CCT

## Documento de Visão e Elicitação de Requisitos

*Projeto de Engenharia de Requisitos Aplicada ao Contexto Educacional*

<img src="images/logo_gac.png" width="450" alt="GAC - Gestão de Ativos do CCT"/>

**Disciplina:** Requisitos e Modelagem de Sistemas
**Professor:** Marcelo Bezerra
**Grupo I:** Guilherme Machado Faria, Juan Carlos de Sousa Pereira, Victor Manuel Soares da Silva
**Data:** Maio de 2026 | **Versão:** 1.0
**Repositório:** [https://github.com/oshippai/requisitos-2026-gac-grupol](https://github.com/oshippai/requisitos-2026-gac-grupol)

---

# 1. Documento de Visão do Produto (Issue #1 - Sprint 1)

## O Problema

Atualmente, a locação de projetores (um total de 36 equipamentos) e chaves no CCT é realizada de forma estritamente manual. O processo envolve cadernos de registro físico, planilhas do Google e formulários de papel separados para a retirada e a devolução. Esse modelo operacional analógico gera dores constantes para a equipe de atendimento, resultando em atrasos, erros de anotação e alto índice de retrabalho. Além disso, a ausência de um sistema centralizado cria um "ponto cego" de controle visual, dificultando o rastreio ágil de pendências, como itens não devolvidos, danos físicos aos equipamentos ou a falta de acessórios essenciais (ex: cabos HDMI).

## A Solução Proposta

O sistema GAC (Gestão de Ativos do CCT) tem como objetivo principal digitalizar e unificar a gestão do inventário. A plataforma substituirá o controle em papel por um fluxo de trabalho ágil e digital, garantindo rastreabilidade em tempo real. Isso será alcançado através da implementação de um aceite digital de responsabilidade pelos docentes e de checklists técnicos parametrizados no momento da devolução.

---

# 2. Identificação de Stakeholders (Issue #2 - Sprint 1)

O mapeamento das partes interessadas envolvidas e afetadas pelo sistema GAC é composto por:

* **Direção Estratégica:** Prof. Jackson (Diretor do CCT).
* **Gestão Administrativa/Secretaria:** Fabiana (noite) e Marcia (manhã).
* **Corpo Operacional (Atendentes):** Kildery (Auxiliar Administrativo) e equipa de apoio de 5 auxiliares.
* **Suporte Técnico:** Equipa do DTEC, responsável pelas manutenções e validação dos checklists de hardware.
* **Usuários Finais:** Corpo docente (professores) que realiza a locação diária de ativos.

---

# 3. Elicitação: Roteiro e Resultados (Issues #3 e #4 - Sprint 1)

## Log de Entrevista Operacional

* **Entrevistado:** Kildery (Auxiliar Administrativo).
* **Contexto:** 2 anos de experiência no setor J02.

**Q1: Como descreve a rotina atual de retirada de equipamentos? (Issue #3)**

> **Resposta:** Hoje o fluxo é lento. O professor solicita o item, preenchemos um formulário físico manualmente e colhemos a assinatura no papel. É um processo burocrático e o manuseio de termos em papel gera desorganização.

**Q2: Quais são os problemas mais críticos na devolução? (Issue #4)**

> **Resposta:** Lidamos com não devolução no prazo, retornos com danos físicos não reportados e, com muita frequência, a falta de acessórios, principalmente cabos HDMI.

**Q3: O que traria melhoria imediata para o setor? (Issue #4)**

> **Resposta:** A adoção de tecnologia para facilitar a rotina. Precisamos de um checklist organizado por armário para validar o estado e o funcionamento real do equipamento na devolução.

---

# 4. Especificação de Requisitos e Regras (Sprint 2)

## 4.1. Requisitos Funcionais (Issue #5)

* **RF01:** O sistema deve possuir um cadastro centralizado dos 36 projetores e das chaves/salas do CCT.
* **RF02:** O sistema deve unificar os processos de retirada e devolução, eliminando formulários independentes.
* **RF03:** O sistema deve registrar acessórios (HDMI, USB) entregues com o projetor.
* **RF04:** O sistema deve permitir o preenchimento de um checklist técnico no momento da devolução.

## 4.2. Requisitos Não Funcionais (Issue #6)

* **RNF01 (Usabilidade):** Interface de "Fricção Zero" para garantir agilidade no balcão de retirada.
* **RNF02 (Segurança):** O aceite digital deve possuir a mesma validade institucional que o termo assinado atual.

## 4.3. Regras de Negócio (Issue #7)

* **RN01:** O projetor deve ser devolvido obrigatoriamente até o final do dia.
* **RN02:** É obrigatório o aceite do Termo de Responsabilidade para autorizar o empréstimo.
* **RN03:** O sistema deve gerir duas chaves por sala (original e reserva).

---

# 5. Backlog Inicial Priorizado (Issue #8 - Sprint 2)

| ID              | Descrição                                            | Prioridade       |
| :-------------- | :----------------------------------------------------- | :--------------- |
| **RF01**  | Cadastro centralizado de ativos (projetores e chaves)  | **Alta**   |
| **RF02**  | Unificação do fluxo de Retirada/Devolução          | **Alta**   |
| **RN02**  | Obrigatoriedade do aceite do Termo de Responsabilidade | **Alta**   |
| **RNF02** | Validação jurídica e segurança do aceite digital   | **Alta**   |
| **RF04**  | Checklist técnico no momento da devolução           | **Média** |
| **RN01**  | Regra de devolução obrigatória até o final do dia  | **Média** |
| **RN03**  | Controle de múltiplas chaves (Original e Reserva)     | **Média** |
| **RF03**  | Registro de acessórios (Cabo HDMI, USB, etc.)         | **Baixa**  |
| **RNF01** | Usabilidade com "Fricção Zero" (Interface rápida)   | **Baixa**  |

---

# 6. Modelagem UML (Issues #9, #10 e #11 - Sprint 2)

*Nota: Os diagramas visuais (Casos de Uso, Classes e Sequência) devem ser consultados na documentação PDF anexa ou exportados como imagem para a pasta `/images` do repositório.*

* **Diagrama de Casos de Uso:** Representa as interações entre os atores (Professor e Atendente) e o Sistema GAC.
* **Diagrama de Classes:** Modela as entidades principais do sistema (`Usuario`, `Equipamento`, `Emprestimo`, `Checklist`).
* **Diagrama de Sequência:** Detalha o fluxo principal de retirada e devolução do ativo no tempo.

---

# 7. Evidências e Anexos

* **Acesso do Professor:** Convite enviado e pendente para o colaborador `profBezerra` no repositório GitHub.

---

*Documento gerado para a P1 de Requisitos e Modelagem de Sistemas.* *Projeto GAC - Gestão de Ativos do CCT*
