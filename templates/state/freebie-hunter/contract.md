# Freebie Hunter Data Contract

This contract applies to every Freebie Hunter run. Keep these field names exact
when writing JSON files.

## Canonical Files

- `config.json`: search configuration
- `listings.json`: master state
- `outreach-queue.json`: queue for human-selected outreach
- `../reports/freebie-hunter-report.md`: human-readable report

Do not create alternative snapshot, mirror, or legacy files with similar
content.

## config.json

```json
{
  "version": 1,
  "configured": false,
  "source": {
    "name": "",
    "site": "kleinanzeigen",
    "city": "",
    "category": "Zu verschenken",
    "searchUrl": "",
    "pageUrls": [],
    "maxPages": 3
  }
}
```

Rules:

- If `configured=false` or `source.searchUrl` is missing, no collection run may
  start.
- Ask the user for the city or a copied Kleinanzeigen search URL for
  `Zu verschenken`.
- Set `configured=true` only when the URL clearly matches the target city and
  category.
- `source.pageUrls` contains the pages the collector may fetch. Page 1 must be
  `source.searchUrl`.
- `source.maxPages` limits fetched search pages.
- Source configuration lives only in `config.json`.

## listings.json

Top level:

```json
{
  "version": 1,
  "updatedAt": "ISO-8601 or null",
  "listings": []
}
```

Listing object:

```json
{
  "listingId": "string",
  "sourceUrl": "string",
  "canonicalUrl": "string",
  "title": "string",
  "location": "string",
  "postedText": "string",
  "previewText": "string",
  "imageUrl": "string",
  "firstSeenAt": "ISO-8601",
  "lastSeenAt": "ISO-8601",
  "status": "discovered",
  "changeFingerprint": "string",
  "needsEvaluation": true,
  "evaluation": {
    "lastEvaluatedAt": null,
    "resaleScore": 0,
    "confidence": "low",
    "reasons": [],
    "riskFlags": [],
    "estimatedFlipPotential": "low",
    "recommendedAction": "review",
    "stage": "list"
  },
  "outreach": {
    "status": "idle",
    "lastActionAt": null,
    "draftedAt": null,
    "sentAt": null,
    "attemptCount": 0,
    "sellerFingerprint": "",
    "messageDraft": "",
    "lastError": ""
  }
}
```

## outreach-queue.json

Top level:

```json
{
  "version": 1,
  "updatedAt": "ISO-8601 or null",
  "items": []
}
```

Queue object:

```json
{
  "listingId": "string",
  "canonicalUrl": "string",
  "title": "string",
  "status": "selected",
  "queuedAt": "ISO-8601",
  "lastQueuedBy": "chat|operator|cron",
  "outreachStatus": "pending"
}
```

## Status Values

Listing status:

- `discovered`
- `screened`
- `shortlisted`
- `ignored`
- `selected`
- `drafted`
- `sent`
- `failed`
- `expired`

Outreach status:

- `idle`
- `pending`
- `drafted`
- `sent`
- `failed`
