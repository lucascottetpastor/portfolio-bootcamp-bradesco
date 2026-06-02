# 📚 Caderno Temático: APIs REST com Laravel

> Projeto desenvolvido como parte do desafio prático do [BootCamp do Bradesco na DIO](https://web.dio.me/track/bradesco-dados-ciberseguranca-genai), explorando o uso do **NotebookLM** como ferramenta de aprendizagem ativa com IA.

---

## 🧭 1. Contexto e Objetivos

### Contexto

O Laravel, sendo um dos frameworks PHP mais adotados no mercado, oferece uma estrutura robusta e elegante para a construção de APIs, com recursos nativos como autenticação, validação, rotas, recursos, middlewares e muito mais.

Este caderno temático foi criado para aprofundar os conhecimentos sobre **desenvolvimento de APIs RESTful utilizando Laravel**, combinando leitura ativa de fontes técnicas com a assistência do **NotebookLM (Google)** como ferramenta de síntese e geração de insights.

### Objetivos de Estudo

- ✅ Compreender os princípios fundamentais de uma API REST (verbos HTTP, status codes, idempotência)
- ✅ Dominar a estrutura de rotas de API no Laravel (`api.php`, Route::resource, Route::apiResource`)
- ✅ Entender autenticação stateless com **Laravel Sanctum** e **JWT**
- ✅ Aplicar boas práticas de versionamento, validação de dados e tratamento de erros
- ✅ Utilizar **API Resources** do Laravel para serialização consistente de respostas
- ✅ Documentar APIs com **Swagger/OpenAPI**

---

## 📂 2. Curadoria de Fontes

As fontes abaixo foram selecionadas por serem abertas, técnicas e diretamente relevantes ao tema. Todas foram carregadas no NotebookLM como base de conhecimento.

| # | Título | Tipo | Link |
|---|--------|------|------|
| 1 | **Laravel Documentation - HTTP Client & Routing** | Documentação Oficial | [laravel.com/docs](https://laravel.com/docs/routing) |
| 2 | **RESTful Web API Design - Microsoft Guidelines** | Guia Técnico (PDF/Web) | [learn.microsoft.com](https://learn.microsoft.com/en-us/azure/architecture/best-practices/api-design) |
| 3 | **PHP The Right Way** | Guia Open Source | [phptherightway.com](https://phptherightway.com) |
| 4 | **Laravel API Tutorial - Build a REST API (Tuts+)** | Artigo Técnico | [code.tutsplus.com](https://code.tutsplus.com/tutorials/laravel-restful-api-tutorial--cms-31801) |
| 5 | **HTTP Status Codes - RFC 9110** | Especificação RFC | [rfc-editor.org/rfc/rfc9110](https://www.rfc-editor.org/rfc/rfc9110) |

> 💡 **Observação:** As fontes 1, 2 e 3 foram adicionadas via link direto no NotebookLM. As fontes 4 e 5 foram salvas em PDF e feito upload manual.

---

## 🧪 3. Engenharia de Prompts e Aprendizados

Esta seção documenta as perguntas estratégicas elaboradas no NotebookLM, as respostas obtidas e os aprendizados do processo - incluindo ajustes e dificuldades (troubleshooting).

---

### 🔹 Prompt 1 - Conceito Central

**Objetivo:** Entender o que é uma API REST e como o Laravel se encaixa nesse contexto.

**Prompt utilizado:**
```
"Com base nas fontes carregadas, o que é uma API REST?
Explique de forma progressiva: conceito básico -> princípios REST -> como o Laravel implementa esses princípios nativamente."
```

**Resposta obtida:**

Uma API REST (Representational State Transfer) é um estilo arquitetural para sistemas distribuídos baseado em 6 restrições: interface uniforme, stateless, cache, client-server, sistema em camadas e código sob demanda. No Laravel, esses princípios se traduzem em: rotas bem definidas (`routes/api.php`), uso dos verbos HTTP (GET, POST, PUT, PATCH, DELETE), respostas em JSON via `response()->json()` e controle de estado via tokens (Sanctum/JWT) — sem sessões no servidor.

**Fonte citada pelo NotebookLM:** Microsoft REST API Guidelines + Documentação Laravel

**Dificuldades / Refinamento:**
> Na primeira tentativa, o prompt retornou uma resposta muito genérica sobre REST sem mencionar Laravel. Foi necessário adicionar a instrução *"como o Laravel implementa esses princípios nativamente"* para direcionar a resposta às fontes específicas do framework.

---

### 🔹 Prompt 2 - Estrutura de Rotas

**Objetivo:** Entender como organizar rotas de API no Laravel de forma escalável.

**Prompt utilizado:**
```
"Explique a diferença entre Route::resource e Route::apiResource no Laravel.
Quando devo usar cada um? Dê exemplos práticos de endpoints gerados por cada método."
```

**Resposta obtida:**

- `Route::resource` gera 7 rotas incluindo as de views (`create` e `edit`), adequado para aplicações web.
- `Route::apiResource` gera apenas 5 rotas (index, store, show, update, destroy), removendo as rotas de formulário — ideal para APIs puras.

**Exemplo de endpoints gerados por `Route::apiResource('posts', PostController::class)`:**

| Verbo | URI | Action |
|-------|-----|--------|
| GET | /posts | index |
| POST | /posts | store |
| GET | /posts/{post} | show |
| PUT/PATCH | /posts/{post} | update |
| DELETE | /posts/{post} | destroy |

**Fonte citada pelo NotebookLM:** Documentação Oficial Laravel

**Dificuldades / Refinamento:**
> O NotebookLM inicialmente misturou informações de versões diferentes do Laravel (9 e 11). Foi necessário adicionar ao prompt: *"Considere apenas o Laravel 11"* para obter uma resposta atualizada e consistente.

---

### 🔹 Prompt 3 - Autenticação com Sanctum

**Objetivo:** Compreender como implementar autenticação stateless em APIs Laravel.

**Prompt utilizado:**
```
"Como funciona a autenticação de APIs com Laravel Sanctum?
Explique o fluxo desde o registro do usuário até a proteção de rotas com middleware.
Compare brevemente com JWT."
```

**Resposta obtida:**

O Laravel Sanctum oferece autenticação via **tokens de API simples** (sem estado) e **autenticação de SPA via cookie**. Para APIs REST puras, o fluxo é:

1. Usuário envia `POST /login` com credenciais
2. A API valida e retorna um token via `$user->createToken('api-token')->plainTextToken`
3. O client envia o token no header: `Authorization: Bearer {token}`
4. As rotas protegidas usam o middleware `auth:sanctum`

**vs JWT:** O Sanctum armazena tokens no banco (revogáveis facilmente). O JWT é stateless puro (token autocontido), sem necessidade de banco — melhor para microsserviços, porém mais complexo de revogar.

**Fonte citada pelo NotebookLM:** Documentação Laravel (Sanctum)

**Dificuldades / Refinamento:**
> O prompt inicial não mencionava "comparação com JWT" e a resposta ficou incompleta para o objetivo de estudo. Adicionada a instrução de comparação na segunda tentativa.

---

### 🔹 Prompt 4 - Tratamento de Erros e Status Codes

**Objetivo:** Aprender boas práticas de resposta de erro em APIs REST.

**Prompt utilizado:**
```
"Quais são as boas práticas para tratamento de erros em APIs REST?
Liste os principais HTTP status codes e quando usar cada um.
Como o Laravel facilita o retorno de erros padronizados?"
```

**Resposta obtida:**

Boas práticas incluem: sempre retornar JSON estruturado, nunca expor stack traces em produção, e usar status codes semanticamente corretos.

| Status | Significado | Uso |
|--------|-------------|-----|
| 200 | OK | Requisição bem-sucedida |
| 201 | Created | Recurso criado com sucesso |
| 204 | No Content | DELETE bem-sucedido |
| 400 | Bad Request | Dados inválidos enviados |
| 401 | Unauthorized | Não autenticado |
| 403 | Forbidden | Autenticado mas sem permissão |
| 404 | Not Found | Recurso não encontrado |
| 422 | Unprocessable Entity | Falha de validação |
| 500 | Server Error | Erro interno |

No Laravel, o `Handler.php` (ou `bootstrap/app.php` no Laravel 11) centraliza o tratamento de exceções. Usar `abort(404)` ou lançar `ModelNotFoundException` retorna automaticamente a resposta correta.

**Fonte citada pelo NotebookLM:** RFC 9110 + Microsoft REST Guidelines

---

### 🔹 Prompt 5 - API Resources

**Objetivo:** Entender como padronizar as respostas JSON da API.

**Prompt utilizado:**
```
"O que são Laravel API Resources e por que devo usá-los?
Como criar um Resource e um ResourceCollection?
Dê um exemplo de resposta JSON antes e depois de usar Resources."
```

**Resposta obtida:**

**API Resources** são classes de transformação que desacoplam o modelo Eloquent da resposta JSON. Criados com `php artisan make:resource UserResource`.

**Sem Resource (resposta direta do Eloquent):**
```json
{ "id": 1, "name": "Lucas", "password": "$2y$...", "created_at": "..." }
```

**Com Resource (controlado e seguro):**
```json
{ "id": 1, "name": "Lucas", "email": "lucas@example.com" }
```

Vantagens: controle total dos campos expostos, ocultação de dados sensíveis, adição de metadados, consistência entre endpoints.

**Dificuldades / Refinamento:**
> Nenhuma dificuldade neste prompt, foi o mais objetivo e bem respondido de todos. O NotebookLM trouxe exemplos específicos na documentação Laravel e no artigo Tuts+.

---

## 📖 4. Miniguia de Estudo (Entrega Final)

### 🗂️ 4.1 Resumo Estruturado

#### Bloco 1 — Fundamentos REST
- REST é um **estilo arquitetural**, não um protocolo
- 6 restrições: stateless, uniform interface, client-server, cacheable, layered system, code on demand
- Recursos são identificados por **URIs** (ex: `/users/42`)
- Operações são expressas pelos **verbos HTTP** (GET, POST, PUT, PATCH, DELETE)

#### Bloco 2 — Laravel e APIs
- Rotas de API ficam em `routes/api.php` com prefixo `/api` automático
- Controllers de API são criados com `php artisan make:controller --api`
- `Route::apiResource` é o padrão para CRUD completo sem views
- Middlewares de grupo `api` já aplicam throttle (rate limiting) por padrão

#### Bloco 3 — Autenticação
- **Sanctum** → ideal para SPAs, mobile e APIs simples (tokens no banco, revogáveis)
- **JWT** → ideal para microsserviços (stateless puro, token autocontido)
- Sempre proteja rotas sensíveis com `middleware('auth:sanctum')`

#### Bloco 4 — Qualidade e Boas Práticas
- Use **Form Requests** (`php artisan make:request`) para validação desacoplada
- Use **API Resources** para serialização consistente e segura
- Padronize respostas de erro com um envelope JSON: `{ "message": "...", "errors": {...} }`
- Versione sua API via prefixo de rota: `/api/v1/`, `/api/v2/`
- Documente com **Swagger** via pacote `darkaonline/l5-swagger`

---

### 📝 4.2 Glossário

| Termo | Definição |
|-------|-----------|
| **REST** | Estilo arquitetural para sistemas distribuídos baseado em recursos e verbos HTTP |
| **Endpoint** | URL específica que representa um recurso ou ação na API |
| **Verbo HTTP** | Método da requisição (GET, POST, PUT, PATCH, DELETE) que define a operação |
| **Stateless** | Cada requisição deve conter todas as informações necessárias; o servidor não guarda estado da sessão |
| **JSON** | JavaScript Object Notation - formato padrão de troca de dados em APIs REST modernas |
| **Middleware** | Camada intermediária que intercepta requisições (autenticação, rate limit, CORS) |
| **Sanctum** | Pacote oficial do Laravel para autenticação de APIs via tokens simples ou cookies |
| **JWT** | JSON Web Token - token autocontido e assinado digitalmente, sem necessidade de armazenamento no servidor |
| **API Resource** | Classe Laravel que transforma modelos Eloquent em respostas JSON controladas |
| **Form Request** | Classe Laravel para validação e autorização desacoplada do Controller |
| **Route Model Binding** | Injeção automática de modelos Eloquent nas rotas com base no ID da URI |
| **Rate Limiting** | Controle de quantas requisições um cliente pode fazer em um período (throttle) |
| **Idempotência** | Propriedade de operações que produzem o mesmo resultado independentemente de quantas vezes são executadas |
| **CORS** | Cross-Origin Resource Sharing - política que controla quais domínios externos podem acessar a API |
| **Versionamento** | Prática de manter múltiplas versões da API (`/v1`, `/v2`) para não quebrar clientes existentes |

---

## 🛠️ Ferramentas Utilizadas

| Ferramenta | Uso |
|------------|-----|
| [NotebookLM](https://notebooklm.google.com) | Síntese das fontes e geração de respostas contextualizadas |
| [GitHub](https://github.com) | Repositório e documentação do projeto |
| [Laravel Docs](https://laravel.com/docs) | Fonte primária técnica |

---

## 👤 Autor

[![GitHub](https://img.shields.io/badge/GitHub-lucascottetpastor-black?style=flat&logo=github)](https://github.com/lucascottetpastor)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-lucas--cottet-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/lucascottet/)

---

*Projeto desenvolvido para Desafio de Projeto do [BootCamp do Bradesco na DIO](https://web.dio.me/track/bradesco-dados-ciberseguranca-genai) -> Caderno Temático com NotebookLM.*
