# 📊 Analytics

Public endpoints for dashboard rankings and platform-wide stats. No authentication required. Endpoints that require a logged-in user (e.g. user stats, claim rewards) are not documented here.

***

## GET /api/analytics/dashboard/rankings/traders

Get top traders ranked by total trading volume (native token or USD) on a chain.

**Query parameters (all optional):**

| Parameter | Type            | Description                                                     |
| --------- | --------------- | --------------------------------------------------------------- |
| `limit`   | integer (1–100) | Number of results (default: 20)                                 |
| `chainId` | integer         | Chain ID; if omitted or invalid, first configured chain is used |

**Response:** `success`, `rankings` (array of objects with e.g. `rank`, `username`, `address`, `avatar`, `totalVolumeUSD`, `totalVolume`).

***

## GET /api/analytics/dashboard/rankings/points

Get top users ranked by points on a chain.

**Query parameters (all optional):**

| Parameter | Type            | Description                                                     |
| --------- | --------------- | --------------------------------------------------------------- |
| `limit`   | integer (1–100) | Number of results (default: 20)                                 |
| `chainId` | integer         | Chain ID; if omitted or invalid, first configured chain is used |

**Response:** `success`, `rankings` (array with e.g. `rank`, `username`, `address`, `avatar`, `points`), optional `isCached`.

***

## GET /api/analytics/platform/stats

Get platform-wide transparency statistics for a chain (volume, tokens created, fees, treasury, buyback, tier distribution).

**Query parameters (optional):**

| Parameter | Type    | Description                                                     |
| --------- | ------- | --------------------------------------------------------------- |
| `chainId` | integer | Chain ID; if omitted or invalid, first configured chain is used |

**Response:** `success`, and fields such as `totalVolume`, `totalVolumeUSD`, `totalTokensCreated`, `totalRewardsDistributed`, `tierDistribution`, `treasury` (address, balanceETH, balanceUSD), `fees` (buybackFee, treasuryFee), `buybackLp` (threshold, state), etc. Values may be defaults if stats are not yet synced.
