# Análise Técnica Completa — datacx-mentoria

**Projeto:** Data CX Mentoria (Protocolo Vértice)  
**Domínios:** datacxmento-63ijiyeh.manus.space | datacxmentoria.business  
**Data da análise:** 01/03/2026  
**Autor:** Manus AI  

---

## 1. Visão Geral do Projeto

O **datacx-mentoria** é uma plataforma completa de mentoria em CX, Dados e IA, desenvolvida para o mentor **Samuel Rosa**. A plataforma combina landing pages públicas, área de membros com conteúdo educacional (60 módulos), sistema de avaliação de perfil profissional com IA, jornadas de acompanhamento, comunidade, gamificação, workspace de consultoria, e integração com Stripe para pagamentos.

O projeto foi construído ao longo de **70 fases de desenvolvimento**, acumulando **982 itens concluídos** e **9 itens pendentes** no todo.md. O codebase possui **267 testes automatizados** passando em 24 arquivos de teste.

---

## 2. Stack Tecnológica

| Camada | Tecnologia | Versão |
|--------|-----------|--------|
| **Frontend** | React + TypeScript | React 19.2, TS 5.9 |
| **Estilização** | Tailwind CSS 4 + shadcn/ui | Tailwind 4.1 |
| **Animações** | Framer Motion | 12.23 |
| **Roteamento** | Wouter | 3.3 |
| **Estado/API** | tRPC + TanStack Query | tRPC 11.6, TQ 5.90 |
| **Backend** | Express + tRPC | Express 4.21 |
| **Banco de dados** | MySQL/TiDB + Drizzle ORM | Drizzle 0.44 |
| **Autenticação** | Manus OAuth + Email/Senha (bcryptjs) | — |
| **Pagamentos** | Stripe | 20.3 |
| **Email** | Resend | 6.9 |
| **IA/LLM** | OpenAI (via Manus Forge API) | 6.19 |
| **Storage** | AWS S3 | — |
| **Build** | Vite 7 + esbuild | — |
| **Testes** | Vitest | 2.1 |
| **Runtime** | Node.js 22 + tsx (dev) | — |

---

## 3. Estrutura de Arquivos

