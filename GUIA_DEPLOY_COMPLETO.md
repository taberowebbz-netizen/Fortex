
# 🚀 Guia Completo de Deploy - O que é e Como Fazer

## 📖 O que é Deploy?

**Deploy** significa **publicar sua aplicação na internet** para que qualquer pessoa possa acessar.

### Situação Atual
- ✅ Sua aplicação funciona no seu computador (`localhost:3000`)
- ❌ Outras pessoas **não conseguem** acessar
- ❌ Só funciona quando você executa `npm run dev`

### Depois do Deploy
- ✅ Aplicação disponível 24/7 na internet
- ✅ Qualquer pessoa pode acessar via URL
- ✅ Funciona em qualquer dispositivo (celular, tablet, PC)
- ✅ Não precisa do seu computador ligado

---

## 🌐 O que são Vercel e Netlify?

São **plataformas de hospedagem** que guardam sua aplicação na internet **gratuitamente**.

### 🟢 Vercel (RECOMENDADO)

**Por que escolher:**
- Criada pela mesma empresa do Next.js
- Deploy automático em 2 minutos
- Domínio grátis: `seu-app.vercel.app`
- SSL/HTTPS automático (segurança)
- Melhor performance para Next.js

**Plano Grátis:**
- ✅ Deploy ilimitado
- ✅ 100GB de tráfego/mês
- ✅ Suficiente para milhares de usuários
- ✅ Sem cartão de crédito necessário

### 🔵 Netlify (Alternativa)

**Características:**
- Também oferece plano grátis
- Domínio: `seu-app.netlify.app`
- Boa para sites estáticos
- Interface amigável

---

## 🎯 Método 1: Deploy via Vercel (MAIS FÁCIL)

### Passo 1: Criar Conta no GitHub (5 minutos)

**O que é GitHub?**
- Plataforma para guardar código online
- Como um "Google Drive" para programadores
- Necessário para deploy automático

**Como fazer:**

1. Acesse: https://github.com
2. Clique em **"Sign up"** (Criar conta)
3. Preencha:
   - Email
   - Senha
   - Nome de usuário
4. Confirme seu email

### Passo 2: Subir Código para GitHub (10 minutos)

Abra o terminal na pasta do seu projeto e execute:

```bash
# 1. Inicializar Git (se ainda não fez)
git init

# 2. Adicionar todos os arquivos
git add .

# 3. Fazer primeiro commit (salvar versão)
git commit -m "Deploy inicial do Fortex"

# 4. Criar repositório no GitHub
# Vá em: https://github.com/new
# - Nome: fortex-mining
# - Deixe PÚBLICO
# - NÃO marque "Initialize with README"
# - Clique em "Create repository"

# 5. Conectar com GitHub (SUBSTITUA seu-usuario pelo seu username)
git remote add origin https://github.com/seu-usuario/fortex-mining.git

# 6. Enviar código
git branch -M main
git push -u origin main
```

**Possíveis erros:**

❌ **"git: command not found"**
→ Instale o Git: https://git-scm.com/downloads

❌ **"Permission denied"**
→ Configure suas credenciais do GitHub

### Passo 3: Deploy na Vercel (5 minutos)

**Opção A: Via Interface Web (Mais Fácil)**

1. Acesse: https://vercel.com
2. Clique em **"Sign up"**
3. Escolha **"Continue with GitHub"**
4. Autorize a Vercel a acessar seus repositórios
5. Clique em **"Import Project"**
6. Selecione o repositório **"fortex-mining"**
7. Configurações (deixe padrão):
   - Framework: **Next.js** ✅ (detecta automaticamente)
   - Root Directory: `./`
   - Build Command: `npm run build`
   - Output Directory: `.next`

8. **Adicionar Variáveis de Ambiente:**
   - Clique em **"Environment Variables"**
   - Adicione (se tiver World ID configurado):
     ```
     NEXT_PUBLIC_WORLD_APP_ID = app_staging_seu_id_aqui
     NEXT_PUBLIC_WORLD_ACTION_ID = fortex-mining
     ```

