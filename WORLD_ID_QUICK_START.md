
# ⚡ Quick Start - World ID em 5 Minutos

## 1️⃣ Criar Conta (2 minutos)

```bash
# Acesse
https://developer.worldcoin.org

# Clique em "Sign Up"
# Use Google, Apple ou Email
# Confirme seu email
```

## 2️⃣ Obter App ID (1 minuto)

```bash
# No Developer Portal:
# 1. Vá em "Projects"
# 2. Clique "Create Project"
# 3. Nome: "Fortex Mining"
# 4. Copie o App ID (app_staging_...)
```

## 3️⃣ Configurar Variáveis (1 minuto)

```bash
# Crie arquivo .env.local na raiz do projeto
cat > .env.local << EOF
NEXT_PUBLIC_WORLD_APP_ID=app_staging_seu_app_id_aqui
NEXT_PUBLIC_WORLD_ACTION_ID=fortex-mining-verification
NEXT_PUBLIC_APP_URL=http://localhost:3000
NODE_ENV=development
EOF
```

## 4️⃣ Iniciar Servidor (1 minuto)

```bash
npm run dev
```

## 5️⃣ Testar

```bash
# Abra http://localhost:3000
# Clique em "Verificar com World ID"
# Siga as instruções
# ✅ Pronto!
```

---

## 🔑 Variáveis Necessárias

| Variável | Valor | Obrigatório |
|----------|-------|------------|
| `NEXT_PUBLIC_WORLD_APP_ID` | `app_staging_...` | ✅ Sim |
| `NEXT_PUBLIC_WORLD_ACTION_ID` | `fortex-mining-verification` | ✅ Sim |
| `NEXT_PUBLIC_APP_URL` | `http://localhost:3000` | ✅ Sim |
| `NODE_ENV` | `development` | ✅ Sim |

---

## 📱 Testar Verificação

1. Clique no botão "Verificar com World ID"
2. Você será redirecionado para o World ID
3. Siga as instruções na tela
4. Retorne ao app automaticamente
5. Veja a mensagem de sucesso

---

## 🚀 Deploy (Vercel)

```bash
# 1. Adicione variáveis no Vercel
# https://vercel.com/[seu-usuario]/[seu-projeto]/settings/environment-variables

# 2. Adicione:
NEXT_PUBLIC_WORLD_APP_ID=app_staging_seu_app_id
NEXT_PUBLIC_WORLD_ACTION_ID=fortex-mining-verification
NEXT_PUBLIC_APP_URL=https://seu-dominio.vercel.app

# 3. Faça push
git push origin main

# 4. Vercel fará deploy automaticamente
```

---

## ❓ Problemas?

| Problema | Solução |
|----------|---------|
| "App ID inválido" | Copie o App ID correto do Developer Portal |
| "SDK não carregou" | Limpe cache: `rm -rf .next && npm run dev` |
| "Verificação falhou" | Tente novamente em alguns minutos |
| "CORS error" | Adicione seu domínio em Settings do Developer Portal |

---

**Pronto!** Sua integração World ID está funcionando! 🎉
