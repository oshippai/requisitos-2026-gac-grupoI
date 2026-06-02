# Documento de Especificação de Requisitos de Software (SRS)
**Projeto:** GAC - Gestão de Ativos do CCT  
**Padrão Estrutural:** IEEE 830-1998 (Adaptado)  
**Milestone:** M2 - Especificação e Protótipo

---

## 1. Introdução

### 1.1 Propósito
O propósito deste documento é especificar os requisitos de software para o sistema **GAC (Gestão de Ativos do CCT)**. Este documento destina-se aos desenvolvedores, ao professor orientador (stakeholder avaliador), aos atendentes do setor operacional e à direção do CCT. Ele fornece a base para o design, validação e desenvolvimento do protótipo navegável.

### 1.2 Escopo do Produto
O sistema GAC digitalizará e unificará a gestão do inventário de chaves e projetores do CCT. A plataforma substituirá o controle em papel por um fluxo ágil baseado em leitura de QR Code/NFC, garantindo rastreabilidade em tempo real, emissão de termos de responsabilidade com aceite digital e checklists técnicos parametrizados na devolução.

### 1.3 Definições, Acrônimos e Abreviações
* **GAC:** Gestão de Ativos do CCT.
* **CCT:** Centro de Ciências e Tecnologia.
* **SRS:** Software Requirements Specification (Especificação de Requisitos de Software).
* **RF / RNF / RN:** Requisito Funcional / Não Funcional / Regra de Negócio.
* **DTEC:** Departamento Técnico (Responsável pelo suporte e validação de hardware).

### 1.4 Visão Geral do Documento
Este documento está dividido em três partes principais: a Introdução (Seção 1), a Descrição Geral do sistema e seus usuários (Seção 2) e os Requisitos Específicos e Casos de Uso detalhados (Seção 3).

---

## 2. Descrição Geral

### 2.1 Perspectiva do Produto
O GAC é um sistema web/mobile independente que operará no balcão de atendimento do CCT. Ele fará a ponte entre o inventário físico (armários de projetores e chaves) e a autenticação institucional dos professores, integrando-se via leitura de etiquetas físicas (QR Code/NFC).

### 2.2 Funções do Produto
As principais funções do sistema incluem:
* Cadastro e gestão de inventário de ativos e acessórios.
* Registro rápido de retiradas via scanner.
* Geração e validação de Termos de Responsabilidade com aceite digital.
* Registro de devoluções atreladas a um checklist técnico obrigatório.

### 2.3 Características dos Usuários (Personas)
* **Atendente (Ex: Kildery):** Usuário operacional. Precisa de uma interface ágil ("Fricção Zero") para não gerar filas no balcão e de checklists de segurança para resguardar a responsabilidade sobre avarias.
* **Professor (Docente):** Usuário final. Tem pouco tempo disponível. Interage com o sistema apenas para dar o aceite digital no seu dispositivo móvel antes de retirar a chave/projetor.
* **Direção / Secretaria:** Usuários gerenciais. Precisam de acesso a relatórios de auditoria e rastreabilidade (saber quem atrasou ou danificou equipamentos).

### 2.4 Restrições Gerais
* O equipamento projetor deve ser devolvido obrigatoriamente até o final do dia letivo (Regra de Negócio).
* Nenhuma retirada de projetor patrimonial pode ser concluída sem o registro e validação jurídica do Aceite Digital.

---

## 3. Requisitos Específicos

Nesta seção, os requisitos mapeados na Sprint 1 (Elicitação) são detalhados para a Sprint de Especificação (M2).

### 3.1 Requisitos Funcionais (RF)
* **RF01:** O sistema deve possuir um cadastro centralizado dos 36 projetores e das chaves/salas do CCT.
* **RF02:** O sistema deve unificar os processos de retirada e devolução, eliminando formulários de papel independentes.
* **RF03:** O sistema deve registrar acessórios (HDMI, USB, Controle Remoto) entregues e vinculá-los ao ativo principal.
* **RF04:** O sistema deve obrigar o preenchimento de um checklist técnico (estado físico, cabos, funcionamento) no momento da devolução.

### 3.2 Requisitos Não Funcionais (RNF)
* **RNF01 (Usabilidade):** Interface "Fricção Zero" para garantir agilidade no balcão, exigindo o mínimo de cliques possíveis para um empréstimo.
* **RNF02 (Segurança):** O aceite digital do termo de responsabilidade deve possuir validade jurídica, vinculando a transação à matrícula autenticada do docente.

### 3.3 Regras de Negócio (RN)
* **RN01:** O ativo retirado deve ser devolvido obrigatoriamente até o final do dia letivo corrente da retirada.
* **RN02:** É obrigatório o aceite do Termo de Responsabilidade para autorizar o empréstimo (Bloqueio de sistema).
* **RN03:** O sistema deve gerenciar o status individualizado de duas chaves físicas por sala do CCT (Original e Reserva).

### 3.4 Especificações de Casos de Uso (CDUs)
O detalhamento das interações entre sistema e atores (Ações, Fluxos Alternativos e Exceções) encontra-se documentado separadamente no formato LAPIS, visando maior granularidade de leitura.

* **Especificação dos Casos de Uso:** Detalha as validações do sistema, incluindo os fluxos de disponibilidade e assinatura digital para a retirada de ativos. *(Ver arquivo: `Especificação dos Casos de Uso.md`)*

---
*Fim do Documento SRS.*