```
datacx-mentoria/
├── client/
│   ├── public/                    # Arquivos estáticos (manifest, sw.js, robots.txt)
│   ├── index.html                 # HTML principal (Google Fonts, meta tags)
│   └── src/
│       ├── components/            # Componentes reutilizáveis
│       │   ├── ui/                # shadcn/ui (50+ componentes)
│       │   ├── Navbar.tsx         # Navbar principal (237 linhas)
│       │   ├── Footer.tsx         # Footer global (175 linhas)
│       │   ├── DashboardLayout.tsx # Layout sidebar (264 linhas)
│       │   ├── MembersSidebar.tsx # Sidebar da área de membros (246 linhas)
│       │   ├── JornadaManager.tsx # Gestão de jornadas (1407 linhas)
│       │   ├── RadarHistorySection.tsx # Histórico do Radar (1283 linhas)
│       │   ├── AssessmentComparison.tsx # Comparação de assessments (349 linhas)
│       │   ├── AIChatBox.tsx      # Chat com IA (335 linhas)
│       │   ├── AIAssistant.tsx    # Assistente flutuante (328 linhas)
│       │   ├── ShareBadgeModal.tsx # Compartilhar medalhas (295 linhas)
│       │   ├── OnboardingWelcome.tsx # Onboarding (146 linhas)
│       │   ├── SEO.tsx            # Meta tags SEO (150 linhas)
│       │   ├── JsonLd.tsx         # Schema.org (217 linhas)
│       │   ├── Map.tsx            # Google Maps (155 linhas)
│       │   └── ErrorBoundary.tsx  # Error boundary
│       ├── contexts/
│       │   └── ThemeContext.tsx    # Dark/light theme
│       ├── hooks/
│       │   ├── useComposition.ts
│       │   ├── useMobile.tsx
│       │   └── usePersistFn.ts
│       ├── lib/
│       │   ├── trpc.ts            # tRPC client binding
│       │   ├── analytics.ts       # Analytics tracking
│       │   └── utils.ts           # Utilidades (cn, etc.)
│       ├── pages/                 # 35 páginas (ver seção 4)
│       ├── App.tsx                # Rotas + layout (138 linhas)
│       ├── main.tsx               # Providers
│       ├── index.css              # Tokens de design, tema global
│       └── const.ts               # Constantes (login URL, etc.)
├── server/
│   ├── _core/                     # Framework (NÃO EDITAR)
│   │   ├── index.ts               # Entry point do servidor
│   │   ├── context.ts             # tRPC context (user, req)
│   │   ├── trpc.ts                # publicProcedure, protectedProcedure
│   │   ├── oauth.ts               # Manus OAuth handler
│   │   ├── env.ts                 # Variáveis de ambiente
│   │   ├── llm.ts                 # invokeLLM helper
│   │   ├── notification.ts        # notifyOwner helper
│   │   ├── imageGeneration.ts     # generateImage helper
│   │   ├── voiceTranscription.ts  # transcribeAudio helper
│   │   ├── tts.ts                 # Text-to-speech
│   │   ├── dataApi.ts             # Data API (Yahoo Finance, etc.)
│   │   ├── map.ts                 # Google Maps backend
│   │   ├── sdk.ts                 # Forge SDK
│   │   ├── cookies.ts             # Cookie handling
│   │   ├── vite.ts                # Vite middleware
│   │   └── systemRouter.ts        # System tRPC router
│   ├── routers.ts                 # TODOS os tRPC routers (3353 linhas) ⚠️
│   ├── db.ts                      # Query helpers (3389 linhas) ⚠️
│   ├── storage.ts                 # S3 helpers (storagePut, storageGet)
│   ├── products.ts                # Definição dos produtos Stripe
│   ├── emailService.ts            # Serviço de email (Resend)
│   ├── emailAuth.ts               # Auth por email/senha
│   ├── onboardingEmails.ts        # Drip campaign
│   ├── weeklyReport.ts            # Relatório semanal
│   ├── nurtureProcessor.ts        # Nurture de leads
│   ├── openaiChat.ts              # Chat com OpenAI
│   ├── apostilaGenerator.ts       # Gerador de apostilas
│   ├── certificateGenerator.ts    # Gerador de certificados
│   ├── assessment/
│   │   ├── scoringEngine.ts       # Motor de pontuação
│   │   ├── reportGenerator.ts     # Gerador de relatório IA
│   │   └── pdfGenerator.ts        # Gerador de PDF (NÃO FUNCIONAL)
│   └── *.test.ts                  # 24 arquivos de teste
├── drizzle/
│   ├── schema.ts                  # Schema do banco (1150 linhas, 40+ tabelas)
│   └── relations.ts               # Relações Drizzle
├── shared/
│   ├── types.ts                   # Tipos compartilhados
│   ├── const.ts                   # Constantes compartilhadas
│   └── challengeSegments.ts       # Segmentação de leads
├── scripts/                       # Scripts de geração de conteúdo
├── package.json
├── vite.config.ts
├── vitest.config.ts
├── drizzle.config.ts
├── tsconfig.json
└── todo.md                        # Histórico de 70 fases (1644 linhas)
```

---

## 4. Rotas e Páginas

### 4.1 Páginas Públicas (sem autenticação)

