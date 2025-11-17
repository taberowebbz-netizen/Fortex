
# 🚀 Checklist de Deploy - Fortex para World App

## Pré-Deploy

### 1. Criar Ícones PWA
- [ ] Criar `icon-192.png` (192x192px)
- [ ] Criar `icon-512.png` (512x512px)
- [ ] Criar `favicon.ico` (32x32px)
- [ ] Criar `screenshot-1.png` (540x720px)
- [ ] Colocar todos em `public/`
- [ ] Deletar `public/icon-placeholder.txt`

### 2. Obter Credenciais World ID
- [ ] Criar conta em https://developer.worldcoin.org
- [ ] Registrar aplicativo "Fortex"
- [ ] Copiar App ID (formato: `app_staging_xxx` ou `app_xxx`)
- [ ] Configurar Action ID: `fortex-mining`
- [ ] Adicionar callback URL: `https://seu-dominio.com`

### 3. Configurar Variáveis de Ambiente
- [ ] Criar arquivo `.env.local`
- [ ] Adicionar `NEXT_PUBLIC_WORLD_APP_ID`
- [ ] Adicionar `NEXT_PUBLIC_WORLD_ACTION_ID`
- [ ] Adicionar `NEXT_PUBLIC_APP_URL`
- [ ] (Opcional) Configurar VAPID keys para push notifications

### 4. Testar Localmente
```bash
# Build de produção
npm run build

# Testar build
npm start

# Verificar em http://localhost:3000
```

- [ ] App carrega sem erros
- [ ] World ID funciona
- [ ] Mineração funciona
- [ ] PWA instala corretamente
- [ ] Service Worker registra
- [ ] Ícones aparecem corretamente

### 5. Lighthouse Audit
- [ ] Abrir DevTools (F12)
- [ ] Lighthouse → Progressive Web App
- [ ] Score > 90
- [ ] Corrigir problemas encontrados

---

## Deploy em Produção

### Opção 1: Vercel (Recomendado)

```bash
# Instalar Vercel CLI
npm i -g vercel

# Login
vercel login

# Deploy
vercel --prod
```

**Configurar no Vercel Dashboard:**
1. Acesse https://vercel.com/dashboard
2. Selecione o projeto
3. Settings → Environment Variables
4. Adicionar:
   - `NEXT_PUBLIC_WORLD_APP_ID`
   - `NEXT_PUBLIC_WORLD_ACTION_ID`
   - `NEXT_PUBLIC_APP_URL`

### Opção 2: Netlify

```bash
# Instalar Netlify CLI
npm i -g netlify-cli

# Login
netlify login

# Deploy
netlify deploy --prod
```

**Configurar no Netlify:**
1. Site settings → Environment variables
2. Adicionar as mesmas variáveis

### Opção 3: Servidor Próprio

**Requisitos:**
- Node.js 18+
- HTTPS configurado (obrigatório)
- PM2 ou similar para gerenciamento

```bash
# Build
npm run build

# Iniciar com PM2
pm2 start npm --name "fortex" -- start

# Configurar NGINX reverse proxy
# Certificado SSL (Let's Encrypt)
```

---

## Pós-Deploy

### 1. Verificar Produção
- [ ] App acessível via HTTPS
- [ ] Ícones carregam corretamente
- [ ] World ID funciona em produção
- [ ] PWA instala em dispositivos reais
- [ ] Service Worker ativo
- [ ] Notificações funcionam (se configurado)

### 2. Testar em Dispositivos Reais

**Android:**
- [ ] Chrome → Menu → "Instalar app"
- [ ] Verificar ícone na home screen
- [ ] Testar modo offline
- [ ] Verificar World ID

**iOS:**
- [ ] Safari → Share → "Adicionar à Tela Inicial"
- [ ] Verificar ícone
- [ ] Testar funcionalidades

**Desktop:**
- [ ] Chrome → Ícone de instalação na barra
- [ ] Instalar e testar

### 3. Configurar Analytics (Opcional)
- [ ] Google Analytics 4
- [ ] Vercel Analytics
- [ ] Sentry (error tracking)

