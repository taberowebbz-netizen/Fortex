
# 🌍 Guia Completo de Configuração World ID (Worldcoin)

## 📋 Índice
1. [Pré-requisitos](#pré-requisitos)
2. [Criar Conta no Developer Portal](#criar-conta-no-developer-portal)
3. [Configurar Variáveis de Ambiente](#configurar-variáveis-de-ambiente)
4. [Instalar Dependências](#instalar-dependências)
5. [Testar Integração](#testar-integração)
6. [Deploy em Produção](#deploy-em-produção)
7. [Troubleshooting](#troubleshooting)

---

## 🔧 Pré-requisitos

Antes de começar, você precisa ter:

- ✅ Node.js 18.17.0 ou superior
- ✅ npm 9.0.0 ou superior
- ✅ Conta Google ou Apple (para criar conta no World ID)
- ✅ Projeto Next.js já configurado (Fortex Mining)

**Verificar versões instaladas:**

```bash
node --version
npm --version
```

---

## 🌐 Criar Conta no Developer Portal

### Passo 1: Acessar o Portal

1. Acesse: **https://developer.worldcoin.org**
2. Clique em **"Sign Up"** (Criar Conta)
3. Escolha entre:
   - Google
   - Apple
   - Email

### Passo 2: Criar Novo Projeto

1. Após fazer login, vá em **"Projects"** (Projetos)
2. Clique em **"Create Project"** (Criar Projeto)
3. Preencha os dados:
   - **Project Name**: `Fortex Mining`
   - **Description**: `Plataforma de mineração de tokens com verificação World ID`
   - **Website**: `https://fortex.vercel.app` (ou seu domínio)

### Passo 3: Obter App ID

1. Após criar o projeto, você verá a página de configuração
2. Procure por **"App ID"** (algo como: `app_staging_xxxxxxxxxxxxxxxx`)
3. **Copie e guarde este ID** - você precisará dele!

### Passo 4: Criar Action

1. No painel do projeto, vá em **"Actions"**
2. Clique em **"Create Action"** (Criar Ação)
3. Configure:
   - **Action Name**: `fortex-mining-verification`
   - **Description**: `Verificação de identidade para mineração Fortex`
   - **Max Verifications**: `1` (uma vez por usuário)
   - **Verification Level**: Selecione ambas (Orb e Device)

4. Clique em **"Create"** (Criar)

---

## 🔐 Configurar Variáveis de Ambiente

### Passo 1: Criar Arquivo .env.local

Na raiz do seu projeto, crie um arquivo chamado `.env.local`:

```bash
# No terminal, na raiz do projeto
touch .env.local
```

### Passo 2: Adicionar Variáveis

Abra o arquivo `.env.local` e adicione:

```env
# ========================================
# WORLD ID CONFIGURATION (OBRIGATÓRIO)
# ========================================

# Para DESENVOLVIMENTO/STAGING:
NEXT_PUBLIC_WORLD_APP_ID=app_staging_xxxxxxxxxxxxxxxx

# Substitua "xxxxxxxxxxxxxxxx" pelo seu App ID real!
# Exemplo real:
# NEXT_PUBLIC_WORLD_APP_ID=app_staging_a1b2c3d4e5f6g7h8

# Action ID (não alterar)
NEXT_PUBLIC_WORLD_ACTION_ID=fortex-mining-verification

# ========================================
# CONFIGURAÇÕES ADICIONAIS
# ========================================

# URL do seu app (necessário para World ID)
NEXT_PUBLIC_APP_URL=http://localhost:3000

# Para produção:
# NEXT_PUBLIC_APP_URL=https://fortex.vercel.app

# Ambiente
NODE_ENV=development
```

### Passo 3: Verificar Arquivo

Confirme que o arquivo foi criado corretamente:

```bash
cat .env.local
```

Você deve ver algo como:
```
NEXT_PUBLIC_WORLD_APP_ID=app_staging_a1b2c3d4e5f6g7h8
NEXT_PUBLIC_WORLD_ACTION_ID=fortex-mining-verification
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

---

## 📦 Instalar Dependências

### Passo 1: Verificar package.json

O projeto já tem as dependências necessárias. Verifique se estão presentes:

```bash
npm list | grep -E "next|react|lucide"
```

### Passo 2: Instalar/Atualizar

Se precisar instalar ou atualizar:

```bash
# Instalar todas as dependências
npm install

# Ou atualizar se necessário
npm update
```

### Passo 3: Verificar Instalação

```bash
npm list next
```

Deve mostrar:
```
fortex-mining@1.0.0
└── next@15.2.4
```

---

## 🧪 Testar Integração

### Passo 1: Iniciar Servidor de Desenvolvimento

```bash
npm run dev
```

Você deve ver:
```
> next dev --turbopack

  ▲ Next.js 15.2.4
  - Local:        http://localhost:3000
  - Environments: .env.local

✓ Ready in 2.5s
```

### Passo 2: Acessar a Aplicação

Abra seu navegador e acesse:
```
http://localhost:3000
```

### Passo 3: Testar Verificação World ID

1. Na página inicial, você verá o card **"Verificação World ID"**
2. Clique no botão **"Verificar com World ID"**
3. Você será redirecionado para o World ID Simulator (em staging)

### Passo 4: Usar o Simulator

Para testar em ambiente de staging:

1. Acesse: **https://simulator.worldcoin.org**
2. Faça login com sua conta World ID
3. Siga as instruções para simular uma verificação
4. Você será redirecionado de volta para o app

### Passo 5: Verificar Sucesso

Após a verificação bem-sucedida:
- ✅ Você verá uma mensagem de sucesso
- ✅ O card mostrará "Verificado com World ID"
- ✅ Seus tokens serão atualizados
- ✅ Uma conquista será desbloqueada

---

## 🚀 Deploy em Produção

### Passo 1: Preparar para Produção

Quando estiver pronto para produção:

1. Acesse o **Developer Portal** novamente
2. Vá em **"Settings"** (Configurações)
3. Mude de **"Staging"** para **"Production"**
4. Você receberá um novo **App ID de produção**

### Passo 2: Atualizar Variáveis de Ambiente

No seu host (Vercel, etc), adicione:

```env
NEXT_PUBLIC_WORLD_APP_ID=app_xxxxxxxxxxxxxxxx
NEXT_PUBLIC_WORLD_ACTION_ID=fortex-mining-verification
NEXT_PUBLIC_APP_URL=https://fortex.vercel.app
NODE_ENV=production
```

### Passo 3: Deploy

```bash
# Fazer commit das mudanças
git add .
git commit -m "feat: configurar World ID para produção"

# Push para o repositório
git push origin main

# Vercel fará deploy automaticamente
```

### Passo 4: Verificar Deploy

1. Acesse sua URL de produção
2. Teste a verificação World ID
3. Confirme que tudo funciona

---

## 🐛 Troubleshooting

### Erro: "App ID inválido"

**Causa**: O App ID no `.env.local` está incorreto ou não existe.

**Solução**:
```bash
# 1. Verificar arquivo .env.local
cat .env.local

# 2. Confirmar App ID no Developer Portal
# https://developer.worldcoin.org/projects

# 3. Copiar App ID correto e atualizar .env.local

# 4. Reiniciar servidor
npm run dev
```

### Erro: "World ID SDK não carregou"

**Causa**: Script do World ID não foi carregado corretamente.

**Solução**:
```bash
# 1. Limpar cache
rm -rf .next
rm -rf node_modules/.cache

# 2. Reiniciar servidor
npm run dev

# 3. Limpar cache do navegador (Ctrl+Shift+Delete)

# 4. Tentar novamente
```

### Erro: "Verificação falhou"

**Causa**: Problema na comunicação com servidores do World ID.

**Solução**:
```bash
# 1. Verificar se está em staging ou produção
echo $NEXT_PUBLIC_WORLD_APP_ID

# 2. Confirmar que a action existe no Developer Portal

# 3. Verificar console do navegador (F12)
# Procure por mensagens de erro

# 4. Tentar novamente em alguns minutos
```

### Erro: "CORS - Cross-Origin"

**Causa**: Domínio não autorizado no World ID.

**Solução**:
```bash
# 1. Ir para Developer Portal
# https://developer.worldcoin.org/settings

# 2. Em "Allowed Domains", adicionar:
# - http://localhost:3000 (desenvolvimento)
# - https://fortex.vercel.app (produção)

# 3. Salvar e aguardar 5 minutos

# 4. Tentar novamente
```

### Erro: "Nullifier Hash duplicado"

**Causa**: Usuário já foi verificado anteriormente.

**Solução**:
```bash
# 1. Limpar dados locais
# Abrir DevTools (F12)
# Console > localStorage.clear()

# 2. Recarregar página
# Ctrl+Shift+R (hard refresh)

# 3. Tentar verificação novamente
```

---

## 📊 Monitorar Verificações

### Dashboard do Developer Portal

1. Acesse: **https://developer.worldcoin.org/dashboard**
2. Você verá:
   - Total de verificações
   - Taxa de sucesso
   - Distribuição Orb vs Device
   - Usuários únicos verificados

### Logs Locais

Para ver logs de verificação no seu app:

```bash
# Abrir DevTools (F12)
# Ir para Console
# Você verá mensagens como:

# ✅ World ID verification successful
# ❌ World ID verification failed
# ⚠️ World ID error: ...
```

---

## 🔒 Segurança

### Boas Práticas

1. **Nunca compartilhe seu App ID privado**
   - Apenas `NEXT_PUBLIC_WORLD_APP_ID` é público
   - Outros IDs devem ser mantidos em segredo

2. **Validar sempre no backend**
   - Nunca confie apenas na verificação do frontend
   - Sempre verificar a prova no servidor

3. **Usar HTTPS em produção**
   - World ID requer HTTPS
   - HTTP só funciona em localhost

4. **Limpar dados sensíveis**
   - Não armazene dados pessoais
   - Use apenas o `nullifier_hash` como ID único

---

## 📚 Recursos Adicionais

- 📖 **Documentação Oficial**: https://docs.worldcoin.org
- 💬 **Discord Community**: https://discord.gg/worldcoin
- 🐦 **Twitter**: https://twitter.com/worldcoin
- 📧 **Suporte**: developers@worldcoin.org
- 🔗 **Developer Portal**: https://developer.worldcoin.org

---

## ✅ Checklist Final

Antes de considerar a integração completa:

- [ ] Conta criada no Developer Portal
- [ ] App ID obtido e guardado
- [ ] Action criada e ativa
- [ ] `.env.local` configurado corretamente
- [ ] Servidor de desenvolvimento rodando
- [ ] Verificação testada com sucesso
- [ ] Tokens atualizados após verificação
- [ ] Conquista desbloqueada
- [ ] Dados salvos no localStorage
- [ ] Sem erros no console do navegador

---

## 🎉 Próximos Passos

Após completar a configuração:

1. **Customizar Recompensas**
   - Editar `src/lib/mining-storage.ts`
   - Ajustar `TOKENS_PER_CYCLE` e `MINING_CYCLE_DURATION`

2. **Adicionar Mais Badges**
   - Editar array `BADGES` em `mining-storage.ts`
   - Criar lógica de desbloqueio

3. **Integrar com Blockchain** (opcional)
   - Usar Wagmi para conectar carteira
   - Fazer transações on-chain

4. **Deploy em Produção**
   - Seguir guia de deploy
   - Configurar variáveis de produção
   - Testar completamente

---

**Dúvidas?** Consulte a documentação oficial ou entre em contato com o suporte do World ID! 🚀