9. Clique em **"Deploy"** 🚀

**Opção B: Via Terminal (Avançado)**

```bash
# 1. Instalar Vercel CLI
npm install -g vercel

# 2. Login
vercel login
# Abrirá navegador para autenticar

# 3. Deploy
vercel

# 4. Responder perguntas:
# - Set up and deploy? Y
# - Which scope? (escolha sua conta)
# - Link to existing project? N
# - What's your project's name? fortex-mining
# - In which directory is your code located? ./
# - Want to override settings? N

# 5. Deploy em produção
vercel --prod
```

### Passo 4: Acessar Sua Aplicação (1 minuto)

Após o deploy, a Vercel mostrará:

```
✅ Production: https://fortex-mining.vercel.app
```

**Pronto!** Sua aplicação está online! 🎉

Teste:
- Abra a URL no navegador
- Teste no celular
- Compartilhe com amigos

---

## 🎯 Método 2: Deploy via Netlify

### Via Interface Web

1. Acesse: https://netlify.com
2. Clique em **"Sign up"** → **"GitHub"**
3. Autorize o Netlify
4. Clique em **"Add new site"** → **"Import an existing project"**
5. Selecione **GitHub** → Autorize
6. Escolha repositório **"fortex-mining"**
7. Configure:
   - Build command: `npm run build`
   - Publish directory: `.next`
8. Adicione variáveis de ambiente (se necessário)
9. Clique em **"Deploy site"**

### Via Terminal

```bash
# 1. Instalar Netlify CLI
npm install -g netlify-cli

# 2. Login
netlify login

# 3. Deploy
netlify deploy

# 4. Produção
netlify deploy --prod
```

---

## ✅ Checklist Pré-Deploy

Antes de fazer deploy, verifique:

- [ ] Código funciona localmente (`npm run dev`)
- [ ] Não há erros no console do navegador
- [ ] Arquivo `.gitignore` está configurado
- [ ] Imagens estão na pasta `public/`
- [ ] `package.json` tem todas dependências
- [ ] Testou build de produção (`npm run build`)

---

## 🔄 Como Atualizar Depois do Deploy

### Deploy Automático (Vercel + GitHub)

```bash
# 1. Fazer mudanças no código
# 2. Salvar e commitar
git add .
git commit -m "Adiciona nova funcionalidade"

# 3. Enviar para GitHub
git push

# 4. Vercel detecta e faz deploy automático! 🎉
# Aguarde 2-3 minutos
```

### Deploy Manual

```bash
# Vercel
vercel --prod

# Netlify
netlify deploy --prod
```

---

## 🐛 Problemas Comuns e Soluções

### ❌ Erro: "Module not found"

**Causa:** Dependência faltando

**Solução:**
```bash
rm -rf node_modules package-lock.json
npm install
git add .
git commit -m "Fix dependencies"
git push
```

### ❌ Erro: "Build failed"

**Causa:** Erro de compilação

**Solução:**
1. Veja os logs no dashboard da Vercel
2. Teste localmente: `npm run build`
3. Corrija os erros mostrados
4. Faça commit e push novamente

### ❌ Erro: "Page not found"

**Causa:** Rota incorreta

**Solução:**
- Verifique se arquivos estão em `src/app/`
- Confirme nomenclatura: `page.tsx`, `layout.tsx`

### ❌ Erro: "Environment variable not found"

**Causa:** Variável de ambiente não configurada

**Solução:**
1. Vercel Dashboard → Seu Projeto
2. Settings → Environment Variables
3. Adicione as variáveis necessárias
4. Redeploy: Settings → Deployments → Redeploy

---

## 🔧 Configurar Domínio Personalizado (Opcional)

### Domínios Grátis

