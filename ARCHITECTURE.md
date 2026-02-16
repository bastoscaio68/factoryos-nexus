# FactoryOS Nexus — Arquitetura Técnica

## Visão Geral

FactoryOS Nexus é um sistema de visualização e controle centralizado que usa **Three.js** para criar uma experiência visual imersiva do ecossistema FactoryOS.

```
┌────────────────────────────────────────────────────────────────────────────┐
│                           FACTORYOS NEXUS                                   │
├────────────────────────────────────────────────────────────────────────────┤
│                                                                            │
│                              🌐 NEXUS CORE                                  │
│                    (Visualização 3D Interativa)                            │
│                                                                            │
│         ┌──────────┐     ┌──────────┐     ┌──────────┐                  │
│         │  BRAIN   │────►│ ORQUEST. │────►│  TRADING │                  │
│         │  Node    │     │   Node   │     │   Node   │                  │
│         └──────────┘     └──────────┘     └──────────┘                  │
│              │               │                   │                          │
│              ▼               ▼                   ▼                          │
│         ┌──────────┐  ┌──────────┐      ┌──────────┐                     │
│         │ PROJECTS │  │  AGENTS  │      │ FINANCE  │                     │
│         │  Node    │  │   Hub    │      │   Node   │                     │
│         └──────────┘  └──────────┘      └──────────┘                     │
│                                                                            │
└────────────────────────────────────────────────────────────────────────────┘
```

---

## 🎨 Componentes Visuais (Three.js)

### 1. Nexus Core Globe
- Esfera central representando o "cérebro" do sistema
- Anéis orbitais mostrando fluxo de dados
- Partículas animadas representando agentes ativos
- Cores dinâmicas baseadas no status do sistema

### 2. Agent Nodes
- Esferas menores orbitando o núcleo
- Cada nó = um agente
- Tamanho = volume de atividade
- Cor = status (ativo, ocupado, inativo)

### 3. Flow Streams
- Linhas conectando nós
- Animação de pulsos mostrando mensagens
- Cores indicando tipo de comunicação

### 4. Data Constellation
- Stars de fundo com dados do sistema
- Clusters de projetos, métricas, trades

---

## 📂 Estrutura do Projeto

```
factoryos-nexus/
├── src/
│   ├── components/
│   │   ├── NexusCore.jsx          # Globe 3D principal
│   │   ├── AgentNode.jsx         # Nós de agentes
│   │   ├── FlowStream.jsx        # Conexões animadas
│   │   ├── CommandCenter.jsx     # 输入 de comandos
│   │   ├── MetricsPanel.jsx      # KPIs e métricas
│   │   └── AgentStatus.jsx       # Cards de status
│   ├── hooks/
│   │   ├── useAgents.js          # Dados dos agentes
│   │   ├── useProjects.js        # Dados dos projetos
│   │   ├── useTrading.js         # Dados de trading
│   │   └── useNexus.js           # Core logic
│   ├── services/
│   │   ├── github.js             # GitHub API
│   │   ├── openclaw.js           # Gateway API
│   │   └── websocket.js           # Tempo real
│   ├── styles/
│   │   ├── colors.css            # Variáveis de cor
│   │   └── animations.css         # Animações
│   └── utils/
│       ├── calculations.js        # math helpers
│       └── formatters.js         # data formatting
├── public/
│   └── assets/
│       └── textures/
├── index.html
└── package.json
```

---

## 🔌 Integrações

### GitHub API
```javascript
GET /repos/bastoscaio68/factoryos-dashboard/contents
GET /repos/bastoscaio68/factoryos-dashboard/commits
```

### OpenClaw Gateway
```javascript
ws://localhost:18790 (local)
ws://gateway.factoryos.io (produção)
```

### Trading Data (opcional)
```javascript
GET https://api.coingecko.com/v3/coins/bitcoin
```

---

## 🎯 Fluxo de Dados

```
1. User Access
        │
        ▼
2. Load Initial Data (GitHub API)
        │
        ▼
3. Connect WebSocket (OpenClaw)
        │
        ▼
4. Render Nexus Core (Three.js)
        │
        ▼
5. Update in Real-time ◄────────┐
        │                         │
        ▼                         │
6. User Interactions            │
        │                         │
        ▼                         │
7. Command Processing           │
        │                         │
        └─────────────────────────┘
```

---

## 📊 Métricas em Tempo Real

| Métrica | Fonte | Atualização |
|---------|-------|------------|
| Agentes ativos | OpenClaw | 1s |
| Projetos | GitHub | 30s |
| PnL Trading | CoinGecko | 5s |
| Income/Expense | Manual | 1h |

---

## 🎨 Design Tokens

```css
:root {
  /* Cores Principais */
  --nexus-core: #00d4ff;
  --nexus-glow: #00ffcc;
  --agent-active: #10b981;
  --agent-busy: #f59e0b;
  --agent-inactive: #6b7280;
  
  /* Status Colors */
  --status-success: #10b981;
  --status-warning: #f59e0b;
  --status-error: #ef4444;
  --status-info: #3b82f6;
  
  /* Backgrounds */
  --bg-deep: #0a1628;
  --bg-card: rgba(15, 31, 53, 0.95);
  --bg-glass: rgba(10, 22, 40, 0.8);
}
```

---

*Arquitetura criada pela Reunião Extraordinária FactoryOS*
*Data: 2026-02-16 15:35 GMT-3*