| Rota | Componente | Descrição |
|------|-----------|-----------|
| `/` | Home.tsx (806 linhas) | Landing page principal |
| `/sobre` | About.tsx | Sobre o mentor Samuel Rosa |
| `/ofertas` (+ `/programas`, `/planos`, `/precos`) | Offers.tsx (1031 linhas) | Planos e preços |
| `/contato` | Contact.tsx (745 linhas) | Formulário de contato |
| `/radar` (+ `/radar-vertice`) | RadarVertice.tsx (1854 linhas) | Autoavaliação Radar Vértice |
| `/mentoria-jovens` | MentoriaJovens.tsx | Página da persona Jovens |
| `/mentoria-gestores` | MentoriaGestores.tsx | Página da persona Gestores |
| `/mentoria-executivos` | MentoriaExecutivos.tsx | Página da persona Executivos |
| `/empresas` | Empresas.tsx | Página para empresas |
| `/cases/120-matriculas` (+ `/cases/fco`, `/case-fco`, `/case`) | CaseFCO.tsx | Case de sucesso FCO |
| `/avaliacao-de-perfil` | AssessmentLanding.tsx (926 linhas) | Landing do Assessment |
| `/login` | Login.tsx (496 linhas) | Login email/senha + OAuth |
| `/reset-password` | ResetPassword.tsx | Reset de senha |
| `/privacidade` | Privacidade.tsx | Política de privacidade |
| `/verificar-certificado` | VerifyCertificate.tsx | Verificação pública de certificados |

### 4.2 Páginas Protegidas (requer autenticação)

| Rota | Componente | Descrição |
|------|-----------|-----------|
| `/membros` | Members.tsx (1441 linhas) | Área de membros (conteúdos, soluções) |
| `/membros/conteudo/:id` | ContentView.tsx (1095 linhas) | Visualização de conteúdo individual |
| `/conteudos` | Conteudos.tsx (428 linhas) | Biblioteca de conteúdos |
| `/perfil` | Profile.tsx (860 linhas) | Perfil do usuário |
| `/jornada` | Jornada.tsx (478 linhas) | Jornada de acompanhamento |
| `/comunidade` | Comunidade.tsx (483 linhas) | Fórum da comunidade |
| `/workspace` (+ `/:projectId`) | Workspace.tsx (592 linhas) | Workspace de consultoria |
| `/eventos` | Eventos.tsx | Eventos e office hours |
| `/mensagens` (+ `/:recipientId`) | Mensagens.tsx | Mensagens diretas |
| `/certificados` | Certificates.tsx (734 linhas) | Certificados do usuário |
| `/assessment` (+ `/:sessionId`) | Assessment.tsx (1155 linhas) | Avaliação de perfil |
| `/quiz/:contentId` | Quiz.tsx (414 linhas) | Quizzes de módulos |
| `/upgrade` | Upgrade.tsx (631 linhas) | Upgrade de plano |
| `/pagamento-sucesso` | PaymentSuccess.tsx | Confirmação de pagamento |
| `/ajuda` | Help.tsx | Central de ajuda |
| `/admin` | Admin.tsx (2745 linhas) | Painel administrativo |

---

## 5. Schema do Banco de Dados (40+ Tabelas)

### 5.1 Tabelas Principais

| Tabela | Descrição | Campos-chave |
|--------|-----------|-------------|
| `users` | Usuários (OAuth + email/senha) | id, openId, email, role (admin/user), passwordHash, avatarUrl, phone, company, position |
| `mentorship_programs` | Programas de mentoria | slug, name, type, price, stripePriceId, isActive |
| `enrollments` | Matrículas | userId, programId, status, paymentStatus, stripeSubscriptionId |
| `contents` | Conteúdos/módulos (60+) | title, type, category, moduleCode, nivel, pilar, fileUrl, videoUrl, markdownContent |
| `user_progress` | Progresso do aluno | userId, contentId, completed |

### 5.2 Tabelas de Controle de Acesso

| Tabela | Descrição |
|--------|-----------|
| `plan_module_access` | Mapeamento plano → módulos acessíveis |
| `user_module_overrides` | Overrides admin (grant/revoke por usuário) |

### 5.3 Tabelas de Gamificação

| Tabela | Descrição |
|--------|-----------|
| `user_points` | Pontos e nível do usuário |
| `point_transactions` | Histórico de transações de pontos |
| `badges` | Definição de medalhas |
| `user_badges` | Medalhas conquistadas |

### 5.4 Tabelas da Comunidade

| Tabela | Descrição |
|--------|-----------|
| `community_posts` | Posts do fórum (com spaces) |
| `community_comments` | Comentários (nested) |
| `community_likes` | Curtidas em posts/comentários |
| `community_events` | Eventos (office hours, workshops) |
| `event_registrations` | Inscrições em eventos |
| `direct_messages` | Mensagens diretas entre usuários |
| `notifications` | Notificações do sistema |

