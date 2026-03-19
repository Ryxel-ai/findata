# @ryxel-ai/findata

TypeScript SDK for the **Ryxel Data B2B API**, auto-generated from the OpenAPI specification.

## Installation

```bash
# Core SDK
npm install @ryxel-ai/findata @hey-api/client-fetch

# Optional: React Query support
npm install @tanstack/react-query
```

## Setup

Configure the API client with your API key:

```typescript
import { client } from "@ryxel-ai/findata/client";

client.setConfig({
  baseUrl: "https://api.ryxeldata.com",
  headers: {
    "x-api-key": "YOUR_API_KEY",
  },
});
```

## Usage with React Query (Optional)

This requires `@tanstack/react-query` to be installed.

```tsx
import { useQuery } from "@tanstack/react-query";
import { getInsiderTransactionsOptions } from "@ryxel-ai/findata/react-query";

function InsiderTransactions() {
  const { data, isLoading } = useQuery(
    getInsiderTransactionsOptions({
      query: { ticker: "AAPL", limit: 100 },
    })
  );

  if (isLoading) return <div>Loading...</div>;

  return (
    <ul>
      {data?.transactions.map((tx, i) => (
        <li key={i}>
          {tx.ownerName} — {tx.transactionCode} — ${tx.transactionValue}
        </li>
      ))}
    </ul>
  );
}
```

## Direct SDK Usage

```typescript
import { getInsiderTransactions } from "@ryxel-ai/findata/sdk";

const { data } = await getInsiderTransactions({
  query: { ticker: "TSLA", limit: 50 },
});

console.log(data?.transactions);
```