# 🚀 @ryxel-ai/findata

The official TypeScript SDK for the **Ryxel Data API** 📊.

## 🌟 Introduction

**Ryxel Data** provides institutional-grade financial datasets through a simple, RESTful API. This SDK is auto-generated from the OpenAPI specification and designed to give you programmatic access to high-quality financial data, including:

- 📑 **Insider Transactions**: Direct access to SEC Form 4 and Form 3 filings.
- 📦 **ETF Holdings**: Comprehensive visibility into exchange-traded fund portfolios.
- 💰 **Earnings & IPOs**: Up-to-date calendars and historical data.
- 🏛️ **Institutional Data**: Standardized datasets for large-scale analysis.

All data is sourced directly from official filings and standardized for easy consumption, allowing you to focus on building your application instead of cleaning data.

## 📚 Documentation

For detailed guides, endpoint references, and API documentation, please visit: **[https://data.ryxel.ai/docs](https://data.ryxel.ai/docs)**

## 📦 Installation

```bash
# Core SDK
npm install @ryxel-ai/findata @hey-api/client-fetch

# Optional: React Query support
npm install @tanstack/react-query
```

## ⚙️ Setup

Configure the API client with your API key (don't have one? [create an account at data.ryxel.ai](https://data.ryxel.ai)):

```typescript
import { client } from "@ryxel-ai/findata/client";

client.setConfig({
  baseUrl: "https://api.ryxeldata.com",
  headers: {
    "x-api-key": "YOUR_API_KEY",
  },
});
```

## ⚛️ Usage with React Query

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

## 🛠️ Direct SDK Usage

```typescript
import { getInsiderTransactions } from "@ryxel-ai/findata/sdk";

const { data } = await getInsiderTransactions({
  query: { ticker: "TSLA", limit: 50 },
});

console.log(data?.transactions);
```