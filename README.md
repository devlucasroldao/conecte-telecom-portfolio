# 🌐 Conecte Telecom — Plataforma Web

> Auditoria de segurança, novas funcionalidades e otimização de uma plataforma web em produção para um provedor de internet real, com mais de 1.000 clientes ativos.

[![Site ao vivo](https://img.shields.io/badge/Site%20ao%20vivo-seconecte.net-0A62BA?style=for-the-badge&logo=vercel&logoColor=white)](https://seconecte.net)
[![Next.js](https://img.shields.io/badge/Next.js%2014-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://vercel.com)

> ⚠️ **Repositório de portfólio** — o código-fonte é propriedade do cliente e não está publicado aqui.
> Este README documenta o trabalho técnico realizado, como estudo de caso.

---

## 📖 Sobre o Projeto

A Conecte Telecom é um provedor de internet fibra óptica real, em Arroio do Sal, RS. Fui responsável por levar a plataforma web já existente do cliente — site institucional, painel administrativo, contratação digital — por um processo completo: **auditoria de segurança, correção de vulnerabilidades reais, construção de funcionalidades novas do zero e otimização de performance**, culminando na migração para o domínio próprio da empresa.

Não é projeto de portfólio fictício. É produto em produção, com cliente real, tráfego real e dado real de mais de mil assinantes.

---

## 🖼️ Screenshots

> *Prints com dados fictícios/de teste serão adicionados em breve — nunca dado real de cliente.*

<!-- Adicionar prints aqui:
![Home](./screenshots/home.png)
![Central de Ajuda](./screenshots/ajuda.png)
![Assinatura de contrato](./screenshots/contrato.png)
![Painel de Analytics](./screenshots/analytics.png)
![Admin](./screenshots/admin.png)
-->

---

## ✨ Funcionalidades

### Site público
- 🏠 **Home institucional** com identidade visual própria, planos, cobertura por bairro e depoimentos reais
- 📶 **Verificação de cobertura** por bairro, integrada ao WhatsApp comercial
- 🖊️ **Contratação 100% digital** — formulário, escolha de plano, leitura de contrato e assinatura eletrônica, com geração automática de PDF
- 🎭 **Hero sazonal** — versões de conteúdo alternáveis (padrão/verão/inverno) para acompanhar a sazonalidade real do negócio
- 🆘 **Central de Ajuda** com busca unificada, categorias e artigos estruturados
- 📱 **Mobile-first**, com menu e navegação reformulados para clareza de uso

### Painel administrativo
- 🔐 **Autenticação em duas etapas (2FA/TOTP)**, log de tentativas de login e rate limiting
- 📄 **Gestão de contratos** com sistema de versionamento — cada proposta assinada preserva o texto legal exato vigente no momento da assinatura, mesmo que o modelo mude depois
- 📊 **Analytics de conversão construído do zero** — dezenas de pontos de clique (WhatsApp, planos) rastreados, com histórico mensal navegável e exportação de relatórios em PDF
- 🖼️ **Central de conteúdo** — textos, imagens, planos, depoimentos e cobertura editáveis sem tocar em código
- 🔗 **Página de links** (link-in-bio) com métricas próprias

---

## 🛠️ Stack Tecnológica

| Camada | Tecnologia | Decisão |
|---|---|---|
| **Frontend** | Next.js 14 (App Router) | Server Components, SSR nativo, deploy simples na Vercel |
| **Linguagem** | TypeScript | Segurança de tipo em um projeto com dado sensível (contrato, dado pessoal) |
| **Estilo** | Tailwind CSS | Consistência visual rápida de manter em painel + site público |
| **Banco de dados** | Supabase (PostgreSQL) | Row Level Security nativa, essencial dado o volume de dado pessoal envolvido |
| **Autenticação** | Supabase Auth + TOTP próprio | 2FA implementado para a conta administrativa |
| **Storage** | Supabase Storage (buckets públicos e privados) | Documentos assinados em bucket privado, com acesso via signed URL |
| **Deploy** | Vercel | CI/CD automático, domínio próprio do cliente |
| **Análise** | Google Analytics + Analytics próprio | Métrica de tráfego geral + rastreamento de conversão sob controle direto |

---

## 🗄️ Banco de Dados (Supabase / PostgreSQL) — visão geral

```sql
propostas_contrato    -- propostas de contrato e status de assinatura
contratos_templates   -- versionamento do texto legal dos contratos
planos                -- catálogo de planos de internet
depoimentos           -- avaliações reais exibidas no site
bairros               -- cobertura geográfica por bairro
ajuda_categorias      -- categorias da Central de Ajuda
ajuda_artigos         -- artigos publicados
eventos_clique        -- eventos de conversão (WhatsApp, planos)
links_botoes          -- botões da página de link-in-bio
configuracoes         -- conteúdo editável do site (textos, imagens, contatos)
admin_login_log       -- auditoria de tentativas de login administrativo
```

> Estrutura simplificada — tabelas auxiliares de rate limiting e MFA omitidas por não agregarem ao entendimento geral.

---

## 🔒 Segurança — um recorte do trabalho

Parte relevante deste projeto foi uma auditoria de segurança completa, que incluiu:

- Identificação e correção de uma falha de controle de acesso a dados que expunha informação pessoal de clientes via API pública — corrigida e validada em produção antes de qualquer incidente registrado.
- Bloqueio de uma rota que permitia gerar documentos com identidade visual e dados legais da empresa sem nenhuma transação real associada.
- Revisão completa de políticas de acesso a nível de linha (RLS) em toda a base de dados, incluindo tabelas criadas antes do início do versionamento formal de migrations.
- Armazenamento de documentos sensíveis (contratos assinados) em bucket privado, com acesso temporário controlado por signed URLs — nunca exposição direta.

*Detalhes técnicos de exploração não são divulgados aqui por princípio de divulgação responsável — o foco é o processo e a solução, não o vetor.*

---

## 🤖 IA como Ferramenta de Desenvolvimento

Este projeto foi conduzido com uso intencional de IA (Claude, Anthropic) como par de trabalho — não como substituto de decisão técnica, mas como acelerador de execução sob minha condução direta.

- **Investigação antes de correção** — toda vez que um bug parecia ter uma causa óbvia, a prática foi confirmar com evidência real (log, reprodução controlada, consulta direta ao banco) antes de aplicar qualquer fix.
- **Auditoria assistida** — varreduras completas de segurança e de consistência de dado (ex: identificar números de contato divergentes espalhados pelo código) feitas de forma sistemática, não pontual.
- **Correção de causa raiz** — mais de uma vez, o problema relatado tinha origem completamente diferente da hipótese inicial (ex: um bug de UI intermitente que na real era uma divergência de renderização entre servidor e cliente).

> A diferença entre "parece corrigido" e "está corrigido" só aparece quando alguém força a verificação real em vez de aceitar a explicação mais plausível. Foi o princípio que guiou o projeto inteiro.

---

## 👨‍💻 Sobre o Desenvolvedor

**Lucas Roldão** — desenvolvedor responsável pela manutenção, segurança e evolução da plataforma da Conecte Telecom.

Este projeto representa minha capacidade de:
- Auditar e corrigir vulnerabilidades reais em produção, sem interromper a operação do cliente
- Construir funcionalidades completas do zero (contratação digital, analytics de conversão)
- Tomar decisões de arquitetura de dado com dado sensível envolvido
- Diagnosticar problemas de performance e renderização até a causa raiz
- Usar IA de forma estratégica, mantendo o julgamento técnico sob controle humano

📧 Aberto a oportunidades — entre em contato!

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/devlucasroldao/)
[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/devlucasroldao)

---

<div align="center">
  <p>Feito com atenção a detalhe e disciplina de verificação por Lucas Roldão</p>
</div>