Por padrão você recebe:
- Vercel: `fortex-mining.vercel.app`
- Netlify: `fortex-mining.netlify.app`

### Domínio Próprio (Pago)

**Comprar domínio:**
- Namecheap: ~$10/ano
- GoDaddy: ~$12/ano
- Registro.br: ~R$40/ano

**Configurar na Vercel:**
1. Vercel Dashboard → Settings → Domains
2. Clique em **"Add Domain"**
3. Digite seu domínio: `fortexmining.com`
4. Siga instruções para configurar DNS
5. Aguarde propagação (até 48h)

---

## 📊 Monitorar Sua Aplicação

### Vercel Dashboard

Acesse: https://vercel.com/dashboard

**Métricas disponíveis:**
- 📈 **Analytics**: Quantas visitas
- 🐛 **Logs**: Erros em tempo real
- ⚡ **Performance**: Velocidade da app
- 🌍 **Deployments**: Histórico de deploys

### Alertas

Configure notificações:
- Email quando deploy falha
- Slack/Discord integração
- Alertas de downtime

---

## 💰 Custos

### Plano Grátis Vercel

**Incluído:**
- ✅ Deploy ilimitado
- ✅ 100GB bandwidth/mês
- ✅ Domínio `.vercel.app` grátis
- ✅ SSL automático (HTTPS)
- ✅ Suficiente para ~10.000 usuários/mês

**Quando precisa pagar?**
- Tráfego > 100GB/mês
- Mais de 3 membros na equipe
- Funcionalidades enterprise

**Plano Pro:** $20/mês
- 1TB bandwidth
- Analytics avançado
- Suporte prioritário

---

## 🎯 Próximos Passos Após Deploy

1. ✅ **Testar aplicação online**
   - Abra em diferentes navegadores
   - Teste no celular
   - Verifique todas funcionalidades

2. ✅ **Compartilhar URL**
   - Envie para amigos testarem
   - Poste nas redes sociais
   - Adicione ao portfólio

3. ✅ **Configurar World ID** (se ainda não fez)
   - Registre no World Developer Portal
   - Atualize variáveis de ambiente
   - Redeploy

4. ✅ **Submeter ao World App**
   - Siga guia em `WORLD_INTEGRATION.md`
   - Aguarde aprovação
   - Publique na World App Store

5. ✅ **Monitorar e Melhorar**
   - Acompanhe analytics
   - Corrija bugs reportados
   - Adicione novas funcionalidades

---

## 📞 Suporte e Recursos

### Documentação Oficial

- **Vercel**: https://vercel.com/docs
- **Netlify**: https://docs.netlify.com
- **Next.js**: https://nextjs.org/docs
- **GitHub**: https://docs.github.com

### Comunidades

- **Discord Vercel**: https://vercel.com/discord
- **Stack Overflow**: Tag `vercel` ou `netlify`
- **Reddit**: r/nextjs, r/webdev

### Tutoriais em Vídeo

- YouTube: "Deploy Next.js Vercel"
- YouTube: "GitHub para iniciantes"

---

## 🎉 Resumo Rápido

**3 Passos para Deploy:**

1. **GitHub** → Guarda seu código online
2. **Vercel** → Transforma código em site funcionando
3. **Compartilhar** → URL pública para todos acessarem

**Tempo Total:** ~20 minutos
**Custo:** R$ 0,00 (grátis)
**Dificuldade:** Fácil

---

## 🚀 Comando Único (Para Quem Tem Pressa)

Se você já tem Git e Vercel CLI instalados:

```bash
# Deploy completo em 1 comando
git init && \
git add . && \
git commit -m "Initial deploy" && \
vercel --prod
```

---

**Desenvolvido com ❤️ para facilitar seu deploy!**

Dúvidas? Consulte os outros guias:
- `QUICK_START.md` - Guia rápido
- `DEPLOYMENT_CHECKLIST.md` - Checklist detalhado
- `WORLD_INTEGRATION.md` - Integração World ID

