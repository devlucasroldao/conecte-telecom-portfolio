# 🌐 Conecte Telecom — Plataforma Web

> Auditoria de segurança, novas funcionalidades e otimização de uma plataforma web em produção para um provedor de internet com mais de 1.000 clientes ativos.

[![Site ao vivo](https://img.shields.io/badge/Site%20ao%20vivo-seconecte.net-0A62BA?style=for-the-badge&logo=vercel&logoColor=white)](https://seconecte.net)
[![Next.js](https://img.shields.io/badge/Next.js%2014-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)](https://nextjs.org)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org)
[![Supabase](https://img.shields.io/badge/Supabase-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](https://vercel.com)

> ⚠️ **Repositório de estudo de caso** — o código-fonte é propriedade da empresa e não está publicado aqui.

---

## 📖 Sobre o projeto

A Conecte Telecom é um provedor de internet fibra óptica em Arroio do Sal, RS, onde sou o responsável pelo marketing digital. Por iniciativa própria, assumi a evolução do site institucional que a empresa já tinha e transformei em uma plataforma completa: **auditoria de segurança, funcionalidades novas e otimização de performance**, até a migração para o domínio próprio da empresa.

## 📈 Em números

| | |
|---|---|
| Auditoria de segurança | 39 achados (5 críticos), todos corrigidos antes de qualquer incidente |
| Rastreamento de conversão | de 3 de 19 para 35 de 35 pontos de contato |
| Carregamento nas páginas afetadas | de 150–1000 ms para 2–20 ms |
| Contatos pelo WhatsApp vindos do site | cerca de 40 por mês (ago–set/2026) |

## ✨ Funcionalidades

**Site público**
- 🖊️ **Contratação 100% digital** — escolha de plano, leitura do contrato e assinatura eletrônica, com geração automática de PDF
- 📶 **Verificação de cobertura** por bairro, integrada ao WhatsApp comercial
- 🆘 **Central de Ajuda** com busca unificada e artigos por categoria

**Painel administrativo**
- 🔐 **2FA (TOTP)**, log de tentativas de login e rate limiting
- 📄 **Versionamento de contratos** — cada assinatura preserva o texto legal vigente naquele momento, mesmo que o modelo mude depois
- 📊 **Analytics de conversão próprio** — cliques em WhatsApp e planos, histórico mensal e exportação em PDF
- 🖼️ **Central de conteúdo** — textos, imagens, planos e cobertura editáveis sem tocar em código

---

## 🛠️ Stack Tecnológica

| Camada | Tecnologia | Decisão |
|---|---|---|
| **Frontend** | Next.js 14 (App Router) | Server Components, SSR nativo, deploy simples na Vercel |
| **Linguagem** | TypeScript | Segurança de tipo em um projeto com dado sensível (contrato, dado pessoal) |
| **Estilo** | Tailwind CSS | Consistência visual rápida de manter em painel + site público |
| **Banco de dados** | Supabase (PostgreSQL) | Row Level Security nativa, essencial dado o volume de dado pessoal envolvido |
| **Autenticação** | Supabase Auth + TOTP | 2FA na conta administrativa |
| **Deploy** | Vercel | CI/CD automático, domínio próprio da empresa |
| **Análise** | Google Analytics + Analytics próprio | Métrica de tráfego geral + rastreamento de conversão sob controle direto |

---

## 🗄️ Modelo de dados (resumo)

```sql
propostas_contrato    -- propostas de contrato e status de assinatura
contratos_templates   -- versionamento do texto legal dos contratos
planos / bairros      -- catálogo de planos e cobertura por bairro
eventos_clique        -- eventos de conversão (WhatsApp, planos)
configuracoes         -- conteúdo editável do site
admin_login_log       -- auditoria de tentativas de login administrativo
```

---

## 🔒 Segurança — um recorte do trabalho

Antes da migração para o domínio próprio da empresa, fiz uma auditoria de segurança completa na plataforma. Dela saíram:

- Correção de uma falha crítica de controle de acesso, validada em produção antes de qualquer incidente.
- Revisão completa das políticas de acesso a nível de linha (RLS) em toda a base de dados, incluindo tabelas criadas antes do versionamento formal de migrations.
- Armazenamento de contratos assinados em bucket privado, com acesso temporário por signed URLs.

*Detalhes técnicos da falha não são divulgados aqui, por princípio de divulgação responsável.*

---

## 🤖 IA como ferramenta de desenvolvimento

O projeto foi conduzido com Claude (Anthropic) como par de trabalho, com as decisões técnicas sob minha condução.

- **Investigação antes de correção** — confirmar a causa com evidência (log, reprodução controlada, consulta ao banco) antes de aplicar qualquer fix.
- **Causa raiz** — mais de uma vez o problema tinha origem diferente da hipótese inicial, como um bug de UI intermitente que era uma divergência de renderização entre servidor e cliente.

---

## 👨‍💻 Contato

**Lucas Roldão** · [LinkedIn](https://www.linkedin.com/in/devlucasroldao/) · [Portfólio](https://devlucasroldao.vercel.app) · lucasroldao2802@gmail.com
