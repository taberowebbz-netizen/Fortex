
# 📡 Documentação da API - Fortex Mining

## Visão Geral

Esta documentação descreve todas as rotas de API disponíveis no aplicativo Fortex para gerenciamento de mineração, recompensas e ranking.

## Base URL

```
/next_api
```

## Autenticação

Todas as rotas que modificam dados requerem verificação World ID. O `worldIdHash` deve ser enviado no corpo da requisição.

---

## 🔨 Mining Endpoints

### Iniciar Mineração

**POST** `/mining/start`

Inicia uma nova sessão de mineração para um usuário verificado.

**Request Body:**
```json
{
  "userId": "user_123",
  "worldIdHash": "0x..."
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "worldIdHash": "0x...",
    "startTime": 1704067200000,
    "isActive": true,
    "tokensEarned": 0,
    "miningRate": 10
  }
}
```

---

### Parar Mineração

**POST** `/mining/stop`

Finaliza uma sessão de mineração e calcula recompensas.

**Request Body:**
```json
{
  "userId": "user_123",
  "startTime": 1704067200000,
  "sessionDuration": 3600
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "tokensEarned": 11.0,
    "sessionDuration": 3600,
    "bonusApplied": true,
    "bonusPercentage": 10,
    "timestamp": "2024-01-01T00:00:00.000Z"
  }
}
```

**Bônus:**
- Sessões > 1 hora: +10% de tokens

---

### Reivindicar Tokens

**POST** `/mining/claim`

Reivindica tokens minerados e adiciona ao saldo do usuário.

**Request Body:**
```json
{
  "userId": "user_123",
  "tokensToClaim": 50.5,
  "worldIdHash": "0x..."
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "tokensClaimed": 50.5,
    "transactionId": "tx_1704067200000_user_123",
    "timestamp": "2024-01-01T00:00:00.000Z",
    "status": "success"
  }
}
```

---

## 🎁 Rewards Endpoints

### Reivindicar Recompensa Diária

**POST** `/rewards/daily`

Processa check-in diário e concede recompensas.

**Request Body:**
```json
{
  "userId": "user_123",
  "consecutiveDays": 5,
  "worldIdHash": "0x..."
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "rewardAmount": 7.5,
    "consecutiveDays": 6,
    "nextRewardIn": 86400000,
    "bonusApplied": true,
    "timestamp": "2024-01-01T00:00:00.000Z"
  }
}
```

**Cálculo de Recompensa:**
- Base: 5 FORTEX
- Bônus de Streak: +0.5 FORTEX por dia consecutivo (máx 30 dias)

---

### Verificar Status de Recompensa Diária

**GET** `/rewards/daily?userId=user_123`

Verifica se o usuário pode fazer check-in.

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "canCheckIn": true,
    "lastCheckIn": "2024-01-01T00:00:00.000Z",
    "nextCheckInAvailable": "2024-01-02T00:00:00.000Z",
    "consecutiveDays": 5
  }
}
```

---

## 🏆 Leaderboard Endpoints

### Obter Ranking

**GET** `/leaderboard?limit=10&offset=0`

Retorna o ranking global de mineradores.

**Query Parameters:**
- `limit` (opcional): Número de resultados (padrão: 10)
- `offset` (opcional): Offset para paginação (padrão: 0)

**Response:**
```json
{
  "success": true,
  "data": {
    "leaderboard": [
      {
        "rank": 1,
        "userId": "user_1",
        "username": "Minerador 1",
        "totalTokens": 9500,
        "level": 7,
        "verificationLevel": "orb",
        "isVerified": true
      }
    ],
    "totalMiners": 1000,
    "userRank": 42,
    "lastUpdated": "2024-01-01T00:00:00.000Z"
  }
}
```

---

## 📊 User Stats Endpoints

### Obter Estatísticas do Usuário

**GET** `/user/stats?userId=user_123`

Retorna estatísticas detalhadas de mineração do usuário.

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "totalMined": 1234.56,
    "todayMined": 45.67,
    "weeklyMined": 320.5,
    "monthlyMined": 890.12,
    "averagePerDay": 30.5,
    "miningHours": 123.5,
    "rank": 42,
    "totalMiners": 1000,
    "weeklyData": [
      {
        "day": "Dom",
        "amount": 45.5,
        "date": "2024-01-01T00:00:00.000Z"
      }
    ],
    "lastActive": "2024-01-01T00:00:00.000Z"
  }
}
```

---

## 🏅 Badges Endpoints

### Verificar e Conceder Badges

**POST** `/badges/check`

Verifica conquistas e concede badges automaticamente.

**Request Body:**
```json
{
  "userId": "user_123",
  "totalTokens": 150,
  "totalMined": 200,
  "consecutiveDays": 10,
  "currentBadges": ["first_mine"]
}
```

**Response:**
```json
{
  "success": true,
  "data": {
    "userId": "user_123",
    "newBadges": ["week_streak", "hundred_tokens"],
    "totalBadges": 3,
    "allBadges": ["first_mine", "week_streak", "hundred_tokens"],
    "timestamp": "2024-01-01T00:00:00.000Z"
  }
}
```

**Badges Disponíveis:**
- `first_mine`: Primeira mineração completa
- `week_streak`: 7 dias consecutivos
- `month_streak`: 30 dias consecutivos
- `hundred_tokens`: 100+ tokens acumulados
- `thousand_tokens`: 1000+ tokens acumulados
- `top_10`: Top 10 no ranking

---

## ❌ Tratamento de Erros

Todas as rotas retornam erros no seguinte formato:

```json
{
  "success": false,
  "errorCode": "INVALID_REQUEST",
  "errorMessage": "User ID is required"
}
```

**Códigos de Status HTTP:**
- `200`: Sucesso
- `201`: Criado com sucesso
- `400`: Requisição inválida
- `403`: Não autorizado (World ID não verificado)
- `404`: Recurso não encontrado
- `500`: Erro interno do servidor

---

## 🔐 Segurança

### World ID Verification

Todas as operações que modificam dados requerem:
1. `userId` válido
2. `worldIdHash` do usuário verificado
3. Verificação de prova criptográfica

### Rate Limiting

- Mineração: 1 sessão ativa por usuário
- Check-in diário: 1 vez a cada 24 horas
- Reivindicação de tokens: Sem limite (mas requer tokens disponíveis)

---

## 📚 Biblioteca Cliente

Use `src/lib/api-mining.ts` para chamadas tipadas:

```typescript
import { miningApi } from '@/lib/api-mining';

// Iniciar mineração
const session = await miningApi.startMining(userId, worldIdHash);

// Parar mineração
const result = await miningApi.stopMining(userId, startTime, duration);

// Obter ranking
const leaderboard = await miningApi.getLeaderboard(10, 0);
```

---

## 🧪 Testes

### Exemplo com cURL

```bash
# Iniciar mineração
curl -X POST http://localhost:3000/next_api/mining/start \
  -H "Content-Type: application/json" \
  -d '{"userId":"user_123","worldIdHash":"0xtest"}'

# Obter ranking
curl http://localhost:3000/next_api/leaderboard?limit=5
```

---

## 📝 Notas

- Todos os timestamps são em formato ISO 8601
- Valores de tokens são números decimais com até 4 casas
- IDs de usuário seguem o formato `user_*` ou `wld_*`
- Dados de ranking são atualizados em tempo real