### 5.5 Tabelas do Radar Vértice

| Tabela | Descrição |
|--------|-----------|
| `radar_leads` | Leads capturados (scores, respostas, segmentação) |
| `radar_nurture_messages` | Sequência de nurture automatizada |

### 5.6 Tabelas de Consultoria/Jornada

| Tabela | Descrição |
|--------|-----------|
| `consulting_projects` | Projetos de consultoria |
| `project_tasks` | Tarefas do projeto |
| `project_documents` | Documentos do projeto |
| `project_meetings` | Reuniões e atas |
| `project_milestones` | Marcos do projeto |
| `project_stages` | Etapas da jornada |
| `stage_contents` | Conteúdos por etapa (docs, vídeos, links, texto, áudio) |
| `stage_checklist_items` | Checklist por etapa |
| `stage_checklist_progress` | Progresso do checklist por usuário |
| `stage_comments` | Comentários nas etapas |
| `stage_deliverables` | Entregas por etapa |
| `stage_member_progress` | Progresso do membro na etapa |
| `project_chats` | Chat do projeto |

### 5.7 Tabelas do Assessment

| Tabela | Descrição |
|--------|-----------|
| `assessment_item_bank` | Banco de itens (60 questões: likert, SJT, micro_work_sample, attention_check) |
| `assessment_sessions` | Sessões de avaliação |
| `assessment_responses` | Respostas individuais |
| `assessment_scores` | Scores computados por bloco/constructo |
| `assessment_reports` | Relatórios gerados por IA (JSON + PDF) |

### 5.8 Outras Tabelas

| Tabela | Descrição |
|--------|-----------|
| `certificates` | Certificados emitidos |
| `quizzes` | Quizzes dos módulos |
| `quiz_questions` | Perguntas dos quizzes |
| `quiz_attempts` | Tentativas de quiz |
| `module_chats` | Chat com Tutor IA por módulo |
| `module_materials` | Materiais versionados |
| `content_persona_versions` | Apostilas + áudios por persona |
| `chat_feedback` | Feedback do Tutor IA (estrelas) |
| `scheduled_emails` | Emails agendados (drip campaign) |
| `coupons` | Cupons de desconto |
| `coupon_usages` | Uso de cupons |
| `contact_submissions` | Submissões de contato |
| `testimonials` | Depoimentos |
| `analytics_events` | Eventos de analytics |
| `audit_logs` | Logs de auditoria |
| `system_health_logs` | Logs de saúde do sistema |

---

## 6. Routers tRPC (28 namespaces)

O arquivo `server/routers.ts` possui **3353 linhas** com todos os routers em um único arquivo. Abaixo a lista completa de namespaces:

