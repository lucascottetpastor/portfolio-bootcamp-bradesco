# 🎯 Desafio: Extraindo Insights do Feedback de Clientes Bancários

> Projeto desenvolvido como parte do [Bootcamp do Bradesco na DIO](https://web.dio.me/track/bradesco-dados-ciberseguranca-genai), explorando o uso de **Engenharia de Prompts** como ferramenta de análise de dados com IA.

---

## 🧭 1. Contexto e Objetivos

### Contexto

Bancos e fintechs lidam diariamente com grandes volumes de feedbacks de clientes distribuídos em múltiplos canais: aplicativo, Pix, cartão de crédito, atendimento por chat. Transformar esses comentários soltos em insights é um desafio real de dados e experiência do cliente.

Este desafio foi criado para praticar a construção de **prompts estruturados e eficazes**, capazes de orientar uma IA a analisar feedbacks bancários de forma organizada, segura e útil para tomada de decisão.

### Objetivos

- ✅ Definir uma intenção clara para a análise com IA
- ✅ Adicionar contexto, dados disponíveis e restrições ao prompt
- ✅ Unir todas as peças em um prompt final reutilizável e bem estruturado
- ✅ Aplicar boas práticas de engenharia de prompts (papel da IA, formato de saída, restrições)
- ✅ Garantir o cuidado com dados sensíveis em um contexto bancário

---

## 🧱 2. Construção do Prompt - Passo a Passo

Esta seção documenta os três passos utilizados para construir o prompt final, do mais simples ao mais completo.

---

### 🔹 Passo 1 - Definindo a Intenção

**Objetivo:** Descrever o que a IA deve produzir, para quem e com qual finalidade.

**Intenção definida:**

> Quero que a IA analise comentários de clientes sobre os canais digitais de um banco (aplicativo, Pix, cartão de crédito e atendimento por chat) para identificar reclamações frequentes, elogios e oportunidades de melhoria.
>
> O resultado será usado por uma equipe de experiência do cliente para apoiar decisões de priorização de melhorias nos canais digitais e redução de atritos no atendimento.
>
> A entrega deve conter um resumo executivo, uma tabela com os principais temas identificados, exemplos de comentários como evidência e recomendações por área.
>
> O resultado será considerado bom se for claro, organizado, baseado nos comentários fornecidos e útil para priorizar ações.

**Aprendizado desta etapa:**
> Definir o público que vai usar a análise (equipe de CX) e o critério de qualidade ("útil para priorizar ações") ajudou a deixar a intenção mais direcionada do que apenas dizer "analise os feedbacks".

---

### 🔹 Passo 2 - Adicionando Contexto e Restrições

**Objetivo:** Incluir informações de apoio, limites e cuidados para orientar melhor a resposta da IA.

**Contexto e restrições definidos:**

> **Contexto:** Estou trabalhando com feedbacks de clientes bancários relacionados ao aplicativo mobile, transações Pix, cartão de crédito e atendimento por chat.
>
> **Dados disponíveis:** A base contém data do comentário, canal de atendimento (app, chat, Pix, cartão), texto livre do feedback escrito pelo cliente e nota de satisfação de 1 a 5.
>
> **Critérios de análise:** A IA deve classificar os feedbacks por tema (ex: usabilidade, lentidão, segurança, atendimento), sentimento (positivo, negativo, neutro), urgência (alta, média, baixa) e produto citado.
>
> **Cuidados e restrições:**
> - Use apenas os dados fornecidos.
> - Não invente números, causas ou conclusões.
> - Não exponha dados pessoais ou sensíveis dos clientes.
> - Se houver informação insuficiente, indique a limitação claramente.
> - Use linguagem simples, direta e voltada para tomada de decisão.

**Aprendizado desta etapa:**
> A restrição de "não inventar números ou conclusões" é essencial em contextos bancários, uma análise com dados fabricados pode gerar decisões erradas. Adicionar os campos disponíveis na base também ajudou a IA a saber exatamente o que pode e o que não pode usar.

---

### 🔹 Passo 3 - Prompt Final

**Objetivo:** Reunir intenção, contexto, critérios e restrições em um único comando.

**Prompt final:**

```
Atue como analista de dados e experiência do cliente em um banco digital.

Sua tarefa é analisar feedbacks de clientes sobre aplicativo mobile, Pix, cartão de crédito
e atendimento por chat para identificar temas recorrentes, sentimentos e
oportunidades concretas de melhoria.

Contexto: A análise será usada por uma equipe de experiência do cliente para priorizar
melhorias nos canais digitais e reduzir atritos no atendimento. O foco é transformar
comentários soltos em insights claros, apoiando decisões de produto e operação.

Dados disponíveis: Serão fornecidos comentários contendo data, canal de atendimento (app,
chat, Pix ou cartão), texto livre do feedback e nota de satisfação de 1 a 5.

Instruções de análise:
1. Classifique cada feedback por tema, sentimento (positivo, negativo ou neutro), urgência
   (alta, média ou baixa) e produto citado.
2. Identifique os principais padrões, problemas recorrentes, elogios e oportunidades de melhoria.
3. Aponte evidências nos dados fornecidos, usando trechos curtos dos comentários como exemplo.
4. Sugira ações práticas para a equipe de experiência do cliente e para os times responsáveis
   por cada canal.

Formato da resposta:
- Resumo executivo com até 5 linhas destacando os pontos mais críticos.
- Tabela com colunas: Tema - Sentimento - Urgência - Evidência - Ação sugerida.
- Lista final com as 3 principais prioridades de melhoria.

Restrições:
- Use apenas os dados fornecidos.
- Não invente números, causas ou conclusões.
- Não exponha dados pessoais ou sensíveis.
- Informe limitações quando os dados não forem suficientes para uma conclusão.
- Use linguagem simples, direta e voltada para tomada de decisão.
```

**Aprendizado desta etapa:**
> Unir tudo em um único bloco revelou uma redundância: o contexto e as restrições apareciam duas vezes. A revisão final foi essencial para deixar o prompt mais limpo sem perder nenhuma instrução importante. O formato da resposta foi o elemento que mais impactou a qualidade do resultado, sem ele, a IA tende a responder em texto corrido, dificultando a leitura.

---

## 📝 3. Glossário de Engenharia de Prompts

| Termo | Definição |
|-------|-----------|
| **Prompt** | Instrução ou conjunto de instruções enviadas à IA para orientar sua resposta |
| **Papel da IA** | Definição do perfil ou função que a IA deve assumir (ex: analista, consultor, revisor) |
| **Intenção** | Descrição clara do que se espera que a IA produza e para qual finalidade |
| **Contexto** | Informações de apoio que ajudam a IA a entender o cenário e o público da análise |
| **Restrições** | Limites que definem o que a IA deve evitar fazer (inventar dados, expor PII, etc.) |
| **Formato de saída** | Especificação de como a resposta deve ser estruturada (tabela, lista, resumo, etc.) |
| **Sentimento** | Classificação do tom emocional de um texto: positivo, negativo ou neutro |
| **PII** | Personally Identifiable Information — dados que identificam uma pessoa (nome, CPF, etc.) |
| **Insight** | Descoberta relevante extraída de dados que apoia uma decisão ou ação |
| **Prompt Reutilizável** | Prompt genérico com campos variáveis que pode ser adaptado para diferentes contextos |

---

## 🛠️ Ferramentas Utilizadas

| Ferramenta | Uso |
|------------|-----|
| [Claude (Anthropic)](https://claude.ai) | Auxílio no refinamento do prompt |
| [GitHub](https://github.com) | Repositório e documentação do projeto |

---

## 👤 Autor

[![GitHub](https://img.shields.io/badge/GitHub-lucascottetpastor-black?style=flat&logo=github)](https://github.com/lucascottetpastor)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-lucascottet-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/lucascottet/)

---

*Projeto desenvolvido para o Desafio Criativo do [Bootcamp do Bradesco na DIO](https://web.dio.me/track/bradesco-dados-ciberseguranca-genai) — Engenharia de Prompts aplicada à análise de feedbacks bancários.*
