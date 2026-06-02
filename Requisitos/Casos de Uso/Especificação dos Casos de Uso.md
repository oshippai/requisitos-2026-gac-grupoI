# Especificação de Requisitos Funcionais

## Caso de Uso (CDU) - GAC

---

## Histórico de Versões

| Data       | Versão | Descrição                                                                  | Autor             |
|------------|---------|----------------------------------------------------------------------------|-------------------|
| 02/06/2026 | 1.0     | Criação do caso de uso de retirada e empréstimo de ativo patrimonial       | Grupo I           |

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
| Atendente | Realiza o registro, vinculação de acessórios e liberação física do equipamento |

---

## 4.2 Secundário

| Ator | Descrição |
|---|---|
| Professor | Responsável pela solicitação e pelo aceite digital do Termo de Responsabilidade |
| Sistema Patrimonial | Responsável por validar a existência e status do ativo no inventário |
| Sistema de Autenticação | Responsável pela autenticação do atendente e do professor |

---

# 5. Precondições

| Código | Descrição |
|---|---|
| PRE01 | O atendente deve estar autenticado no sistema GAC |
| PRE02 | O equipamento deve estar cadastrado e possuir identificação física (QR Code/NFC) |
| PRE03 | O equipamento deve estar com o status “Disponível” no banco de dados |

---

# 6. Fluxo Principal

## P1. Acessar funcionalidade de empréstimo

### P1.1.
O atendente acessa o módulo de "Nova Retirada" no painel principal do sistema GAC.

---

## P2. Identificar professor solicitante

### P2.1.
O atendente insere a matrícula do professor ou realiza a leitura da carteirinha institucional (NFC).

### P2.2.
O sistema processo a identificação e realiza a busca na base de dados de usuários.

### P2.3.
O sistema apresenta na tela os dados do docente (Nome, Departamento, Foto e Status de Pendências).

---

## P3. Identificar e validar ativo (projetor/chave)

### P3.1.
O atendente realiza a leitura da etiqueta física (QR Code ou NFC) colada no ativo.

### P3.2.
O sistema identifica o equipamento patrimonial no banco de dados.

### P3.3.
O sistema apresenta os dados técnicos do ativo (Número, Modelo, Status e Acessórios Padrão).

---

## P4. Selecionar acessórios entregues

### P4.1.
O sistema exibe o checklist de saída para os acessórios.

### P4.2.
O atendente marca no sistema quais itens extras estão acompanhando o projetor (Cabo HDMI, Controle, etc.).

---

## P5. Processar Termo de Responsabilidade Digital

### P5.1.
O atendente clica em "Gerar Termo de Saída".

### P5.2.
O sistema compila os dados e gera o Termo de Responsabilidade específico.

### P5.3.
O sistema dispara instantaneamente uma notificação para o dispositivo móvel do professor logado no app GAC.

### P5.4.
O professor abre a notificação, lê o resumo e clica em "Aceitar e Assinar Eletronicamente".

### P5.5.
O sistema valida a assinatura digital (RN02).

---

## P6. Confirmar e registrar retirada

### P6.1.
O sistema atualiza a tela do atendente com a mensagem "Termo Assinado com Sucesso".

### P6.2.
O atendente clica no botão "Confirmar Liberação de Ativo".

### P6.3.
O sistema registra a transação completa no banco de dados.

---

## P7. Finalizar operação

### P7.1.
O sistema altera o status do ativo de "Disponível" para "Emprestado".

### P7.2.
O sistema gera o comprovante eletrônico de retirada.

### P7.3.
O atendente entrega fisicamente o equipamento e os acessórios ao professor.

---

# 7. Fluxos Alternativos

## A1. Falha na leitura do QR Code/NFC do Ativo

### A1.1.
O sistema não identifica o QR Code ou a etiqueta está danificada.

### A1.2.
O atendente realiza busca manual digitando o número de tombamento patrimonial.

### A1.3.
O fluxo retorna ao passo P3.2.

---

