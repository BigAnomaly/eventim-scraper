[Eventim Scraper](https://apify.com/zen-studio/eventim-scraper?fpr=data)

# Eventim Scraper | Events, Concerts & Ticket Prices from eventim.de (2026)

> 22+ fields per event at 1,000+ events/minute  — prices, availability, venues, ratings, and 532 searchable categories from Germany's largest ticket platform.

### Copy to your AI assistant

Copy this block into ChatGPT, Claude, Cursor, or any LLM to start using this actor.

```
zen-studio/eventim-scraper on Apify. Call: ApifyClient("TOKEN").actor("zen-studio/eventim-scraper").call(run_input={...}), then client.dataset(run["defaultDatasetId"]).list_items().items for results. Key inputs: categories (array, 532 enum values like "Konzerte", "Jazz & Blues", "Heavy Metal"), city (string), maxResults (int, default 1000). Full actor spec (input schema with all params/enums/defaults, output dataset fields, README): GET https://api.apify.com/v2/acts/zen-studio~eventim-scraper/builds/default (Bearer TOKEN) → inputSchema (JSON string, parse it), actorDefinition.storages.dataset.views.overview.transformation.fields (output field list), readme. Free tier: 10 runs, 10 results/run. Get token: https://console.apify.com/account/integrations
```

## Key Features

- **22+ fields per event** including venue coordinates, per-category ticket prices, and series metadata
- **532 searchable categories** covering concerts, sports, theater, comedy, festivals, and 486 niche genre tags
- **1,000 events in under 60 seconds** with parallel fetching and price enrichment
- **Free tier** with 10 lifetime runs and 10 results per run

![Eventim Scraper](https://images.apifyusercontent.com/KFudb_FWJGXQzS9ysaPfNmaGWIwQqCEVFRbydb4eScM/w:1800/cb:1/aHR0cHM6Ly9paWxpLmlvL0JXTldDVU4ucG5n.webp)

## How to Scrape Eventim Events

### Basic — browse concerts

```
{
    "categories": ["Konzerte"],
    "maxResults": 100
}
```

### Filter by city and date

```
{
    "categories": ["Jazz & Blues"],
    "city": "Berlin",
    "dateFrom": "2026-06-01",
    "dateTo": "2026-06-30",
    "sortBy": "DateAsc"
}
```

### Search by artist

```
{
    "artist": "Rammstein",
    "maxResults": 50
}
```

### Filter by price range

```
{
    "categories": ["Konzerte"],
    "priceMin": 30,
    "priceMax": 80,
    "city": "München"
}
```

## Input Parameters

| Parameter | Type | Default | Description |
| --- | --- | --- | --- |
| `searchTerm` | string |  | Free-text search across artists, events, venues |
| `categories` | array | `["Konzerte"]` | Pick from 532 categories (type to search) |
| `city` | string |  | City name (Berlin, München, Köln, etc.) |
| `dateFrom` | string |  | Start date (YYYY-MM-DD) |
| `dateTo` | string |  | End date (YYYY-MM-DD) |
| `artist` | string |  | Artist name (auto-resolved to ID) |
| `venue` | string |  | Venue name (auto-resolved to ID) |
| `postalCode` | string |  | German PLZ for radius search |
| `distanceKm` | integer | `20` | Radius in km around postal code |
| `priceMin` | integer |  | Min ticket price in EUR |
| `priceMax` | integer |  | Max ticket price in EUR |
| `sortBy` | string | `Recommendation` | Sort: Recommendation, DateAsc, DateDesc, Rating, NameAsc, NameDesc |
| `eventSeriesIds` | array | `[]` | Direct lookup by series ID (skips search) |
| `includePriceDetails` | boolean | `true` | Fetch starting price and availability per event |
| `includeCategoryPricing` | boolean | `false` | Fetch per-category price breakdown (slower) |
| `maxResults` | integer | `1000` | Maximum events to return |

## What Data Can You Extract from Eventim?

Every result includes:

- **Event details** — ID, name, URL, image, type, start/end date
- **Venue** — name, city, street address, postal code, country, lat/lng coordinates
- **Pricing** — starting price, display price, crossed-out price, currency, per-category breakdown
- **Availability** — status (Available, SoldOut, Cancelled, etc.), localized status message
- **Ratings** — count and average score
- **Categories** — hierarchical (parent + child)
- **Series info** — series ID, name, description, total events, date range

### Output Example

```
{
  "eventId": "21471874",
  "eventName": "André Rieu - Tour 2027",
  "eventUrl": "https://www.eventim.de/event/andre-rieu-tour-2027-uber-arena-berlin-21471874/",
  "imageUrl": "https://www.eventim.de/obj/media/.../andre-rieu-27-tickets-2026.jpg",
  "type": "LiveEntertainment",
  "startDate": "2027-01-27T19:30:00+01:00",
  "venue": {
    "name": "Uber Arena Berlin",
    "city": "Berlin",
    "streetAddress": "Uber-Platz 1 (Mühlenstraße 19)",
    "postalCode": "10243",
    "country": "DE",
    "latitude": 52.5167,
    "longitude": 13.4000
  },
  "categories": [
    { "name": "Kultur" },
    { "name": "Klassische Konzerte", "parent": "Kultur" }
  ],
  "tags": ["TICKETDIRECT", "FANTICKET"],
  "status": "Available",
  "statusMessage": "Verfügbar",
  "hasRecommendation": false,
  "marketingLabels": [],
  "rating": { "count": 5334, "average": 4.60 },
  "fromPrice": 65.25,
  "fromPriceDisplay": "€ 65,25",
  "crossedOutPrice": null,
  "currency": "EUR",
  "priceCategories": [
    { "name": "Sitzplatz Premium", "price": 155.25, "currency": "EUR", "availability": "InStock" },
    { "name": "Sitzplatz Kategorie 1", "price": 135.25, "currency": "EUR", "availability": "InStock" },
    { "name": "Sitzplatz Kategorie 2", "price": 115.25, "currency": "EUR", "availability": "InStock" },
    { "name": "Sitzplatz Kategorie 3", "price": 89.25, "currency": "EUR", "availability": "InStock" },
    { "name": "Sitzplatz Kategorie 4", "price": 65.25, "currency": "EUR", "availability": "InStock" },
    { "name": "Sitzplatz Premium - Gangplatz", "price": 160.25, "currency": "EUR", "availability": "InStock" },
    { "name": "Sitzplatz Kategorie 1 - Gangplatz", "price": 140.25, "currency": "EUR", "availability": "InStock" },
    { "name": "Sitzplatz Kategorie 2 - Gangplatz", "price": 120.25, "currency": "EUR", "availability": "InStock" }
  ],
  "eventSeries": {
    "id": "4109350",
    "name": "André Rieu - Tour 2027",
    "url": "https://www.eventim.de/artist/andre-rieu/andre-rieu-tour-2027-4109350/",
    "totalEvents": 11,
    "startDate": "2027-01-13T19:30:00+01:00",
    "endDate": "2027-01-29T20:00:00+01:00"
  },
  "scrapedAt": "2026-04-12T07:30:20Z"
}
```

| Zen Studio Events   •  Event data from every major platform |
| --- |
| Eventim Scraper  ➤ You are here | ![](https://images.apifyusercontent.com/OGUQoDVMfn-X6kMMmslvt9BAmG9bKKXZwWBiWkmtHGM/w:1800/cb:1/aHR0cHM6Ly9hcGlmeS1pbWFnZS11cGxvYWRzLXByb2QuczMudXMtZWFzdC0xLmFtYXpvbmF3cy5jb20vTldZc09HOTZmTUR5OHljZGYtYWN0b3ItRzdrdXI0cGFDenJ5ZlRBZVgtWlFZSWVVVnlvVi1HZW1pbmlfR2VuZXJhdGVkX0ltYWdlX2llYmpwcmllYmpwcmllYmoucG5n.webp)  [10times Events](https://apify.com/zen-studio/10times-events-scraper)  Trade shows & conferences |

## Advanced Usage

### Niche genre tags

Use long-tail tags from the 486-item "Weitere Kategorien" list to find specific genres.

```
{
    "categories": ["Heavy Metal", "Punk"],
    "city": "Hamburg",
    "maxResults": 200
}
```

### Radius search around a postal code

Find events within 50km of central Munich.

```
{
    "postalCode": "80331",
    "distanceKm": 50,
    "categories": ["Konzerte"],
    "sortBy": "DateAsc"
}
```

### Per-category ticket pricing

Get the full price breakdown per ticket category (Kategorie 1, 2, 3, Stehplatz, etc.).

```
{
    "categories": ["Kultur", "Klassische Konzerte"],
    "city": "Berlin",
    "includeCategoryPricing": true,
    "maxResults": 50
}
```

### Direct series lookup

If you already have event series IDs from a previous scrape, look them up directly.

```
{
    "eventSeriesIds": ["3789122", "3967548"]
}
```

## Pricing — Pay Per Event (PPE)

**$6.99 per 1,000 results.**

| Results | Cost |
| --- | --- |
| 10 | ~$0.07 |
| 100 | ~$0.70 |
| 1,000 | ~$6.99 |

Free tier: 10 lifetime runs, 10 results per run.

### Cost Optimization

- Use `categories` and `city` to narrow results before scraping
- Set `maxResults` to only what you need
- Keep `includeCategoryPricing` off unless you need per-category prices (it's slower)

## FAQ

**How many events can I extract?**
eventim.de has 100,000+ events at any time across all categories. You can extract up to the full catalog in a single run.

**How fresh is the data?**
Real-time. Every run fetches live data directly from eventim.de.

**What categories are available?**
532 total: 8 top-level (Konzerte, Sport, Kultur, Humor, Musical & Show, Freizeit, Ticket-Gutschein, VIP & Extras), 49 subcategories (Jazz & Blues, Rock & Pop, Fußball, Theater, etc.), and 486 niche tags (Heavy Metal, K-Pop, 2. Bundesliga, Poetry-Slam, etc.).

**Can I filter by price?**
Yes. Set `priceMin` and/or `priceMax` (in EUR). When price filters are active, the actor returns individual events instead of event series.

**What does "per-category pricing" mean?**
German venues often have tiered seating (Kategorie 1, 2, 3, Stehplatz). The `includeCategoryPricing` option fetches the price for each tier. It's slower because it loads each event's detail page.

**What's the "status" field?**
Available, SoldOut, Cancelled, Moved, Blocked, InProgress, Expired, or Released. The `statusMessage` field gives the German-localized version (e.g. "Wenige Tickets" = few tickets left).

**Does it work for countries outside Germany?**
Currently DE only. Other CTS Eventim markets (AT, CH, PL, NL) use different configurations and haven't been tested.

**What's the free tier?**
10 lifetime runs with 10 results per run. No credit card required.

**Can I use this with my AI assistant?**
Yes. Copy the "Copy to your AI assistant" block above into any LLM. The full input schema with all 532 categories is available via the Apify API.

**How fast is it?**
1,000 events with prices in under 60 seconds. Speed depends on proxy latency and whether per-category pricing is enabled.

## Support

- **Bugs**: Issues tab
- **Features**: Issues tab

## Legal Compliance

Extracts publicly available data. Users must comply with eventim.de terms and data protection regulations (GDPR, CCPA).

---

*Scrape events, prices, and availability from Germany's largest ticket platform.*