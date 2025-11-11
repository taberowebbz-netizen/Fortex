
# 🌍 Guia Completo de Integração World ID

## 📚 Índice
1. [Visão Geral](#visão-geral)
2. [Arquitetura](#arquitetura)
3. [Fluxo de Verificação](#fluxo-de-verificação)
4. [Implementação](#implementação)
5. [Testes](#testes)
6. [Segurança](#segurança)
7. [Troubleshooting](#troubleshooting)

---

## 🎯 Visão Geral

A integração World ID permite que usuários provem sua humanidade de forma anônima e segura usando:

- **Orb Verification**: Verificação presencial com máquinas Orb (máxima segurança)
- **Device Verification**: Verificação via smartphone (mais acessível)

### Benefícios

✅ Prova de humanidade sem revelar identidade
✅ Prevenção de bots e contas falsas
✅ Distribuição justa de tokens
✅ Segurança criptográfica
✅ Privacidade garantida

---

## 🏗️ Arquitetura

### Componentes

```
┌─────────────────────────────────────────────────────────┐
│                    Frontend (Next.js)                    │
│  ┌──────────────────────────────────────────────────┐   │
│  │  WorldIDVerificationCard.tsx                     │   │
│  │  - UI para verificação                           │   │
│  │  - Integração com IDKit Widget                   │   │
│  └──────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│                  Backend (Next.js API)                   │
│  ┌──────────────────────────────────────────────────┐   │
│  │  /api/worldcoin/verify                          │   │
│  │  - Verifica prova criptográfica                  │   │
│  │  - Comunica com World ID API                     │   │
│  └──────────────────────────────────────────────────┘   │
│  ┌──────────────────────────────────────────────────┐   │
│  │  /api/worldcoin/bonus/claim                     │   │
│  │  - Distribui bônus de verificação                │   │
│  │  - Atualiza perfil do usuário                    │   │
│  └──────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────┘
                          ↓
┌─────────────────────────────────────────────────────────┐
│              World ID Servers (Worldcoin)                │
│  - Verifica prova criptográfica                         │
│  - Retorna resultado de verificação                     │
└─────────────────────────────────────────────────────────┘
```

### Arquivos Criados

```
src/
├── app/
│   ├── next_api/
│   │   └── worldcoin/
│   │       ├── verify/route.ts          # Verificar prova
│   │       ├── callback/route.ts        # Callback pós-verificação
│   │       ├── bonus/
│   │       │   └── claim/route.ts       # Reivindicar bônus
│   │       ├── user/[nullifier]/route.ts # Dados do usuário
│   │       └── status/route.ts          # Status da integração
│   └── page.tsx                         # Página principal
├── components/
│   └── world-id/
│       ├── WorldIDVerificationCard.tsx  # Card de verificação
│       ├── WorldIDButton.tsx            # Botão de verificação
│       └── WorldIDProvider.tsx          # Context provider
├── lib/
│   ├── world-id.ts                      # Utilitários World ID
│   ├── worldcoin-client.ts              # Cliente API
│   └── mining-storage.ts                # Armazenamento local
└── types/
    └── world-id.d.ts                    # Tipos TypeScript
```

---

## 🔄 Fluxo de Verificação

### Passo 1: Usuário Inicia Verificação

```
Usuário clica em "Verificar com World ID"
         ↓
IDKit Widget abre
         ↓
Exibe QR Code ou Deep Link
```

### Passo 2: Verificação no World App

```
Usuário escaneia QR Code com World App
         ↓
Seleciona nível de verificação (Orb ou Device)
         ↓
Completa processo de verificação
         ↓
World App gera prova criptográfica
```

### Passo 3: Envio da Prova

```
IDKit Widget recebe prova
         ↓
Frontend envia para backend
         ↓
POST /api/worldcoin/verify
```

### Passo 4: Verificação no Backend

```
Backend recebe prova
         ↓
Valida campos obrigatórios
         ↓
Envia para World ID API
         ↓
World ID API verifica prova
         ↓
Retorna resultado
```

### Passo 5: Atualização do Perfil

```
Se verificação bem-sucedida:
         ↓
Salva dados no localStorage
         ↓
Adiciona bônus de tokens
         ↓
Desbloqueia badge
         ↓
Mostra mensagem de sucesso
```

---

## 💻 Implementação

### 1. Configurar Variáveis de Ambiente

```bash
# .env.local
NEXT_PUBLIC_WORLD_APP_ID=app_staging_seu_app_id
NEXT_PUBLIC_WORLD_ACTION_ID=fortex-mining-verification
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

### 2. Usar o Componente

```tsx
import WorldIDVerificationCard from '@/components/world-id/WorldIDVerificationCard';

export default function Page() {
  const handleSuccess = () => {
    console.log('Verificação bem-sucedida!');
  };

  return (
    <WorldIDVerificationCard onVerificationSuccess={handleSuccess} />
  );
}
```

### 3. Acessar Dados do Usuário

```tsx
import { useWorldID } from '@/components/world-id/WorldIDProvider';

export default function Component() {
  const { user, isVerified } = useWorldID();

  if (isVerified && user) {
    return (
      <div>
        <p>Verificado: {user.verificationLevel}</p>
        <p>ID: {user.nullifierHash}</p>
      </div>
    );
  }

  return <p>Não verificado</p>;
}
```

### 4. Chamar API de Verificação

```tsx
import { worldcoinClient } from '@/lib/worldcoin-client';

const result = await worldcoinClient.verifyProof({
  proof: '0x...',
  merkle_root: '0x...',
  nullifier_hash: '0x...',
  verification_level: 'orb',
  action: 'fortex-mining-verification',
});

if (result.success) {
  console.log('Verificação bem-sucedida!');
}
```

---

## 🧪 Testes

### Teste Local (Staging)

```bash
# 1. Iniciar servidor
npm run dev

# 2. Abrir http://localhost:3000

# 3. Clicar em "Verificar com World ID"

# 4. Usar World ID Simulator
# https://simulator.worldcoin.org

# 5. Verificar console para logs
```

### Teste de API

```bash
# Verificar status da integração
curl http://localhost:3000/api/worldcoin/status

# Resposta esperada:
{
  "success": true,
  "status": "healthy",
  "app_id": "app_staging_...",
  "action_id": "fortex-mining-verification",
  "environment": "staging",
  "timestamp": "2024-01-15T10:30:00Z",
  "message": "Integração World ID funcionando normalmente"
}
```

### Teste de Verificação

```bash
# Simular verificação (não recomendado em produção)
curl -X POST http://localhost:3000/api/worldcoin/verify \
  -H "Content-Type: application/json" \
  -d '{
    "proof": "0x...",
    "merkle_root": "0x...",
    "nullifier_hash": "0x...",
    "verification_level": "orb",
    "action": "fortex-mining-verification",
    "app_id": "app_staging_..."
  }'
```

---

## 🔒 Segurança

### Boas Práticas

1. **Nunca compartilhe credenciais**
   ```bash
   # ❌ Errado
   git add .env.local
   
   # ✅ Correto
   echo ".env.local" >> .gitignore
   ```

2. **Validar sempre no backend**
   ```tsx
   // ❌ Errado - confiar apenas no frontend
   if (result.success) {
     updateBalance();
   }
   
   // ✅ Correto - verificar no backend
   const verified = await verifyProofOnBackend(proof);
   if (verified) {
     updateBalance();
   }
   ```

3. **Usar HTTPS em produção**
   ```
   ❌ http://seu-site.com (não funciona)
   ✅ https://seu-site.com (funciona)
   ```

4. **Limpar dados sensíveis**
   ```tsx
   // Não armazenar dados pessoais
   // Usar apenas nullifier_hash como ID único
   const userId = nullifierHash; // ✅ Seguro
   ```

5. **Rate limiting**
   ```tsx
   // Implementar limite de requisições
   // Máximo 1 verificação por usuário
   // Máximo 10 requisições por minuto
   ```

### Criptografia

- **Zero-Knowledge Proofs**: Prova matemática sem revelar dados
- **Nullifier Hash**: ID único e anônimo
- **Merkle Root**: Raiz da árvore de verificação
- **Proof**: Prova criptográfica da verificação

---

## 🐛 Troubleshooting

### Erro: "App ID inválido"

```bash
# Verificar .env.local
cat .env.local | grep WORLD_APP_ID

# Confirmar no Developer Portal
# https://developer.worldcoin.org/projects

# Copiar App ID correto
NEXT_PUBLIC_WORLD_APP_ID=app_staging_seu_app_id_correto

# Reiniciar servidor
npm run dev
```

### Erro: "SDK não carregou"

```bash
# Limpar cache
rm -rf .next
rm -rf node_modules/.cache

# Reinstalar dependências
npm install

# Reiniciar servidor
npm run dev

# Limpar cache do navegador
# Ctrl+Shift+Delete (Windows/Linux)
# Cmd+Shift+Delete (Mac)
```

### Erro: "Verificação falhou"

```bash
# Verificar logs
# Abrir DevTools (F12)
# Ir para Console
# Procurar por mensagens de erro

# Possíveis causas:
# 1. App ID incorreto
# 2. Action não criada
# 3. Domínio não autorizado
# 4. Problema na rede

# Solução:
# 1. Confirmar App ID
# 2. Criar action no Developer Portal
# 3. Adicionar domínio em Settings
# 4. Tentar novamente
```

### Erro: "CORS - Cross-Origin"

```bash
# Adicionar domínio no Developer Portal
# https://developer.worldcoin.org/settings

# Allowed Domains:
# - http://localhost:3000 (desenvolvimento)
# - https://seu-dominio.com (produção)

# Aguardar 5 minutos para propagação
# Tentar novamente
```

---

## 📊 Monitoramento

### Dashboard

Acesse: https://developer.worldcoin.org/dashboard

Métricas disponíveis:
- Total de verificações
- Taxa de sucesso
- Distribuição Orb vs Device
- Usuários únicos verificados
- Tempo médio de verificação

### Logs Locais

```bash
# Abrir DevTools (F12)
# Console

# Você verá:
# ✅ World ID verification successful
# ❌ World ID verification failed
# ⚠️ World ID error: ...
```

---

## 🚀 Deploy em Produção

### Passo 1: Obter App ID de Produção

1. Acesse Developer Portal
2. Vá em Settings
3. Mude para Production
4. Copie novo App ID

### Passo 2: Atualizar Variáveis

```env
NEXT_PUBLIC_WORLD_APP_ID=app_seu_app_id_producao
NEXT_PUBLIC_WORLD_ACTION_ID=fortex-mining-verification
NEXT_PUBLIC_APP_URL=https://seu-dominio.com
NODE_ENV=production
```

### Passo 3: Deploy

```bash
git add .
git commit -m "feat: configurar World ID para produção"
git push origin main
```

### Passo 4: Verificar

1. Acesse seu site em produção
2. Teste verificação
3. Confirme que tudo funciona

---

## 📚 Recursos

- 📖 [Documentação Oficial](https://docs.worldcoin.org)
- 💬 [Discord Community](https://discord.gg/worldcoin)
- 🐦 [Twitter](https://twitter.com/worldcoin)
- 📧 [Suporte](developers@worldcoin.org)
- 🔗 [Developer Portal](https://developer.worldcoin.org)

---

**Pronto para integrar World ID?** Siga o guia passo a passo e sua aplicação estará segura e verificada! 🚀