## A2. Professor sem dispositivo móvel para assinatura

### A2.1.
O professor informa que está sem celular, sem bateria ou sem internet.

### A2.2.
O atendente seleciona a opção "Assinatura via Totem/Balcão".

### A2.3.
O sistema exibe o Termo de Responsabilidade no tablet voltado para o professor no balcão.

### A2.4.
O professor insere sua senha institucional diretamente no tablet do balcão para validar o aceite.

### A2.5.
O fluxo retorna ao passo P5.5.

---

# 8. Fluxos de Exceção

## E1. Professor com pendência ativa

### E1.1.
No passo P2.3, o sistema identifica que o professor possui um ativo em atraso não devolvido.

### E1.2.
O sistema exibe mensagem de erro [MSG002] e bloqueia o botão de prosseguir.

### E1.3.
O atendente informa ao professor sobre o bloqueio.

### E1.4.
O caso de uso é encerrado sem sucesso.

---

## E2. Equipamento não disponível

### E2.1.
No passo P3.2, o sistema identifica que o ativo lido consta como "Emprestado" ou "Manutenção".

### E2.2.
O sistema exibe mensagem de erro [MSG003].

### E2.3.
O atendente descarta o item, seleciona outro ativo físico e o fluxo retorna ao P3.1.

---

## E3. Recusa do Termo de Responsabilidade

### E3.1.
No passo P5.4, o professor clica em "Recusar Termo" ou o tempo limite de aceite expira.

### E3.2.
O sistema cancela a operação pendente e exibe mensagem de alerta [MSG004].

### E3.3.
O atendente retém o equipamento no balcão.

### E3.4.
O caso de uso é encerrado sem sucesso.

---

# 9. Pós-condições

| Código | Descrição |
|---|---|
| POS01 | O equipamento e seus acessórios mudam para o status "Emprestado" |
| POS02 | A movimentação de saída é registrada com data, hora, matrícula do professor e do atendente |
| POS03 | O Termo de Responsabilidade assinado digitalmente é arquivado |

---

# 10. Requisitos Não Funcionais

| Código | Requisito |
|---|---|
| RNF01 | O fluxo de biometria/leitura no balcão deve exigir o mínimo de cliques ("Fricção Zero") |
| RNF02 | O método de armazenamento da assinatura do termo deve garantir validade jurídica institucional |
| RNF03 | O disparo da notificação para o celular do professor deve ocorrer em até 3 segundos |

---

# 11. Ponto de Extensão

## PE1. Registrar Notificação de Atraso
Permite o agendamento automático de um e-mail de cobrança caso o sistema atinja o fim do dia letivo e o fluxo de devolução não tenha sido iniciado para este ativo.

---

# 12. Frequência de Utilização

| Item | Informação |
|---|---|
| Frequência | Alta |
| Perfil de Uso | Utilização constante pelos atendentes, concentrada nos inícios de turno letivo (manhã/noite) |
| Informações mais acessadas | Matrícula do professor, QR Code do ativo, Status de assinatura |

---

# 13. Interface Visual

## IV1. Tela de Registro de Retirada

### Leiaute da Tela

Tela utilizada pelo atendente para identificar o solicitante, bipar o ativo e gerenciar o envio do termo.

---

## 13.1 Campos da Interface

| Campo | Tipo/Formato | Obrigatório | Descrição | Regra de Negócio |
|---|---|---|---|---|
| Matrícula do Atendente | Texto (20) | Sim | Identificação do atendente | Deve possuir permissão ativa |
| Data/Hora da Retirada | Data/Hora | Sim | Momento da locação | Gerado automaticamente |
| Matrícula do Professor | Texto (20) | Sim | Identificação do docente | Não pode ter pendências |
| Leitura QR Code | QR Code | Sim | Identificação do patrimônio | Deve estar "Disponível" |
| Número Patrimonial | Texto (20) | Sim | Código do ativo | Obtido via QR Code ou manual |
| Cabo HDMI | Checkbox | Não | Acessório entregue | Vincula ao termo gerado |
| Cabo de Energia | Checkbox | Não | Acessório entregue | Vincula ao termo gerado |
| Controle Remoto | Checkbox | Não | Acessório entregue | Vincula ao termo gerado |
| Status da Assinatura | Ícone/Texto | Sim | Indica se o termo foi aceito | Bloqueia entrega se falso |
| Botão “Gerar Termo” | Botão | Sim | Dispara notificação | Habilitado após ler professor e ativo |
| Botão “Confirmar Liberação” | Botão | Sim | Finaliza retirada | Habilitado apenas após aceite digital |
| Botão “Cancelar” | Botão | Não | Cancela operação | Libera o ativo no sistema |

