# Aprovacard

**Cartão NFC que leva o cliente direto para a avaliação da empresa no Google.** O cliente aproxima o celular do cartão e a página de avaliação abre na hora, sem app e sem digitar nada.

🌐 **No ar:** [aprovacard.com](https://aprovacard.com/)

> 🔒 O código-fonte é privado, porque é um produto comercial em produção. Este repositório mostra o que o sistema faz e como ele foi construído.

![Página inicial do Aprovacard](assets/home-desktop.png)

## O que o sistema faz

- **Redirecionamento NFC → Google:** cada cartão tem um link próprio que leva à página de avaliação da empresa, com registro de cada toque.
- **Busca da empresa no checkout:** o cliente encontra o próprio negócio pelo Google Maps/Places, e o cartão já sai configurado.
- **Pagamento com Pix e cartão de crédito** via Asaas, com confirmação automática por webhook.
- **Assinatura opcional** (Relatório Mensal de Evolução), com cancelamento feito pelo próprio cliente.
- **Área do cliente:** pedidos, configurações e acompanhamento.
- **Painel administrativo:** relatórios em PDF, pedidos e um CRM interno para acompanhar a carteira de clientes.
- **Evolução das notas no Google:** sincronização periódica da avaliação de cada empresa.
- **LGPD:** analytics (Google Analytics e Microsoft Clarity) só liga com consentimento (Consent Mode v2).
- **PWA:** instalável no celular.

## Telas

| Checkout | Página "O que é NFC" |
| --- | --- |
| ![Checkout](assets/checkout.png) | ![Tecnologia NFC](assets/nfc.png) |

<p align="center"><img src="assets/home-mobile.png" alt="Versão mobile" width="280"></p>

## Arquitetura

```mermaid
flowchart LR
    C[Cliente toca o cartão NFC] --> W[Cloudflare Worker<br/>site + redirecionamento]
    W --> G[Página de avaliação<br/>no Google]
    U[Comprador] --> F[Front-end<br/>React + Vite]
    F --> S[(Supabase<br/>Postgres + Auth)]
    F --> E[Edge Functions<br/>15 funções]
    E --> A[Asaas<br/>Pix e cartão]
    A -- webhook --> E
    E --> P[Google Places API]
    E --> S
```

- **Front-end:** React + TypeScript + Vite, Tailwind CSS e shadcn/ui (Radix), animações com Framer Motion e GSAP
- **Back-end:** Supabase (Postgres, Auth e Row Level Security) com 15 Edge Functions e 48 migrations versionadas
- **Pagamentos:** Asaas (Pix, cartão de crédito e assinatura recorrente)
- **Integrações:** Google Maps JavaScript API e Places
- **Deploy:** Cloudflare Workers
- **Qualidade:** testes com Vitest e Testing Library, mais testes ponta a ponta do fluxo de avaliação

## Stack

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white) ![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB) ![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white) ![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white) ![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=for-the-badge&logo=supabase&logoColor=white) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white) ![Cloudflare Workers](https://img.shields.io/badge/Cloudflare_Workers-F38020?style=for-the-badge&logo=cloudflareworkers&logoColor=white) ![Vitest](https://img.shields.io/badge/Vitest-6E9F18?style=for-the-badge&logo=vitest&logoColor=white)

## Autor

Desenvolvido por **Matheus Ferraz**: [perfil no GitHub](https://github.com/27r6tr592n-prog) · [Instagram](https://www.instagram.com/m.moreira071)