---

## Submissão ao World App

### 1. Preparar Informações

**Dados do App:**
- Nome: Fortex - Mineração WLD
- Descrição: Minere tokens Fortex com verificação World ID
- Categoria: Finance, Utilities
- URL: https://seu-dominio.com
- Ícone: icon-512.png
- Screenshots: screenshot-1.png

### 2. Registrar no World Developer Portal

1. Acesse https://developer.worldcoin.org
2. Dashboard → Apps → "Create New App"
3. Preencher informações:
   - **App Name**: Fortex
   - **Description**: Plataforma de mineração de tokens com verificação World ID
   - **Website**: https://seu-dominio.com
   - **Category**: Finance
   - **App Type**: Mini App

4. Configurar Permissões:
   - [x] World ID Verification
   - [ ] User Profile (opcional)
   - [ ] Notifications (opcional)

5. Adicionar URLs:
   - **App URL**: https://seu-dominio.com
   - **Callback URL**: https://seu-dominio.com/auth/callback
   - **Privacy Policy**: https://seu-dominio.com/privacy
   - **Terms of Service**: https://seu-dominio.com/terms

6. Upload de Assets:
   - Ícone (512x512)
   - Screenshots (mínimo 2)
   - Banner (opcional)

### 3. Configurar App ID de Produção

Após aprovação, você receberá um App ID de produção:

```env
# Atualizar .env.local e Vercel
NEXT_PUBLIC_WORLD_APP_ID=app_production_xxxxxxxx
```

**Redeploy:**
```bash
vercel --prod
```

### 4. Submeter para Revisão

1. Developer Portal → Submit for Review
2. Aguardar aprovação (1-2 semanas)
3. Responder a feedback se necessário
4. Após aprovação, app aparece no World App Store

### 5. Monitorar Lançamento

- [ ] Verificar listagem no World App
- [ ] Testar instalação via World App
- [ ] Monitorar analytics
- [ ] Coletar feedback de usuários
- [ ] Responder reviews

---

## Manutenção Pós-Lançamento

### Atualizações
```bash
# Fazer alterações no código
git commit -m "feat: nova funcionalidade"

# Deploy automático (Vercel/Netlify)
git push origin main

# Ou manual
vercel --prod
```

### Monitoramento
- [ ] Verificar logs de erro (Sentry)
- [ ] Analisar métricas (Analytics)
- [ ] Responder feedback de usuários
- [ ] Atualizar documentação

### Checklist Semanal
- [ ] Verificar uptime
- [ ] Revisar analytics
- [ ] Responder reviews
- [ ] Verificar issues no GitHub
- [ ] Atualizar dependências (se necessário)

---

## Troubleshooting

### World ID não funciona em produção
- Verificar App ID correto
- Confirmar HTTPS ativo
- Verificar callback URLs
- Checar console para erros

### PWA não instala
- Verificar manifest.json
- Confirmar service worker registrado
- Testar em janela anônima
- Verificar HTTPS

### Ícones não aparecem
- Verificar caminhos no manifest.json
- Confirmar arquivos em public/
- Limpar cache do navegador
- Rebuild e redeploy

---

## Recursos

- **World ID Docs**: https://docs.worldcoin.org/id
- **Developer Portal**: https://developer.worldcoin.org
- **Vercel Docs**: https://vercel.com/docs
- **PWA Checklist**: https://web.dev/pwa-checklist/
- **Lighthouse**: https://developers.google.com/web/tools/lighthouse

---

## Status Atual

- [x] Código completo
- [x] Integração World ID
- [x] PWA configurado
- [x] Documentação
- [ ] **Ícones criados** ← PRÓXIMO PASSO
- [ ] **World ID de produção** ← APÓS ÍCONES
- [ ] **Deploy em produção** ← APÓS WORLD ID
- [ ] **Submissão ao World App** ← FINAL

---

**Última Atualização**: 2024
**Versão**: 1.0.0
**Status**: Pronto para Deploy (após criar ícones)
