---
name: metrics
description: Calcula métricas de testes QA, distribuição de severidade dos defeitos, pontuação de saúde do sistema, riscos e recomendação de Go Live a partir de entradas numéricas de QA. Use quando o usuário solicitar indicadores de QA, resumos de execução de testes, análise de defeitos, cálculos de saúde do sistema ou apoio à decisão de Go Live.
---

# Métricas

Use esta skill para calcular indicadores de QA a partir de números de testes e organizar o resultado de acordo com o formato de saída solicitado pelo usuário.

## Entrada

Aceite a entrada como um objeto JSON, tabela, lista com marcadores, texto corrido ou texto copiado com métricas. Extraia e normalize estes campos:

- `cenariosCriados`: total de cenários de teste planejados ou criados.
- `cenariosExecutados`:cenários já executados.
- `cenariosAprovados`: cenários executados aprovados ou que passaram.
- `cenariosReprovados`: cenários executados reprovados ou que falharam.
- `cenariosRetestados`: cenários retestados.
- `cenariosBloqueados`: cenários bloqueados.
- `defeitosCriticos`: defeitos críticos.
- `defeitosAltos`: defeitos de severidade alta.
- `defeitosMedios`: defeitos de severidade média.
- `defeitosBaixos`: defeitos de severidade baixa.

Se um campo obrigatório estiver ausente, solicite apenas os valores faltantes antes de calcular. Valide se todos os valores são numéricos, finitos e maiores ou iguais a zero. Valide se `cenariosExecutados` não é maior que `cenariosCriados`.

Se `cenariosAprovados + cenariosReprovados` for maior que `cenariosExecutados`, sinalize a inconsistência e solicite correção, a menos que o usuário diga explicitamente que as categorias podem se sobrepor.

## Processamento

Arredonde percentuais e indicadores decimais para 2 casas decimais. Quando o denominador for zero, retorne `0` para esse percentual em vez de falhar. Para `defeitosPorCenarioExecutado`, divida por pelo menos `1` para evitar divisão por zero.

Calcule:

- `percentualExecucao = cenariosExecutados / cenariosCriados * 100`
- `percentualAprovacao = cenariosAprovados / cenariosExecutados * 100`
- `percentualFalhas = cenariosReprovados / cenariosExecutados * 100`
- `percentualRetestes = cenariosRetestados / cenariosExecutados * 100`
- `percentualBloqueados = cenariosBloqueados / cenariosCriados * 100`
- `totalDefeitos = defeitosCriticos + defeitosAltos + defeitosMedios + defeitosBaixos`
- `taxaCriticos = defeitosCriticos / totalDefeitos * 100`
- `taxaAltos = defeitosAltos / totalDefeitos * 100`
- `taxaMedios = defeitosMedios / totalDefeitos * 100`
- `taxaBaixos = defeitosBaixos / totalDefeitos * 100`
- `defeitosPorCenarioExecutado = totalDefeitos / max(cenariosExecutados, 1)`

Calcule a pontuação de saúde:

```Texto
approvalScore = percentualAprovacao
executionScore = percentualExecucao
lowFailureScore = max(0, 100 - percentualFalhas)
criticalBlockedRate = (defeitosCriticos + cenariosBloqueados) / max(cenariosCriados, 1) * 100
lowCriticalAndBlockedScore = max(0, 100 - criticalBlockedRate)

saude =
  approvalScore * 0.4 +
  executionScore * 0.3 +
  lowFailureScore * 0.2 +
  lowCriticalAndBlockedScore * 0.1
```

Arredonde `saude` para 2 casas decimais.

## Saidas

Classifique o resultado como:

- `saude >= 90`: `status = Verde`, `indicador = Aprovado para Go Live`, `recomendacao = Pode subir para Producao.`
- `saude >= 75` and `< 90`: `status = Amarelo`, `indicador = Go Live com atencao`, `recomendacao = Subir com atencao e monitoramento.`
- `saude < 75`: `status = Vermelho`, `indicador = Go Live nao recomendado`, `recomendacao = Nao recomendado subir para Producao.`

Quando o usuário não solicitar uma estrutura específica, prefira esta ordem:

1. Resumo executivo com `saude`, `status`, `indicador`, e `recomendacao`.
2. Entrada validada com os valores de entrada normalizados.
3. Informações de processamento com as fórmulas aplicadas, regra de arredondamento, tratamento de denominador zero e quaisquer premissas.
4. Indicadores calculados com taxas de execução, aprovação, reprovação, reteste, bloqueio, total de defeitos, densidade de defeitos e taxas por severidade.
5. Riscos e pontos de atenção.
6. Recomendação final.

Mencione os riscos quando a execução estiver baixa, a aprovação estiver baixa, as reprovações estiverem altas, houver cenários bloqueados, existirem defeitos críticos, existirem defeitos de severidade alta ou forem encontradas inconsistências nos dados.

Se o usuário solicitar JSON, retorne apenas esta estrutura:

```json
{
  "entradaValidada": {},
  "processamento": [],
  "indicadores": {},
  "defeitos": {},
  "saudeSistema": {
    "saude": 0,
    "status": "",
    "indicador": "",
    "recomendacao": ""
  },
  "riscos": [],
  "recomendacaoFinal": ""
}
```

## Exemplo

Entrada:

```json
{
  "cenariosCriados": 100,
  "cenariosExecutados": 90,
  "cenariosAprovados": 82,
  "cenariosReprovados": 8,
  "cenariosRetestados": 6,
  "cenariosBloqueados": 2,
  "defeitosCriticos": 0,
  "defeitosAltos": 1,
  "defeitosMedios": 3,
  "defeitosBaixos": 5
}
```

Resultado-chave esperado:

- `percentualExecucao`: 90%
- `percentualAprovacao`: 91.11%
- `percentualFalhas`: 8.89%
- `percentualRetestes`: 6.67%
- `percentualBloqueados`: 2%
- `totalDefeitos`: 9
- `defeitosPorCenarioExecutado`: 0.1
- `saude`: 91.47%
- `status`: Verde
- `Go Live`: Pode subir para Producao.
