# Signalist

Plataforma web para acompanhar o mercado financeiro, organizar uma watchlist e receber resumos personalizados de notícias com inteligência artificial.

O Signalist reúne dados de ações e criptomoedas em um dashboard responsivo, permite que cada usuário acompanhe seus ativos favoritos e usa IA para transformar notícias de mercado em resumos mais relevantes ao seu perfil.

## Funcionalidades

- Dashboard com visão geral de ações, criptomoedas e notícias do mercado
- Busca de ativos e consulta de cotações pela Finnhub
- Watchlist individual para usuários autenticados
- Cadastro e login com e-mail e senha
- Autenticação social com GitHub
- Onboarding com perfil de investimento, objetivos e tolerância a risco
- E-mail de boas-vindas personalizado com Gemini
- Resumo diário de notícias baseado nos ativos acompanhados
- Processamento assíncrono e tarefas agendadas com Inngest
- Persistência de usuários e watchlists no MongoDB
- Tratamento de limites e falhas da API de mercado

## Tecnologias

### Front-end

- Next.js 16
- React 19
- TypeScript
- Tailwind CSS 4
- Radix UI
- React Hook Form
- Lucide React
- next-themes

### Back-end e integrações

- Server Actions e Route Handlers do Next.js
- Better Auth
- MongoDB e Mongoose
- Finnhub API
- Google Gemini
- Inngest
- Nodemailer

## Como funciona

1. O usuário cria uma conta ou entra com o GitHub.
2. Durante o onboarding, informa objetivos, interesses e tolerância a risco.
3. O Signalist usa esses dados para gerar uma apresentação personalizada com Gemini.
4. O usuário pesquisa ativos e adiciona ações ou criptomoedas à watchlist.
5. O dashboard consulta cotações e notícias pela Finnhub.
6. Uma função agendada pelo Inngest reúne as notícias relacionadas à watchlist.
7. O Gemini gera um resumo e o Nodemailer envia o conteúdo por e-mail.

## Executando localmente

### Pré-requisitos

- Node.js 20 ou superior
- npm
- Uma instância do MongoDB
- Credenciais para Finnhub, Gemini, GitHub OAuth, Inngest e uma conta Gmail com senha de app

### Instalação

```bash
git clone https://github.com/hayax0/Stocks_App.git
cd Stocks_App
npm install
```

Crie um arquivo `.env.local` na raiz do projeto:

```env
MONGODB_URI=
BETTER_AUTH_SECRET=
BETTER_AUTH_BASE_URL=http://localhost:3000

GITHUB_CLIENT_ID=
GITHUB_CLIENT_SECRET=

NEXT_PUBLIC_FINNHUB_API_KEY=
GEMINI_API_KEY=

INNGEST_EVENT_KEY=
INNGEST_SIGNING_KEY=

NODEMAILER_EMAIL=
NODEMAILER_PASSWORD=
```

Depois, inicie o ambiente de desenvolvimento:

```bash
npm run dev
```

A aplicação estará disponível em [http://localhost:3000](http://localhost:3000).

> Para o envio com Gmail, use uma senha de app em `NODEMAILER_PASSWORD`; não utilize a senha principal da conta.

## Scripts

```bash
npm run dev
npm run build
npm run start
npm run lint
```

## Estrutura principal

```text
app/
├── (auth)/          # Cadastro, login e onboarding
├── (root)/          # Dashboard e páginas autenticadas
└── api/inngest/     # Endpoint das funções do Inngest

components/          # Componentes de interface
database/            # Conexão e modelos do MongoDB
lib/
├── actions/         # Dados de mercado e operações da watchlist
├── better-auth/     # Configuração de autenticação
├── inngest/         # Eventos, funções e prompts de IA
└── nodemailer/      # Templates e envio de e-mails
```

## Decisões técnicas

- As chamadas à Finnhub usam cache e tratamento específico para respostas `403` e `429`.
- As consultas da watchlist são feitas de forma controlada para reduzir o risco de exceder o limite da API.
- As rotinas de e-mail ficam fora do fluxo principal da aplicação e são executadas pelo Inngest.
- A autenticação e os dados da watchlist são associados ao usuário armazenado no MongoDB.

## Estado do projeto

O projeto já possui o fluxo principal implementado: autenticação, onboarding, dashboard, consulta de mercado, watchlist e automações de e-mail com IA. Os próximos passos mais importantes são adicionar testes automatizados, ampliar a observabilidade e documentar o processo de deploy.
