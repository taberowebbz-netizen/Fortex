
# ⚡ Guia Rápido - Deploy Fortex no World App

## 🎯 Objetivo
Colocar o Fortex no ar e disponível no World App em **3 passos**.

---

## Passo 1: Criar Ícones (30 minutos)

### Opção Rápida - Canva (Recomendado)

1. **Acesse**: https://canva.com
2. **Crie**: Design → "App Icon" (1024x1024)
3. **Design**:
   - Fundo: Gradiente azul (#2B7FFF) → roxo (#6366f1)
   - Centro: Texto "FTX" ou símbolo de moeda 🪙
   - Estilo: Moderno, minimalista
4. **Baixe**: PNG, alta qualidade
5. **Redimensione**:
   - 192x192 → `icon-192.png`
   - 512x512 → `icon-512.png`

### Ferramentas Online Gratuitas
- **Redimensionar**: https://www.iloveimg.com/resize-image
- **Favicon**: https://favicon.io/favicon-converter/
- **Screenshot**: Capture a tela principal do app (540x720)

### Colocar no Projeto
```bash
# Copiar para public/
public/
  ├── icon-192.png
  ├── icon-512.png
  ├── favicon.ico
  └── screenshot-1.png

# Deletar placeholder
rm public/icon-placeholder.txt
```

---

## Passo 2: Obter World ID (15 minutos)

1. **Registre-se**: https://developer.worldcoin.org
2. **Crie App**:
   - Nome: Fortex
   - Tipo: Mini App
   - Categoria: Finance
3. **Configure**:
   - Action ID: `fortex-mining`
   - Callback URL: `https://seu-dominio.com` (temporário)
4. **Copie App ID**: `app_staging_xxxxxxxx`

### Configurar Localmente
```bash
# Criar .env.local
echo "NEXT_PUBLIC_WORLD_APP_ID=app_staging_xxxxxxxx" > .env.local
echo "NEXT_PUBLIC_WORLD_ACTION_ID=fortex-mining" >> .env.local
```

---

## Passo 3: Deploy (10 minutos)

### Vercel (Mais Fácil)

```bash
# Instalar Vercel CLI
npm i -g vercel

# Login
vercel login

# Deploy
vercel --prod
```

**Configurar Variáveis:**
1. Vercel Dashboard → Seu Projeto
2. Settings → Environment Variables
3. Adicionar:
   - `NEXT_PUBLIC_WORLD_APP_ID` = `app_staging_xxx`
   - `NEXT_PUBLIC_WORLD_ACTION_ID` = `fortex-mining`

**Pronto!** Seu app está no ar em: `https://fortex.vercel.app`

---

## Passo 4: Submeter ao World App (5 minutos)

1. **Volte ao World Developer Portal**
2. **Atualize App**:
   - URL: `https://fortex.vercel.app`
   - Upload ícone (512x512)
   - Upload screenshot
3. **Submit for Review**
4. **Aguarde aprovação** (1-2 semanas)

---

## ✅ Checklist Final

- [ ] Ícones criados e no `public/`
- [ ] World ID configurado
- [ ] Deploy feito (Vercel)
- [ ] App acessível via HTTPS
- [ ] Testado em dispositivo real
- [ ] Submetido ao World App

---

## 🆘 Problemas Comuns

### "World ID não funciona"
→ Verificar App ID no `.env.local` e Vercel

### "Ícones não aparecem"
→ Confirmar arquivos em `public/` e rebuild

### "PWA não instala"
→ Verificar HTTPS e manifest.json

---

## 📞 Suporte

- **Documentação Completa**: Ver `WORLD_INTEGRATION.md`
- **Checklist Detalhado**: Ver `DEPLOYMENT_CHECKLIST.md`
- **Criar Ícones**: Ver `ICONS_GUIDE.md`

---

**Tempo Total Estimado**: ~1 hora
**Dificuldade**: Fácil
**Custo**: Grátis (Vercel free tier)