| Namespace | Tipo | Procedures principais |
|-----------|------|----------------------|
| `auth` | Público + Protegido | me, logout, updateProfile, register, login, requestPasswordReset, resetPassword |
| `programs` | Público + Admin | list, listAll, getBySlug, create, update |
| `enrollments` | Protegido + Admin | myEnrollments, listAll, create, updateStatus, updateEndDate |
| `contents` | Protegido + Admin | list, listByCategory, getById, trails, byPilar, byCode, search, withProgress, checkAccess, accessibleModules, create, update, delete, bulkSetReleaseDates |
| `progress` | Protegido | myProgress, markComplete |
| `testimonials` | Público + Admin | listActive, listAll, create, update, delete |
| `contact` | Público + Admin | submit, listAll, updateStatus |
| `admin` | Admin | metrics, users, getUser, updateUser, deleteUser, analytics, enhancedMetrics, feedbackList, feedbackStatsByModule, studentProgress, moduleEngagement, quizPerformance, getUserAccess, setModuleOverride, removeModuleOverride, grantAllModules, revokeAllOverrides, getPlanModuleMapping |
| `radar` | Público + Admin | submit, getResult, listAll, metrics, updateStatus, generateAnalysis, saveAnalysis, sendDiagnosticEmail, getHistory, segmentTrends, leadsBySegment, sendWhatsappFollowup, sendSegmentNurture, sendWeeklyReport |
| `analytics` | Público | track |
| `stripe` | Público + Protegido | getProducts, createCheckout, getPaymentHistory |
| `coupons` | Admin | validate, listAll, metrics, getById, getUsages, create, update, delete, toggleActive |
| `gamification` | Protegido | myPoints, leaderboard, myBadges, allBadges, myTransactions, myStats |
| `community` | Protegido + Admin | (posts, comments, likes CRUD) |
| `certificates` | Protegido + Admin | myCertificates, getById, verify, getCategoryProgress, generate, generateCategory, listAll |
| `quizzes` | Protegido + Admin | create, addQuestion, getByContent, submitAttempt, myAttempts |
| `ai` | Público | chat |
| `moduleChat` | Protegido | getHistory, getFeedback, submitFeedback |
| `consulting` | Protegido + Admin | listProjects, getProject, createProject, updateProject, getTasks, createTask, updateTask, deleteTask, getDocuments, uploadDocument, deleteDocument, getMeetings, createMeeting, updateMeeting, getChatMessages, sendChatMessage, getMilestones, createMilestone, updateMilestone, getStages, createStage, updateStage, deleteStage, reorderStages, getDeliverables, createDeliverable, updateDeliverable, deleteDeliverable, journeyDashboard, getStageContents, createStageContent, updateStageContent, deleteStageContent, getChecklistItems, createChecklistItem, updateChecklistItem, deleteChecklistItem, toggleChecklist, getComments, addComment, deleteComment, updateMemberProgress, getFullStageDetail, allProjectsWithStages, uploadStageFile |
| `events` | Protegido + Admin | list, upcoming, create, update, register, getRegistrations |
| `dm` | Protegido | getConversations, getMessages, send, unreadCount |
| `notifications` | Protegido | list, markAsRead, markAllAsRead |
| `audit` | Admin | list, logs, stats |
| `health` | Protegido | get |
| `userPersona` | Protegido | get |
| `personaVersions` | Protegido + Admin | byContent, getContentWithPersona, statusOverview, generateApostila, batchGenerate |
| `assessment` | Protegido + Admin | getItems, startSession, saveResponses, complete, getSession, getReport, myHistory, getScores, getCompletedSessions, compareScores, adminStats, linkPdiToJornada |

---

## 7. Variáveis de Ambiente Necessárias

### 7.1 Variáveis do Sistema (injetadas automaticamente pelo Manus)

| Variável | Descrição | Onde é usada |
|----------|-----------|-------------|
| `DATABASE_URL` | Connection string MySQL/TiDB | Drizzle ORM |
| `JWT_SECRET` | Secret para cookies de sessão | server/_core/cookies.ts |
| `VITE_APP_ID` | ID do app Manus OAuth | OAuth flow |
| `OAUTH_SERVER_URL` | URL do servidor OAuth Manus | server/_core/oauth.ts |
| `VITE_OAUTH_PORTAL_URL` | URL do portal de login Manus | Frontend login |
| `OWNER_OPEN_ID` | OpenID do owner | Identificação do admin |
| `OWNER_NAME` | Nome do owner | Notificações |
| `BUILT_IN_FORGE_API_URL` | URL da API Forge (LLM, storage, etc.) | server/_core/llm.ts, etc. |
| `BUILT_IN_FORGE_API_KEY` | Bearer token API Forge (server) | server/_core/sdk.ts |
| `VITE_FRONTEND_FORGE_API_KEY` | Bearer token API Forge (frontend) | Client-side API calls |
| `VITE_FRONTEND_FORGE_API_URL` | URL API Forge (frontend) | Client-side API calls |

### 7.2 Variáveis de Serviços Externos

