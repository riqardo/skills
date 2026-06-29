# Company Jira Documentation Template

Use this structure for full Jira documentation. Keep the output concise, direct, and paste-ready.

## Required Structure

```markdown
**[Tela/Fluxo/Funcionalidade com problema, impacto ou cenário observado]**

## Motivação
- [Motivação que levou à necessidade do ajuste: dor do usuário, impacto no negócio, aumento de suporte, perda operacional, falha de jornada, inconsistência ou necessidade técnica.]
- [Risco técnico, operacional ou de produto, se houver. Use no máximo este segundo bullet.]

## Objetivo
- [Estado final desejado. O que o sistema deve ser capaz de fazer após a demanda?]

## Solução Esperada
- [Descrição do fluxo funcional esperado. Não escrever código; descrever comportamento, regras e respostas do sistema.]

## Critérios de Aceite
- **Dado que** [contexto inicial];
- **Quando** [ação do usuário, sistema ou integração];
- **Então** [resultado esperado, verificável e binário].

## Checklist de Validação
- [ ] 
- [ ] 
- [ ] 

## Observações
- [Bloqueios, dependências de API, impactos em outras telas, exceções, pontos de atenção ou itens a validar com PO/Tech Lead/Segurança.]

## Links Úteis
- [Figma, Jira relacionado, Trello, documentação, evidências ou "Não informado".]
```

## Title Rule

The title must describe what is happening or what is wrong, not the action to be taken.

Prefer:

```markdown
**Tela de Recuperação de Senha com Carregamento Infinito ao Informar E-mail Inválido**
**Tela de Login Não Exibe Feedback Quando a Autenticação Falha**
**Listagem de Pedidos Apresenta Valores Divergentes no Filtro por Período**
```

Avoid by default:

```markdown
**Correção da Tela de Recuperação de Senha**
**Ajuste no Login**
**Implementação de Mensagem de Erro**
**Melhoria no Filtro de Pedidos**
```

## Section Guidance

- **Motivação**: Use a maximum of 2 bullets. The first explains the user/business pain. The second explains technical, operational, support, compliance, or product risk when relevant.
- **Objetivo**: State the desired final state, not the implementation plan.
- **Solução Esperada**: Describe behavior and flow. Include messages, status changes, loading behavior, validation rules, and integration responses when provided.
- **Critérios de Aceite**: Use binary pass/fail criteria. Prefer "Dado que...", "Quando...", "Então...". Split into multiple scenarios when the behavior has multiple branches.
- **Checklist de Validação**: Leave blank checklist items for QA to fill unless the user explicitly asks for suggested validation items.
- **Observações**: Include dependencies, impacts, exceptions, known blockers, and points to validate.
- **Links Úteis**: Include provided links only. If none are provided, write "Não informado."

## Example

Input:

```text
Notei que quando o usuário tenta recuperar a senha e erra o e-mail, o sistema fica carregando infinito em vez de mostrar que o e-mail não existe. Isso está fazendo o pessoal abrir ticket no suporte achando que o site caiu.
```

Output:

```markdown
**Tela de Recuperação de Senha com Carregamento Infinito ao Informar E-mail Inválido**

## Motivação
- Atualmente, o sistema entra em loop de carregamento infinito quando um e-mail inválido é informado na recuperação de senha.
- Isso gera percepção de instabilidade no sistema e aumenta desnecessariamente o volume de chamados no suporte técnico.

## Objetivo
- Garantir que o usuário receba um feedback claro quando o e-mail informado não puder seguir no fluxo de recuperação de senha.

## Solução Esperada
- Ao clicar em "Recuperar Senha", o sistema deve validar a solicitação e interromper o carregamento caso o e-mail seja inválido ou não possa prosseguir. Nessa situação, uma mensagem de alerta deve ser exibida para orientar o usuário sobre o erro.

## Critérios de Aceite
- **Dado que** o usuário informa um e-mail não cadastrado;
- **Quando** clicar no botão de envio;
- **Então** o sistema deve interromper o carregamento e exibir uma mensagem de erro em até 2 segundos.
- **Dado que** a validação retorna erro;
- **Quando** a mensagem for exibida;
- **Então** o botão de envio deve ser reabilitado para permitir nova tentativa.

## Checklist de Validação
- [ ] 
- [ ] 
- [ ] 

## Observações
- Validar com PO/Segurança se a mensagem pode confirmar que o e-mail não existe na base, considerando possíveis restrições de LGPD e segurança.

## Links Úteis
- Não informado.
```