---

## 13.2 Navegabilidade

| Ação | Resultado |
|---|---|
| Ler QR Code válido | Sistema carrega os dados do ativo e habilita seleção de acessórios |
| Inserir Professor com Pendência | Sistema bloqueia tela e exibe mensagem MSG002 |
| Clicar em Gerar Termo | Sistema envia notificação e altera status da assinatura para "Aguardando" |
| Confirmar Liberação | Sistema registra saída e altera status do ativo para "Emprestado" |

---

## 13.3 Mensagens Previstas

| Código | Mensagem |
|---|---|
| MSG001 | Retirada autorizada e registrada com sucesso |
| MSG002 | Operação bloqueada: O professor possui pendências ativas |
| MSG003 | Equipamento indisponível para empréstimo neste momento |
| MSG004 | Operação cancelada: Termo de Responsabilidade recusado |

---

## 13.4 Componentes Visuais

| Área | Componente |
|---|---|
| Identificação | Leitor de Matrícula e QR Code |
| Status do Professor | Card indicativo (Verde para Liberado, Vermelho para Bloqueado) |
| Acessórios | Lista de checkboxes |
| Status do Termo | Spinner/Ícone de carregamento enquanto aguarda aceite |

---

# 14. Observações

| Código | Observação |
|---|---|
| OBS01 | A devolução obrigatoriamente exigirá a conferência dos mesmos acessórios marcados nesta tela |
| OBS02 | O app do professor deve permitir leitura prévia do contrato institucional de uso |

---

# 15. Referências

| Código | Referência |
|---|---|
| REF01 | Documento de Visão do GAC (Issues #1 a #7) |
| REF02 | Diagrama de Casos de Uso (UC04 e UC05) |
| REF03 | Modelo [[LAPIS de Liderança Ágil](https://github.com/ProfBezerra/LAPIS/) |

---

# 16. Checklist de Validação do Artefato (CDU)

## 16.1 Estrutura mínima

- [x] Nome do caso de uso iniciado com verbo no infinitivo.
- [x] Objetivo claro, direto e com foco em um objetivo principal.
- [x] Tipo do caso de uso informado.
- [x] Atores primário e secundários identificados corretamente.
- [x] Precondições registradas.
- [x] Fluxo principal completo e coerente com o objetivo.
- [x] Fluxos alternativos e de exceção definidos.
- [x] Pós-condições registradas.
- [x] Requisitos não funcionais registrados.
- [x] Pontos de extensão identificados.
- [x] Frequência de utilização estimada.

## 16.2 Qualidade da especificação

- [x] Passos escritos com linguagem simples e objetiva.
- [x] Ações descritas no presente do indicativo.
- [x] Alternância entre ação do ator e sistema está clara.
- [x] Não há ambiguidade.
- [x] Regras de negócio e mensagens referenciadas.

## 16.3 Consistência e rastreabilidade

- [x] Fluxos alternativos possuem entrada e saída explícitas.
- [x] Fluxos de exceção vinculados corretamente.
- [x] Referências internas consistentes.
- [x] Interface visual coerente com o fluxo.
- [x] Referências atualizadas.

## 16.4 Revisão final

- [x] Não há contradições entre seções.
- [x] Documento revisado.
- [x] Artefato pronto para desenvolvimento e testes.