| Variável | Descrição | Serviço |
|----------|-----------|---------|
| `OPENAI_API_KEY` | Chave da API OpenAI | Chat IA, Assessment, Apostilas |
| `RESEND_API_KEY` | Chave da API Resend | Envio de emails |
| `EMAIL_FROM` | Email remetente | Emails transacionais |
| `STRIPE_SECRET_KEY` | Chave secreta Stripe | Pagamentos (server) |
| `VITE_STRIPE_PUBLISHABLE_KEY` | Chave pública Stripe | Pagamentos (frontend) |
| `STRIPE_WEBHOOK_SECRET` | Secret do webhook Stripe | Verificação de webhooks |
| `MAKE_WEBHOOK_URL` | URL do webhook Make.com | Automações |

### 7.3 Variáveis de Configuração

| Variável | Descrição |
|----------|-----------|
| `VITE_APP_TITLE` | Título do app ("Data CX Mentoria") |
| `VITE_APP_LOGO` | URL do logo |
| `VITE_ANALYTICS_ENDPOINT` | Endpoint de analytics |
| `VITE_ANALYTICS_WEBSITE_ID` | ID do website para analytics |

### 7.4 Nota sobre o Banco de Dados

O projeto usa **MySQL/TiDB** (não SQLite). A variável `DATABASE_URL` segue o formato:
```
mysql://user:password@host:port/database?ssl={"rejectUnauthorized":true}
```

Para rodar localmente, você precisará de um MySQL 8+ ou TiDB. **Não é possível usar SQLite** sem refatorar todo o schema (usa tipos específicos do MySQL como `mysqlEnum`, `mysqlTable`).

---

## 8. Bugs Conhecidos e Problemas

### 8.1 Bugs Críticos (Funcionalidade Quebrada)

| # | Bug | Localização | Impacto | Detalhes |
|---|-----|-------------|---------|----------|
| 1 | **Assessment PDF não é gerado no servidor** | `server/assessment/pdfGenerator.ts` | O campo `pdfUrl` na tabela `assessment_reports` nunca é preenchido. O download de PDF foi implementado no client-side via `html2pdf.js`, mas depende do usuário estar na página do relatório. | O arquivo `pdfGenerator.ts` existe mas não é chamado em nenhum lugar do `routers.ts`. |
| 2 | **Resumo Executivo do Assessment pode ficar vazio** | `server/assessment/reportGenerator.ts` | Quando o LLM não retorna os campos `executive_summary`, `fit_and_context`, ou `disclaimer`, o relatório fica incompleto. | Fallbacks foram adicionados recentemente (Fase 69), mas dependem da qualidade da resposta do LLM. |
| 3 | **Cron de emails falha com ECONNRESET** | `server/_core/index.ts` (cron jobs) | Emails agendados e nurture não são processados quando a conexão DB cai. | Erro: `DrizzleQueryError: read ECONNRESET`. Falta retry/reconnect no pool de conexões. |
| 4 | **Vídeos são placeholders** | Múltiplas páginas de conteúdo | Vários módulos mostram "Vídeo em breve" em vez de vídeos reais. | Pendente: aguardando URLs do YouTube quando vídeos forem gravados. |

### 8.2 Bugs de UI/UX (Experiência Degradada)

| # | Bug | Localização | Impacto |
|---|-----|-------------|---------|
| 5 | **routers.ts com 3353 linhas** | `server/routers.ts` | Arquivo monolítico dificulta manutenção. Deveria ser dividido em `server/routers/*.ts`. |
| 6 | **db.ts com 3389 linhas** | `server/db.ts` | Mesmo problema — arquivo monolítico com todos os query helpers. |
| 7 | **Admin.tsx com 2745 linhas** | `client/src/pages/Admin.tsx` | Componente gigante, difícil de manter. Deveria ser dividido em sub-componentes. |

### 8.3 Itens Pendentes no todo.md (9 itens)

| # | Item Pendente | Contexto |
|---|--------------|----------|
| 1 | Configurar conta Stripe em produção (Settings → Payment) | Configuração manual do owner |
| 2 | Vincular conta Itaú (Ag: 9056, Cc: 06562-7) no Stripe | Configuração bancária |
| 3 | Configurar Chave PIX: 33a47e94-22f8-4dba-b44f-3f79ab2f2889 | Configuração PIX |
| 4 | Melhorar hospedagem de vídeos | Infraestrutura |
| 5 | Adicionar depoimentos e evidências do resultado (aguardando materiais) | Conteúdo |
| 6 | Adicionar URLs do YouTube quando vídeos estiverem gravados | Conteúdo |
| 7 | Substituir placeholders "Vídeo em breve" | Conteúdo |
| 8 | Revisar valores dos planos (exceto Playbook) | Negócio |
| 9 | Atualizar valores dos planos no código | Negócio |

