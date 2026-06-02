# Especificação de Requisitos Funcionais

## Caso de Uso (CDU) - GAC (Gestão de Ativos do CCT)

---

## Histórico de Versões

| Data       | Versão | Descrição                                                                  | Autor             |
|------------|---------|----------------------------------------------------------------------------|-------------------|
| 02/06/2026 | 1.0     | Criação da especificação do caso de uso de retirada de ativo patrimonial   | Grupo I           |

---

# 1. Nome do Caso de Uso

**Registrar Retirada de Ativo**

---

# 2. Objetivo

Permitir que o atendente realize o processo de empréstimo e retirada de projetores, chaves e acessórios do CCT para um professor, validando a disponibilidade do item, a situação cadastral do docente e coletando eletronicamente o aceite obrigatório do termo de responsabilidade.

---

# 3. Tipo de Caso de Uso

| Item | Valor |
|---|---|
| Tipo do Caso de Uso | Concreto |

---

# 4. Atores

## 4.1 Primário

| Ator | Descrição |
|---|---|
| Atendente | Responsável por operar o sistema no balcão do CCT, bipar o ativo e liberar o equipamento. |

## 4.2 Secundário

| Ator | Descrição |
|---|---|
| Professor | Responsável por solicitar o ativo e realizar o aceite digital do Termo de Responsabilidade. |
| Sistema Patrimonial | Responsável por validar a existência do ativo no inventário centralizado. |

---

# 5. Precondições

| Código | Descrição |
|---|---|
| PRE01 | O atendente deve estar autenticado e ativo no sistema GAC. |
| PRE02 | O ativo (projetor ou chave) deve estar previamente cadastrado no inventário com uma etiqueta física funcional (NFC/QR Code). |
| PRE03 | O ativo solicitado deve estar com o status "Disponível". |

---

# 6. Fluxo Principal

## P1. Iniciar atendimento
### P1.1.
O atendente inicia o fluxo de retirada de ativo no balcão de atendimento.
### P1.2.
O sistema exibe a tela de solicitação de empréstimo.

## P2. Identificar ativo e solicitante
### P2.1.
O atendente realiza a leitura da etiqueta física (QR Code/NFC) do ativo.
### P2.2.
O atendente insere a matrícula do professor solicitante.
### P2.3.
O sistema valida a existência e a disponibilidade do ativo no inventário.
### P2.4.
O sistema checa se o professor possui alguma pendência impeditiva (RN01, RN03).

## P3. Assinatura do Termo de Responsabilidade
### P3.1.
O sistema gera o Termo de Responsabilidade Digital específico para aquela locação.
### P3.2.
O sistema dispara o pedido de assinatura para o dispositivo do professor.
### P3.3.
O professor lê e confirma o aceite digital do termo em seu dispositivo de interface.

## P4. Confirmar retirada
### P4.1.
O sistema valida a assinatura digital e registra a transação de empréstimo.
### P4.2.
O sistema altera o status do ativo para "Emprestado".
### P4.3.
O sistema exibe a mensagem de confirmação de sucesso [MSG01] e libera a entrega física.

## P5. Finalizar operação
### P5.1.
O atendente entrega fisicamente o equipamento (projetor/chave) e os acessórios vinculados ao professor.
### P5.2.
O caso de uso é encerrado com sucesso.

---

# 7. Fluxos Alternativos

## FA01 - Registro Manual de Código de Ativo
Ocorre no Passo 2 do fluxo principal se a etiqueta de QR Code/NFC do ativo estiver danificada ou ilegível.
1. O atendente seleciona a opção de inserção manual de código.
2. O atendente digita o número de tombamento patrimonial gravado no ativo físico.
3. O sistema valida o código inserido e o fluxo retorna ao Passo 2 do fluxo principal.

---

# 8. Fluxos de Exceção

## FE01 - Professor com Pendência de Entrega
Ocorre no Passo 2 do fluxo principal se o sistema detectar que o professor possui um ativo em atraso não devolvido.
1. O sistema interrompe o fluxo e exibe a mensagem de erro [MSG02], alertando sobre a pendência ativa do docente.
2. O atendente informa ao professor que a retirada não pode ser concluída até a regularização do débito patrimonial.
3. O caso de uso é encerrado sem sucesso.

## FE02 - Ativo já Emprestado ou Indisponível
Ocorre no Passo 2 do fluxo principal se o código lido apontar para um ativo que não esteja com o status "Disponível".
1. O sistema exibe a mensagem de erro [MSG03], indicando que o ativo está indisponível para empréstimo.
2. O atendente cancela a operação e seleciona outro ativo disponível.
3. O fluxo retorna ao Passo 2 do fluxo principal.

## FE03 - Recusa do Termo de Responsabilidade
Ocorre no Passo 4 do fluxo principal se o professor recusar ou cancelar o aceite do termo digital.
1. O sistema cancela a operação de empréstimo pendente e exibe a mensagem [MSG04].
2. O atendente retém o equipamento no balcão e não realiza a entrega física.
3. O caso de uso é encerrado sem sucesso.

---

# 9. Pós-condições

| Código | Descrição |
|---|---|
| POS01 | O status do ativo é alterado de "Disponível" para "Emprestado" em tempo real no banco de dados. |
| POS02 | O histórico de movimentação do ativo é atualizado com data, hora, matrícula do professor e ID do atendente responsável. |
| POS03 | O Termo de Responsabilidade Digital assinado é arquivado e indexado na conta institucional do professor para fins de auditoria. |

---

# 10. Regras de Negócio Associadas

| Código | Título | Descrição |
|---|---|---|
| **RN01** | Prazo Limite | O ativo retirado deve ser devolvido obrigatoriamente até o final do dia letivo corrente da retirada. |
| **RN02** | Obrigatoriedade de Termo | Nenhuma retirada de projetor patrimonial pode ser concluída sem o registro e validação do Aceite Digital do Termo de Responsabilidade. |
| **RN03** | Instâncias de Chaves | O sistema deve gerenciar e validar o status individualizado de duas chaves físicas por sala do CCT (Original e Reserva), impedindo o empréstimo simultâneo do mesmo identificador. |

---

# 11. Mensagens do Sistema

| Código | Tipo | Texto da Mensagem |
|---|---|---|
| **MSG01** | Sucesso | "Retirada de Ativo registrada com sucesso! Equipamento liberado para entrega física." |
| **MSG02** | Erro | "Operação bloqueada: O professor possui pendências ativas de devolução no CCT." |
| **MSG03** | Erro | "Ativo Inválido: O equipamento selecionado já se encontra sob o status de Emprestado." |
| **MSG04** | Alerta | "Operação cancelada: O Termo de Responsabilidade Digital foi recusado pelo usuário final." |

---

# 12. Requisitos Não Funcionais Associados

| Código | Categoria | Descrição |
|---|---|---|
| **RNF01** | Usabilidade | O fluxo de biometria/leitura de etiquetas no balcão deve operar sob o conceito de "Fricção Zero", exigindo no máximo 3 cliques do atendente para processar a retirada rápida. |
| **RNF02** | Segurança | O método de armazenamento e criptografia do aceite digital do professor deve garantir conformidade jurídica e não-repúdio institucional equivalente ao papel físico. |

---

# 13. Conclusão do Artefato
*Documento de Especificação de Caso de Uso em conformidade com o Milestone M1 da disciplina Requisitos e Modelagem de Sistemas.*
