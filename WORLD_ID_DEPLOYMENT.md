
# 🚀 Guia de Deploy - World ID em Produção

## 📋 Pré-requisitos

- ✅ Integração World ID testada localmente
- ✅ App ID de produção obtido
- ✅ Domínio configurado
- ✅ HTTPS ativado
- ✅ Todos os testes passando

---

## 🌐 Configurar Domínio no Developer Portal

### Passo 1: Acessar Settings

1. Acesse: https://developer.worldcoin.org
2. Vá em **"Settings"** (Configurações)
3. Procure por **"Allowed Domains"** (Domínios Autorizados)

### Passo 2: Adicionar Domínios

Adicione seus domínios:

```
https://seu-dominio.com
https://www.seu-dominio.com
https://app.seu-dominio.com
```

**Não adicione:**
- ❌ http:// (sem HTTPS)
- ❌ localhost (apenas para desenvolvimento)
- ❌ Portas específicas (ex: :3000)

### Passo 3: Salvar

Clique em **"Save"** (Salvar)

Aguarde 5-10 minutos para propagação.

---

## 🔐 Obter App ID de Produção

### Passo 1: Mudar para Produção

1. No Developer Portal, vá em **"Projects"**
2. Selecione seu projeto
3. Clique em **"Settings"**
4. Procure por **"Environment"** (Ambiente)
5. Mude de **"Staging"** para **"Production"**

### Passo 2: Copiar App ID

Você receberá um novo App ID:

```
app_xxxxxxxxxxxxxxxx (produção)
```

**Guarde este ID com segurança!**

---

## 🔧 Configurar Variáveis no Vercel

### Passo 1: Acessar Vercel

1. Acesse: https://vercel.com/dashboard
2. Selecione seu projeto **"fortex-mining"**
3. Vá em **"Settings"** (Configurações)

### Passo 2: Environment Variables

1. Clique em **"Environment Variables"**
2. Adicione as seguintes variáveis:

```
NEXT_PUBLIC_WORLD_APP_ID = app_seu_app_id_producao
NEXT_PUBLIC_WORLD_ACTION_ID = fortex-mining-verification
NEXT_PUBLIC_APP_URL = https://seu-dominio.com
NODE_ENV = production
```

### Passo 3: Salvar

Clique em **"Save"** (Salvar)

---

## 📤 Fazer Deploy

### Opção 1: Deploy Automático (Recomendado)

```bash
# 1. Fazer commit das mudanças
git add .
git commit -m "feat: configurar World ID para produção"

# 2. Push para main
git push origin main

# 3. Vercel fará deploy automaticamente
# Acompanhe em: https://vercel.com/dashboard
```

### Opção 2: Deploy Manual

```bash
# 1. Instalar Vercel CLI
npm install -g vercel

# 2. Login
vercel login

# 3. Deploy
vercel --prod
```

---

## ✅ Verificar Deploy

### Passo 1: Acessar Site

Acesse seu domínio:
```
https://seu-dominio.com
```

### Passo 2: Testar Verificação

1. Clique em **"Verificar com World ID"**
2. Complete a verificação
3. Confirme que funciona

### Passo 3: Verificar Logs

No Vercel:
1. Vá em **"Deployments"**
2. Clique no deployment mais recente
3. Vá em **"Logs"**
4. Procure por erros

---

## 🔍 Troubleshooting de Deploy

### Erro: "App ID inválido"

```bash
# Verificar variáveis no Vercel
# Settings > Environment Variables

# Confirmar que NEXT_PUBLIC_WORLD_APP_ID está correto
# Deve começar com "app_" (não "app_staging_")

# Fazer redeploy:
# Deployments > Redeploy
```

### Erro: "CORS - Cross-Origin"

```bash
# Adicionar domínio no Developer Portal
# https://developer.worldcoin.org/settings

# Allowed Domains:
# https://seu-dominio.com

# Aguardar 5-10 minutos
# Fazer redeploy
```

### Erro: "SDK não carregou"

```bash
# Limpar cache do Vercel
# Settings > Git > Clear Cache

# Fazer redeploy
# Deployments > Redeploy
```

### Erro: "Verificação falhou"

```bash
# Verificar logs do Vercel
# Deployments > [seu-deployment] > Logs

# Procurar por mensagens de erro
# Confirmar que backend está respondendo

# Testar API:
curl https://seu-dominio.com/api/worldcoin/status
```

---

## 📊 Monitorar em Produção

### Dashboard do World ID

Acesse: https://developer.worldcoin.org/dashboard

Você verá:
- Total de verificações
- Taxa de sucesso
- Distribuição Orb vs Device
- Usuários únicos verificados

### Logs do Vercel

1. Acesse: https://vercel.com/dashboard
2. Selecione seu projeto
3. Vá em **"Logs"**
4. Procure por erros ou avisos

### Monitoramento de Performance

1. Vá em **"Analytics"** no Vercel
2. Verifique:
   - Tempo de resposta
   - Taxa de erro
   - Requisições por segundo

---

## 🔒 Segurança em Produção

### Checklist de Segurança

- [ ] HTTPS ativado
- [ ] App ID de produção configurado
- [ ] Domínios autorizados no Developer Portal
- [ ] Variáveis de ambiente seguras
- [ ] `.env.local` não commitado
- [ ] Rate limiting implementado
- [ ] Validação no backend ativa
- [ ] Logs de segurança configurados

### Boas Práticas

1. **Nunca compartilhe credenciais**
   ```bash
   # ❌ Errado
   git push com .env.local
   
   # ✅ Correto
   .env.local no .gitignore
   ```

2. **Usar HTTPS sempre**
   ```
   ❌ http://seu-dominio.com
   ✅ https://seu-dominio.com
   ```

3. **Validar no backend**
   ```tsx
   // Sempre verificar prova no servidor
   // Nunca confiar apenas no frontend
   ```

4. **Limpar dados sensíveis**
   ```tsx
   // Não armazenar dados pessoais
   // Usar apenas nullifier_hash
   ```

---

## 📈 Escalabilidade

### Se tiver muitos usuários

1. **Implementar cache**
   ```tsx
   // Cache de verificações
   // TTL: 24 horas
   ```

2. **Rate limiting**
   ```tsx
   // Máximo 10 requisições por minuto
   // Máximo 1 verificação por usuário
   ```

3. **Database (opcional)**
   ```tsx
   // Armazenar verificações em banco de dados
   // Melhor performance e segurança
   ```

4. **CDN**
   ```tsx
   // Usar CDN para assets estáticos
   // Melhor performance global
   ```

---

## 🎉 Pronto para Produção!

Parabéns! Sua integração World ID está em produção! 🚀

### Próximos Passos

1. **Monitorar métricas**
   - Acompanhar verificações
   - Analisar taxa de sucesso

2. **Coletar feedback**
   - Ouvir usuários
   - Melhorar UX

3. **Otimizar performance**
   - Analisar logs
   - Implementar melhorias

4. **Expandir funcionalidades**
   - Adicionar mais badges
   - Integrar com blockchain
   - Criar marketplace

---

**Dúvidas?** Consulte a documentação oficial ou entre em contato com o suporte do World ID! 📧