---

## 9. Produtos Stripe Definidos

| ID | Nome | Preço | Tipo |
|----|------|-------|------|
| `playbook_vertice` | Playbook Protocolo Vértice | R$ 497,00 | one_time |
| `mentoria_grupo` | Mentoria em Grupo — Protocolo Vértice | R$ 1.997,00 | one_time |
| `mentoria_sprint` | Mentoria Sprint 1:1 | R$ 2.977,00 | one_time |
| `mentoria_90dias` | Mentoria Vértice 90 Dias | R$ 5.977,00 | one_time |
| `mentoria_executive` | Mentoria Executive | R$ 14.977,00 | one_time |
| `diagnostico_360` | Diagnóstico Vértice 360º | R$ 4.977,00 | one_time |
| `assessoria_mensal` | Assessoria Vértice | R$ 9.977,00/mês | recurring |
| `assessoria_semestral` | Assessoria Vértice 6 Meses | R$ 8.977,00/mês | recurring |
| `assessoria_anual` | Assessoria Vértice 12 Meses | R$ 7.977,00/mês | recurring |

**Nota:** Os valores dos planos estão pendentes de revisão pelo owner (itens 8 e 9 do todo.md).

---

## 10. Testes Automatizados

O projeto possui **24 arquivos de teste** com **267 testes** passando:

| Arquivo de Teste | Testes | Descrição |
|-----------------|--------|-----------|
| `auth.logout.test.ts` | — | Teste de logout |
| `access-control.test.ts` | 17 | Controle de acesso por plano |
| `admin-metrics.test.ts` | — | Métricas admin |
| `assessment.test.ts` | — | Assessment completo |
| `certificateGenerator.test.ts` | — | Geração de certificados |
| `certificates.test.ts` | — | CRUD certificados |
| `chat-feedback.test.ts` | — | Feedback do chat IA |
| `contact.test.ts` | 5 | Formulário de contato |
| `coupons.test.ts` | — | Sistema de cupons |
| `email.test.ts` | — | Envio de emails |
| `emailAuth.test.ts` | — | Auth por email/senha |
| `emailService.test.ts` | — | Serviço de email |
| `jornada.test.ts` | — | Jornada de acompanhamento |
| `make-webhook.test.ts` | 3 | Webhook Make.com |
| `onboardingEmails.test.ts` | — | Emails de onboarding |
| `openai-key.test.ts` | — | Chave OpenAI |
| `personaVersions.test.ts` | — | Versões por persona |
| `radar.test.ts` | 20 | Radar Vértice |
| `radarAnalysis.test.ts` | — | Análise do Radar |
| `radarHistory.test.ts` | — | Histórico do Radar |
| `releaseSchedule.test.ts` | — | Agendamento de releases |
| `seo.test.ts` | — | SEO meta tags |
| `stripe.test.ts` | — | Integração Stripe |
| `v2-content.test.ts` | — | Conteúdos V2 |

---

## 11. Comandos para Rodar o Projeto

```bash
# Instalar dependências
pnpm install

# Configurar variáveis de ambiente
# Criar arquivo .env na raiz com todas as variáveis da seção 7

# Gerar e aplicar migrações do banco
pnpm db:push

# Rodar em desenvolvimento
pnpm dev

# Rodar testes
pnpm test

# Build de produção
pnpm build

# Rodar produção
pnpm start

# Verificar tipos TypeScript
pnpm check
```

---

## 12. Arquitetura de Autenticação

O projeto suporta **dois métodos de autenticação**:

**Manus OAuth:** O fluxo padrão via `server/_core/oauth.ts`. O callback em `/api/oauth/callback` cria/atualiza o usuário e seta um cookie JWT. O frontend usa `getLoginUrl()` de `client/src/const.ts` para redirecionar.

