---
name: jira-documentation
description: Create Jira-ready task documentation from rough notes, chat summaries, code-change summaries, screenshots, or short user descriptions. Use when the user asks to create documentation, Jira documentation, ticket text, task specs, implementation notes, acceptance criteria, QA notes, or a structured description for work done in Visual Studio, Visual Studio Code, or a local code project.
---

# Jira Documentation

## Overview

Turn informal task notes into clear Jira documentation using the company's required structure. Default to Brazilian Portuguese unless the user requests another language.

The user may provide only a rough summary. Produce useful documentation from what is available, mark assumptions clearly, and ask follow-up questions only when a missing detail would materially change the ticket.

## Workflow

1. Identify the requested output:
   - New Jira task/story/bug documentation
   - Documentation for work already done
   - Acceptance criteria only
   - QA/test notes only
   - Technical implementation notes only
   - Short Jira comment/update

2. Extract or infer the core facts:
   - Jira key or title, if provided
   - Issue type: task, story, bug, spike, improvement, or subtask
   - Business/context problem
   - Current behavior and expected behavior
   - User-facing impact
   - Technical scope, files, components, endpoints, services, or database changes
   - Dependencies, risks, constraints, and open questions
   - Testing or validation evidence

3. If the request is underspecified:
   - Continue with reasonable assumptions when the user wants speed.
   - Add an "Assumptions" section.
   - Add an "Open questions" section for unresolved details.
   - Ask at most 3 concise questions before drafting only if the missing information blocks the documentation.

4. Draft the documentation using the required company template in `references/document-template.md`.

5. Make the final output easy to paste into Jira:
   - Use clean headings.
   - Prefer concise bullet points.
   - Avoid invented ticket IDs, file names, metrics, owners, deadlines, or production evidence.
   - Keep technical wording precise, but avoid overexplaining obvious implementation details.

## Output Rules

- Default language: pt-BR.
- Tone: professional, direct, and useful for engineering/product/QA readers.
- Write as a senior QA engineer and systems analyst: direct, technically clear, and strict about acceptance criteria.
- Avoid filler. Prefer plain descriptions of the observed behavior over abstract phrasing.
- Make the business value, user pain, operational risk, or technical risk clear.
- Preserve user-provided terminology for product names, modules, branches, and code entities.
- If the user says the work was done in "studio visual", interpret it as the local IDE/editor context unless they clarify whether it is Visual Studio or Visual Studio Code.
- Use Markdown.
- The title must describe the observed problem, impact, or scenario. Do not title the document as the action to be done.
- Avoid title prefixes such as "Correção de", "Ajuste de", "Implementação de", or "Melhoria de" unless the user explicitly asks for that format.
- Prefer titles like "**Tela de Login Não Exibe Feedback Quando a Autenticação Falha**" or "**Tela de Recuperação de Senha com Carregamento Infinito ao Informar E-mail Inválido**".
- Do not invent ticket IDs, file names, metrics, owners, deadlines, APIs, links, screenshots, or production evidence.
- Use "A validar" or "Não informado" when information is missing and the absence matters.
- When creating bug documentation, include the current behavior inside "Motivação" or "Solução Esperada" instead of adding extra sections outside the company template.
- When creating a Jira comment, be shorter and focus on status, what changed, validation, and next steps.

## Reference

Read `references/document-template.md` whenever drafting a full Jira ticket or full task documentation.
