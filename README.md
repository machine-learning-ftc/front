Interface de chat para verificação de fake news, integrada à API ISIS de fact-checking com machine learning.

## Tecnologias

- React 18
- Vite
- CSS Modules

## Estrutura do projeto

```
src/
├── hooks/
│   └── useFakeChecker.js   # Lógica de integração com a API
└── components/
    ├── App.jsx              # Componente raiz
    ├── ChatMessage.jsx      # Mensagem individual do chat
    ├── VerdictCard.jsx      # Card com o resultado da análise
    ├── TypingIndicator.jsx  # Indicador de carregamento
    ├── WelcomeScreen.jsx    # Tela inicial
    └── ChatInput.jsx        # Campo de entrada do usuário
```

## Como rodar localmente

### Pré-requisitos
- Node.js 18+
- npm

### Instalação

```bash
npm install
```

### Configuração

Crie um arquivo `.env.local` na raiz do projeto:

```env
VITE_API_URL=https://iris-ten-gamma.vercel.app
```

### Rodar em desenvolvimento

```bash
npm run dev
```

Acesse em **http://localhost:5173**

### Build para produção

```bash
npm run build
```

## Integração com o backend

O frontend se comunica com a API ISIS via:

```
POST {VITE_API_URL}/v1/check
```

**Request:**
```json
{ "query": "texto da afirmação" }
```

**Response:**
```json
{
  "id": "uuid | null",
  "status": "found | predicted",
  "data": {
    "verdict": "true | false | Falta contexto | Parcialmente falso",
    "confidence": 0.94,
    "source": "fact_api | ml",
    "url": "string | null"
  }
}
```

**Mapeamento de vereditos:**
| API retorna | Interface exibe |
|---|---|
| `true` | Verdadeiro |
| `false` | Fake News |
| `Falta contexto` | Falta contexto |
| `Parcialmente falso` | Parcialmente falso |

**Erros tratados:**
- `400` — payload inválido
- `503` — provedores indisponíveis

## Deploy

O projeto está deployado na Vercel. Configure a variável de ambiente `VITE_API_URL` nas configurações do projeto antes de fazer o deploy.