**Email/Senha:** Implementado em `server/emailAuth.ts` com bcryptjs. Suporta registro, login, reset de senha via email (Resend). Os campos `passwordHash`, `emailVerified`, `resetToken`, `resetTokenExpiry` na tabela `users` são usados por este fluxo.

O `protectedProcedure` em `server/_core/trpc.ts` verifica o cookie JWT e injeta `ctx.user`. O `adminProcedure` em `server/routers.ts` adiciona verificação de `ctx.user.role === 'admin'`.

---

## 13. Integrações Externas

| Integração | Uso | Arquivos |
|-----------|-----|----------|
| **Stripe** | Pagamentos (checkout, webhooks, histórico) | `server/routers.ts` (stripe namespace), `server/products.ts` |
| **OpenAI** | Chat IA, Assessment report, Apostilas, Análise Radar | `server/openaiChat.ts`, `server/assessment/reportGenerator.ts`, `server/apostilaGenerator.ts` |
| **Resend** | Emails transacionais e marketing | `server/emailService.ts`, `server/onboardingEmails.ts` |
| **Make.com** | Webhook para automações | `server/routers.ts` (contact.submit) |
| **AWS S3** | Storage de arquivos (PDFs, imagens, áudios) | `server/storage.ts` |
| **Manus Forge API** | LLM, TTS, Image Generation, Data API | `server/_core/llm.ts`, `server/_core/tts.ts`, etc. |
| **Google Maps** | Mapas (componente frontend) | `client/src/components/Map.tsx`, `server/_core/map.ts` |

---

## 14. Recomendações para Manutenção

### 14.1 Refatorações Prioritárias

1. **Dividir `server/routers.ts`** (3353 linhas) em arquivos separados por namespace: `server/routers/auth.ts`, `server/routers/admin.ts`, `server/routers/assessment.ts`, etc. Usar `router.merge()` para compor.

2. **Dividir `server/db.ts`** (3389 linhas) em módulos: `server/db/users.ts`, `server/db/contents.ts`, `server/db/assessment.ts`, etc.

3. **Dividir `client/src/pages/Admin.tsx`** (2745 linhas) em sub-componentes: `AdminDashboard`, `AdminUsers`, `AdminContents`, `AdminCoupons`, `AdminRadar`, etc.

4. **Implementar retry/reconnect** no pool de conexões MySQL para evitar erros `ECONNRESET` nos cron jobs.

### 14.2 Funcionalidades Incompletas

1. **PDF do Assessment no servidor** — O `pdfGenerator.ts` existe mas não é integrado. Atualmente o PDF é gerado no client-side via `html2pdf.js`.

2. **Vídeos dos módulos** — Muitos módulos têm placeholder "Vídeo em breve". Quando os vídeos forem gravados, atualizar os campos `videoUrl` nos conteúdos via admin.

3. **Valores dos planos** — Os preços em `server/products.ts` precisam ser revisados e atualizados.

### 14.3 Pontos de Atenção

O projeto depende fortemente da **Manus Forge API** para LLM, storage, notificações e outros serviços. Se migrar para fora do Manus, será necessário substituir os helpers em `server/_core/` por implementações diretas (OpenAI SDK, AWS SDK, etc.).

A autenticação via **Manus OAuth** também precisará ser substituída se o projeto sair do ecossistema Manus. O fluxo de email/senha já existe como alternativa.

---

## 15. Resumo de Métricas do Projeto

| Métrica | Valor |
|---------|-------|
| Fases de desenvolvimento | 70 |
| Itens concluídos (todo.md) | 982 |
| Itens pendentes (todo.md) | 9 |
| Arquivos de teste | 24 |
| Testes automatizados | 267 |
| Páginas/rotas | 35 |
| Tabelas no banco | 40+ |
| Namespaces tRPC | 28 |
| Linhas em routers.ts | 3.353 |
| Linhas em db.ts | 3.389 |
| Linhas em schema.ts | 1.150 |
| Dependências (prod) | 60+ |
| Dependências (dev) | 17 |
