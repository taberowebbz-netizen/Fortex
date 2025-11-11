
# Fortex - Aplicativo de Mineração WLD

![Fortex Logo](https://images.unsplash.com/photo-1621416894569-0f39ed31d247?w=200&h=200&fit=crop)

## 🚀 Visão Geral

Fortex é um aplicativo de mineração de tokens integrado com World ID para verificação de identidade única. Mine tokens FORTEX, complete desafios diários e suba de nível enquanto garante distribuição justa através da verificação World ID.

## ✨ Funcionalidades

### 🎯 Mineração de Tokens
- Sistema de mineração em tempo real
- Taxa de 10 FORTEX por hora
- Contador de tempo ativo
- Feedback visual animado

### 📊 Painel de Estatísticas
- Total de tokens minerados
- Mineração diária
- Ranking entre mineradores
- Gráfico de progresso dos últimos 7 dias

### 💰 Carteira Digital
- Saldo total de tokens
- Histórico completo de transações
- Sistema de reivindicação de tokens
- Integração World ID

### 👤 Perfil e Gamificação
- Sistema de níveis (7 níveis)
- Conquistas e badges
- Check-in diário com bônus progressivo
- Dias consecutivos de mineração

### 🔐 Verificação World ID
- Autenticação única por pessoa
- Bônus de 50 FORTEX ao verificar
- Prevenção de múltiplas contas
- Segurança criptográfica

## 🛠️ Tecnologias

- **Framework**: Next.js 15.2.4 (App Router)
- **Linguagem**: TypeScript
- **Estilização**: Tailwind CSS v4
- **Componentes**: shadcn/ui
- **Ícones**: Lucide React
- **Gráficos**: Recharts
- **Animações**: Framer Motion
- **Autenticação**: World ID (IDKit)
- **Armazenamento**: LocalStorage

## 📦 Instalação

```bash
# Clone o repositório
git clone https://github.com/seu-usuario/fortex.git

# Entre no diretório
cd fortex

# Instale as dependências
pnpm install

# Execute em desenvolvimento
pnpm dev
```

Abra [http://localhost:3000](http://localhost:3000) no navegador.

## 🚀 Deploy na Internet

**Quer publicar sua aplicação online?**

📖 **[GUIA_DEPLOY_COMPLETO.md](./GUIA_DEPLOY_COMPLETO.md)** - Guia completo explicando:
- O que é deploy
- Como funciona Vercel e Netlify
- Passo a passo detalhado
- Solução de problemas comuns
- Como atualizar depois do deploy

**Guias Rápidos:**
- 📖 [QUICK_START.md](./QUICK_START.md) - Deploy em 1 hora
- 📋 [DEPLOYMENT_CHECKLIST.md](./DEPLOYMENT_CHECKLIST.md) - Checklist completo

## 🔧 Configuração

### Variáveis de Ambiente

Crie um arquivo `.env.local`:

```env
NEXT_PUBLIC_WORLD_ID_APP_ID=app_staging_your_app_id
NEXT_PUBLIC_WORLD_ID_ACTION=fortex-mining-verification
```

### Ícones PWA

Adicione os seguintes ícones na pasta `public/`:
- `icon-192.png` (192x192px)
- `icon-512.png` (512x512px)
- `favicon.ico` (32x32px)

## 🌐 Integração World (WLD)

Para integrar com a plataforma World e tornar o Fortex um Mini App oficial, consulte o guia completo:

📖 **[WORLD_INTEGRATION.md](./WORLD_INTEGRATION.md)**

### Passos Rápidos

1. **Registre-se** no [World Developer Portal](https://developer.worldcoin.org)
2. **Obtenha** seu App ID e Action ID
3. **Configure** as variáveis de ambiente
4. **Teste** no World App
5. **Deploy** em produção (HTTPS obrigatório)
6. **Submeta** para revisão

## 📱 Estrutura do Projeto

```
fortex/
├── src/
│   ├── app/
│   │   ├── page.tsx              # Página principal de mineração
│   │   ├── wallet/page.tsx       # Carteira de tokens
│   │   ├── stats/page.tsx        # Estatísticas e ranking
│   │   ├── profile/page.tsx      # Perfil do usuário
│   │   └── layout.tsx            # Layout global
│   ├── components/
│   │   ├── fortex/               # Componentes do Fortex
│   │   │   ├── MiningButton.tsx
│   │   │   ├── TokenDisplay.tsx
│   │   │   ├── DailyCheckIn.tsx
│   │   │   └── BottomNav.tsx
│   │   ├── world-id/             # Componentes World ID
│   │   │   ├── WorldIDButton.tsx
│   │   │   ├── WorldIDProvider.tsx
│   │   │   └── WorldIDVerificationCard.tsx
│   │   └── ui/                   # Componentes shadcn/ui
│   └── lib/
│       ├── mining-storage.ts     # Gerenciamento de dados
│       ├── world-id.ts           # Integração World ID
│       └── utils.ts              # Utilitários
├── public/
│   ├── manifest.json             # PWA manifest
│   └── icons/                    # Ícones do app
└── GUIA_DEPLOY_COMPLETO.md       # Guia de deploy
```

## 🎮 Como Usar

### Mineração

1. Clique no botão **Play** para iniciar a mineração
2. Acompanhe o tempo e tokens acumulados em tempo real
3. Clique em **Stop** para parar e coletar os tokens

### Check-in Diário

1. Acesse a página principal
2. Clique em **Fazer Check-in**
3. Receba bônus progressivo (aumenta a cada dia consecutivo)
4. Marcos especiais em 7, 30 e 90 dias

### Verificação World ID

1. Vá para **Carteira** ou **Perfil**
2. Clique em **Verificar com World ID**
3. Escaneie o QR code ou use biometria
4. Receba 50 FORTEX de bônus

### Sistema de Níveis

- **Nível 1**: 0 tokens - Minerador Iniciante
- **Nível 2**: 100 tokens - Minerador Aprendiz
- **Nível 3**: 500 tokens - Minerador Experiente
- **Nível 4**: 1.000 tokens - Minerador Veterano
- **Nível 5**: 2.500 tokens - Minerador Elite
- **Nível 6**: 5.000 tokens - Minerador Mestre
- **Nível 7**: 10.000 tokens - Minerador Lendário

## 🏆 Conquistas

- 🎯 **Primeira Mineração**: Complete sua primeira sessão
- 📅 **Semana Completa**: 7 dias consecutivos de check-in
- 📆 **Mês Dedicado**: 30 dias consecutivos de check-in
- 💰 **Colecionador**: Acumule 100 tokens
- 💎 **Milionário**: Acumule 1.000 tokens
- 🏅 **Top 10**: Entre no top 10 do ranking

## 🚀 Deploy

### Vercel (Recomendado)

```bash
# Via CLI
npm install -g vercel
vercel login
vercel --prod

# Ou via GitHub (automático)
# Conecte seu repositório no dashboard da Vercel
```

### Netlify

```bash
# Via CLI
npm install -g netlify-cli
netlify login
netlify deploy --prod
```

### Requisitos de Produção

- ✅ HTTPS habilitado
- ✅ Variáveis de ambiente configuradas
- ✅ Ícones PWA criados
- ✅ World ID App ID configurado

**📖 Guia Completo:** [GUIA_DEPLOY_COMPLETO.md](./GUIA_DEPLOY_COMPLETO.md)

## 🔒 Segurança

- Verificação World ID para identidade única
- Validação criptográfica de provas
- Nullifier hash para prevenir duplicatas
- Armazenamento local seguro

## 📊 Performance

- Lighthouse Score: 95+
- First Contentful Paint: < 1.5s
- Time to Interactive: < 3s
- PWA Ready

## 🤝 Contribuindo

Contribuições são bem-vindas! Por favor:

1. Fork o projeto
2. Crie uma branch (`git checkout -b feature/nova-funcionalidade`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Push para a branch (`git push origin feature/nova-funcionalidade`)
5. Abra um Pull Request

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## 📞 Suporte

- **Discord**: [Comunidade Fortex](#)
- **Email**: suporte@fortex.app
- **Docs**: [Documentação Completa](./WORLD_INTEGRATION.md)

## 🙏 Agradecimentos

- [World](https://worldcoin.org) - Verificação de identidade
- [Next.js](https://nextjs.org) - Framework React
- [shadcn/ui](https://ui.shadcn.com) - Componentes UI
- [Tailwind CSS](https://tailwindcss.com) - Estilização

---

**Desenvolvido com ❤️ pela equipe Fortex**

🌐 [Website](#) | 🐦 [Twitter](#) | 💬 [Discord](#)
