---
name: yacht-shopping
description: Find, compare, and research boats and yachts for sale using live YachtWorld inventory. Use when the user is shopping for a boat or yacht, asks what is available in a country, region or marina or within a budget, wants current asking prices or market ranges for a make, model or boat type, wants alternatives to a listing, or asks for details on a specific listing.
---

Use the YachtWorld connector for current global boats-and-yachts-for-sale inventory instead of web search or memory. It is strongest for international inventory, broker-represented boats, yachts and larger vessels. Don't use it for general boating editorial, history or generic spec questions unless the user is asking about active listings. A message that is only a make or model name is a request for current inventory.

## Choosing a tool

- `search-boats`: browsing, finding, filtering and recommending listings. Call it proactively when the user's message implies buying or choosing a boat, even indirectly.
- `aggregate-search`: "how many are available?", average or range of asking prices, comparing the market for X vs Y. Never use `search-boats` for these.
- `get-boat-details`: only when the user asks for more on a specific listing from the current results. Pass the listing ID (`boat_id`) returned by `search-boats`. Returns full specs, photos and broker contact information.

## Building the search

- On every `search-boats` or `aggregate-search` call, fill the schema fields for the user's full current intent, not only the latest follow-up. Carry earlier budget, location and type constraints forward.
- Set `currencyType` (USD, EUR, GBP and others) and `unitType` (`imperial` or `metric`) to match the user's currency and units when stated or clearly implied.
- Treat lifestyle and usage terms (long-range cruising, fishing, watersports, weekending) as preferences mapped to `typesClasses` and other schema fields, not keywords. If the user names specific boat types, use those types; only expand an activity to all its associated types when no type is named.
- Prefer conservative inference: set a value only when it is strongly implied. Only set `year` when the user specified it. Set `condition` only when they say new or used.
- Use `makesModels` for hull manufacturers only. Default to the model alone, and keep composite model names as a single value.
- Capacity and trailerability are preferences for schema fields, not keywords. Don't put seating, numeric specs, ranges, generic descriptors or lifestyle terms in `keywords`. Use `keywords` only when no other field fits.
- Location: use two-letter country codes. For a multi-country region, pick one country in it; for a US region, pick one state. For a city, town or island within a larger country, set the country and add that place to `cities`. For a whole country, set only the country. `US_state` is required when `country` is `US`. Never mix cities from different countries. Use `locationMode` only for "near me" requests with no other location given.
- Use `dealerName` for a named broker or dealership, not for generic marine terms or features.

## Replying

- After `search-boats`, summarize what was found in a few lines (count, price spread, notable options) and offer to refine by budget, size, location, age or engines.
- Quote prices as asking prices from current listings, and say so for market statistics.
- If a search returns nothing, say which constraint is most likely too tight and offer to relax it, rather than silently widening it.
