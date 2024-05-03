# Examples of JSON-RPC usage

## Navigation

- [Example 1](#example-1)

### Example 1

**Source**: <https://github.com/deepspace99/editorial/blob/d7d2ec6f35db9fb2d2efe78c3416e540d5aab39a/src/pages/signup.tsx#L55-L70>

```TypeScript
const response = await fetch(network.nodeUrl, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    jsonrpc: '2.0',
    id: 'dontcare',
    method: 'query',
    params: {
      request_type: 'view_account',
      finality: 'final',
      account_id: `${desiredUsername}.${network.fastAuth.accountIdSuffix}`,
    },
  }),
});

```

### Example 2

**Source**: <https://github.com/thirdweb-dev/dashboard/blob/f834242134f06e0d75e98eee52d9b04e65e0e04a/src/pages/%5BchainSlug%5D/index.tsx#L73-L100>

```TypeScript
return useQuery({
    queryKey: ["chain_stats", { chainId: chain.chainId, rpcUrl }],
    queryFn: async () => {
      // we'll just ... manually fetch?
      const startTimeStamp = performance.now();
      const res = await fetch(rpcUrl, {
        method: "POST",
        body: JSON.stringify({
          jsonrpc: "2.0",
          method: "eth_blockNumber",
          params: [],
          id: 1,
        }),
      });


      const json = await res.json();
      const latency = performance.now() - startTimeStamp;


      return {
        latency,
        blockNumber: parseInt(json.result, 16),
      };
    },
    refetchInterval: 5 * 1000,
    enabled: !!rpcUrl,
    placeholderData,
  });
}

```

### Example 3

**Source**: <https://github.com/MetaMask/metamask-extension/blob/4a1853cf7b66ad1a9da4ef43b23a52a1db7cca6e/ui/contexts/snaps/snap-interface.tsx#L91-L108>

```TypeScript
handleSnapRequest({
  snapId,
  origin: '',
  handler: 'onUserInput',
  request: {
    jsonrpc: '2.0',
    method: ' ',
    params: {
      event: {
        type: event,
        // TODO: Allow null in the types and simplify this
        ...(name !== undefined && name !== null ? { name } : {}),
        ...(value !== undefined && value !== null ? { value } : {}),
      },
      id: interfaceId,
    },
  },
});
```

### Example 4

**Source**: <https://github.com/near/near-discovery/blob/1004f353010a560e8422abf36580bf6e43d5b384/src/pages/signup.tsx#L54-L69>

```TypeScript
const response = await fetch(network.nodeUrl, {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    jsonrpc: '2.0',
    id: 'dontcare',
    method: 'query',
    params: {
      request_type: 'view_account',
      finality: 'final',
      account_id: `${desiredUsername}.${network.fastAuth.accountIdSuffix}`,
    },
  }),
});
```

### Example 5

**Source**: <https://github.com/solana-labs/governance-ui/blob/e8d55a8a8518c64831e19910e582b3d1260814bd/hooks/queries/digitalAssets.ts#L173-L193>

```TypeScript
export const dasByIdQueryFn = async (network: Network, id: PublicKey) => {
  const url = getHeliusEndpoint(network)
  const response = await fetch(url, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      jsonrpc: '2.0',
      id: 'Realms user',
      method: 'getAsset',
      params: {
        id: id.toString(),
      },
    }),
  })


  const x = await response.json()
  if (x.error) return { found: false, result: undefined, err: x.error }
  return { result: x.result as DasNftObject, found: true }
}
```

### Example 6

**Source**: <https://github.com/solana-labs/governance-ui/blob/e8d55a8a8518c64831e19910e582b3d1260814bd/utils/GovernanceTools.tsx#L83-L115C2>

```TypeScript
const getProposalsFilter = (
  programId: PublicKey,
  connection: ConnectionContext,
  memcmpBytes: string,
  pk: PublicKey
) => {
  return {
    jsonrpc: '2.0',
    id: 1,
    method: 'getProgramAccounts',
    params: [
      programId.toBase58(),
      {
        commitment: connection.current.commitment,
        encoding: 'base64',
        filters: [
          {
            memcmp: {
              offset: 0, // number of bytes
              bytes: memcmpBytes, // base58 encoded string
            },
          },
          {
            memcmp: {
              offset: 1,
              bytes: pk.toBase58(),
            },
          },
        ],
      },
    ],
  }
}
```

### Example 7

**Source**: <https://github.com/BitHighlander/skatehive-v2/blob/6bb78846917dd2aac6565c0ec0a69deb6b71ee48/src/lib/pages/home/dao/communityStats.tsx#L34-L39C12>

```TypeScript
const hiveBlogResponse = await axios.post("https://api.hive.blog", {
  jsonrpc: "2.0",
  method: "bridge.get_payout_stats",
  params: { limit: 150 },
  id: 1,
});
```

### Example 8

**Source**: <https://github.com/near/fast-auth-signer/blob/394a4dc0315a1a3925c62149e2cdf69b8e3d0e84/packages/near-fast-auth-signer/src/components/CreateAccount/CreateAccount.tsx#L36-L51>

```TypeScript
const response = await fetch(network.nodeUrl, {
  method:  'POST',
  headers: {
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    jsonrpc: '2.0',
    id:      'dontcare',
    method:  'query',
    params:  {
      request_type: 'view_account',
      finality:     'final',
      account_id:   `${desiredUsername}.${network.fastAuth.accountIdSuffix}`,
    },
  }),
});
```
