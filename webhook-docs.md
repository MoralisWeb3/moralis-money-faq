# Introduction

Moralis Money supports different types of Alerts and one way to receive alerts is through webhooks.

1. [This documentation explains the structure of the payload.](#Payload-Structure)
2. [How to setup a simple server in both Python (using Flask) and JavaScript (using Express.js). ](#Python-Implementation)
3. [How to receive webhooks to a local server](#Receive-a-webhook)

<br>

## Payload Structure

The webhook payload, known as `ICoinPayload`, is defined as follows:

```typescript

interface IGoPlusHolderInfo = {
    address?: string;
    isLocked?: boolean;
    tag?: string;
    isContract?: boolean;
    balance?: string;
    percent?: string;
    lockedDetail?: {
        optTime?: string;
        endTime?: string;
        amount?: string;
    };
};

interface addLockOptions = {
    token1Address: string | null;
    apiType: string;
    lockDate: number | null;
    unlockDate: number | null;
    lockedAmountInPercent: number;
    type: addLockOptions.type;
    pairAddress: string | null;
};

interface IParsedDexToolsApiResponse = {
    symbol: string;
    name: string;
    creationBlock: number;
    metrics: {
        totalSupply?: number;
        maxSupply?: number;
        circulatingSupply?: number;
        txCount: number;
        holders: number;
        tmcap?: number;
        fdv?: number;
    };
    decimals: string;
    totalSupply: string;
    audit: {
        version: number;
        unlimitedFees: boolean;
        status: string;
        proxy: boolean;
        mint: boolean;
        lockTransactions: boolean;
        date: string;
        codeVerified: boolean;
    };
    info: {
        nftCollection: string;
        extraInfo: string;
        email: string;
        description: string;
        ventures: boolean;
    };
    links: {
        slack: string;
        youtube: string;
        tiktok: string;
        medium: string;
        linkedin: string;
        instagram: string;
        facebook: string;
        bitbucket: string;
        github: string;
        website: string;
        twitter: string;
        telegram: string;
        reddit: string;
        discord: string;
    };
    logo: string;
    pairs: Array<{
        tokenRef: {
            symbol: string;
            name: string;
            address: string;
        };
        price: number;
        dextScore: number;
        exchange: string;
        address: string;
    }>;
    reprPair: {
        dextScore?: number;
        price?: number;
        liquidity?: number;
        tokenRef?: string;
        token: string;
        pair: string;
        exchange: string;
        chain: string;
    };
};

interface IParsedGoPlusTokenSecurityResponse = {
    isOpenSource?: boolean;
    isProxy?: boolean;
    isMintable?: boolean;
    ownerAddress?: string;
    canTakeBackOwnership?: boolean;
    ownerChangeBalance?: boolean;
    hiddenOwner?: boolean;
    selfdestruct?: boolean;
    externalCall?: boolean;
    buyTax?: string;
    sellTax?: string;
    cannotBuy?: boolean;
    cannotSellAll?: boolean;
    slippageModifiable?: boolean;
    isHoneyPot?: boolean;
    transferPausable?: boolean;
    isBlacklisted?: boolean;
    isWhitelisted?: boolean;
    isInDex?: boolean;
    dex?: Array<{
        pair?: string;
        liquidity?: string;
        name?: string;
    }>;
    isAntiWhale?: boolean;
    antiWhaleModifiable?: boolean;
    tradingCooldown?: boolean;
    personalSlippageModifiable?: boolean;
    tokenName?: string;
    tokenSymbol?: string;
    holderCount?: string;
    totalSupply?: string;
    holders?: Array<IGoPlusHolderInfo>;
    ownerBalance?: string;
    ownerPercent?: string;
    creatorAddress?: string;
    creatorBalance?: string;
    creatorPercent?: string;
    lpHolderCount?: string;
    lpTotalSupply?: string;
    lpHolders?: Array<IGoPlusHolderInfo>;
    isTrueToken?: boolean;
    isAirdropScam?: boolean;
    trustList?: boolean;
    otherPotentialRisks?: string;
    note?: string;
};

interface ICoinDetails {
    chainId: string;
    address: string;
    logo: string | null;
    name: string;
    rank: number;
    TotalLiquidityLockedInPercent: number | null;
    TotalSupplyLockedInPercent: number | null;
    chainId: string;
    name: string;
    symbol: string;
    logo?: string;
    chainId_coinTokenAddress: string;
    blockNumber: number;
    blockTimestamp: number;
    needsUpdate: number;
    OneHourLiquidityChange: number;
    OneHourLiquidityChangeUSD: number;
    FourHoursLiquidityChange: number;
    FourHoursLiquidityChangeUSD: number;
    TwelveHoursLiquidityChange: number;
    TwelveHoursLiquidityChangeUSD: number;
    OneDayLiquidityChange: number;
    OneDayLiquidityChangeUSD: number;
    TwoDaysLiquidityChange: number;
    TwoDaysLiquidityChangeUSD: number;
    FourDaysLiquidityChange: number;
    FourDaysLiquidityChangeUSD: number;
    OneWeekLiquidityChange: number;
    OneWeekLiquidityChangeUSD: number;
    TwoWeeksLiquidityChange: number;
    TwoWeeksLiquidityChangeUSD: number;
    ThreeWeeksLiquidityChange: number;
    ThreeWeeksLiquidityChangeUSD: number;
    OneMonthLiquidityChange: number;
    OneMonthLiquidityChangeUSD: number;
    OneQuarterLiquidityChange: number;
    OneQuarterLiquidityChangeUSD: number;
    OneHourHoldersChange: number;
    FourHoursHoldersChange: number;
    TwelveHoursHoldersChange: number;
    OneDayHoldersChange: number;
    TwoDaysHoldersChange: number;
    FourDaysHoldersChange: number;
    OneWeekHoldersChange: number;
    TwoWeeksHoldersChange: number;
    ThreeWeeksHoldersChange: number;
    OneMonthHoldersChange: number;
    OneQuarterHoldersChange: number;
    OneHourBuyersChange: number;
    FourHoursBuyersChange: number;
    TwelveHoursBuyersChange: number;
    OneDayBuyersChange: number;
    TwoDaysBuyersChange: number;
    FourDaysBuyersChange: number;
    OneWeekBuyersChange: number;
    TwoWeeksBuyersChange: number;
    ThreeWeeksBuyersChange: number;
    OneMonthBuyersChange: number;
    OneQuarterBuyersChange: number;
    OneHourExperiencedBuyersChange: number;
    FourHoursExperiencedBuyersChange: number;
    TwelveHoursExperiencedBuyersChange: number;
    OneDayExperiencedBuyersChange: number;
    TwoDaysExperiencedBuyersChange: number;
    FourDaysExperiencedBuyersChange: number;
    OneWeekExperiencedBuyersChange: number;
    TwoWeeksExperiencedBuyersChange: number;
    ThreeWeeksExperiencedBuyersChange: number;
    OneMonthExperiencedBuyersChange: number;
    OneQuarterExperiencedBuyersChange: number;
    FullyDilutedValuation: number;
    MarketCap: number;
    LockLastCheckedAt: string;
    LockEvents: Array<addLockOptions>;
    SecurityInfo: {
        lastCheckedAt: number;
        dexTools: IParsedDexToolsApiResponse;
        goPlusSecurity: IParsedGoPlusTokenSecurityResponse;
    };
    lastUpdatedAt: number;
}

interface ICoinPayload {
    webhookData: {
        tokenQueryName: string;
        coins: ICoinDetails[];
        filterUrl: string;
        notificationPeriod: number;
    }
}

```

---

<br>

## Python Implementation

<br>

### Prerequisites

Flask must be installed:

```bash
pip install flask
```

### Server Setup

<br>

Create a new file server.py:

```python
from flask import Flask, request, jsonify

app = Flask(__name__)

@app.route('/', methods=['POST'])
def respond():
    print(request.json)
    return jsonify(request.json), 200

if __name__ == '__main__':
    app.run(port=5000, debug=True)
```

### Start Server

<br>

To start the server, run:

```bash
python server.py
```

The server will listen for POST requests on localhost:5000. When a POST request is received, it prints the JSON body to the console and responds with the same JSON body.

---

<br>

## JavaScript Implementation

<br>

### Prerequisites
Express.js and body-parser must be installed:

```bash
npm install express body-parser
```

<br>

### Server Setup
Create a new file server.js:

```typescript
const express = require('express');
const bodyParser = require('body-parser');

const app = express();

app.use(bodyParser.json());

app.post('/', (req, res) => {
    console.log(req.body);
    res.status(200).json(req.body);
});

app.listen(5000, () => console.log('Server started on port 5000'));
```

<br>

### Start Server

To start the server, run:

```
node server.js
```

The server will listen for POST requests on localhost:5000. When a POST request is received, it prints the JSON body to the console and responds with the same JSON body.

---

<br>

## Receive a webhook

If your server is not hosted on an accessible server you won't be able to receive the webhook locally.

You can use Ngrok to forward requests to your local server

<br>

### Setting Up Ngrok

Ngrok exposes local servers behind NATs and firewalls to the public internet over secure tunnels. It's a very useful tool for webhook development because it lets you inspect the request and response payloads, which are a part of the webhook's HTTP traffic.

<br>

### Installation
Ngrok can be downloaded from their official website. After downloading, unzip the file.

<br>

### Usage

In your terminal, navigate to the directory where you've unzipped ngrok.

Run the following command to start ngrok:

```bash
./ngrok http 5000
```

Replace 5000 with the port where your local server is running.

Ngrok will provide a Forwarding URL, which looks like http://1234567890ab.ngrok.io or https://1234567890ab.ngrok.io. 

Use this URL as your webhook URL in Moralis Money UI.

![Screenshot 2023-05-18 at 7 19 51 PM](https://github.com/gabkk/moralis-money-faq/assets/10153882/bec9f186-4995-40ea-8a48-f24cb349640c)


<br>

With ngrok running, your local server is now publicly accessible from the internet.

Send a webhook to the ngrok URL, and ngrok will forward the request to your local server.

