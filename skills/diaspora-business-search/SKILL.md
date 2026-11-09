---
name: diaspora-business-search
description: Find African and Caribbean diaspora businesses across the US, Canada and beyond — restaurants, braiders, caterers, grocers, tailors, shippers and more — using the live Ni Biashara directory.
---

Use this skill when the user asks to find, look up, or get details about a diaspora-owned business: a restaurant, braider, caterer, grocer, tailor, shipper, coffee roaster, bar, bakery, or any other African or Caribbean business in the US, Canada or beyond.

## Choosing the right tool

1. **Finding businesses by type, cuisine, service or city** → call `search_directory` with the user's keywords in `q`. Add `city`, `metro`, or `category` when the user names one. Use natural language: "ethiopian restaurant", "hair braiding", "jamaican caterer", "african grocery", "nigerian tailor".
2. **Getting details on one specific business** → call `get_business` with the listing `id` from a search result. Returns the public listing: name, category, city, metro, phone, website, social links, listing page, and claim status.
3. **Answering "which metros have the most businesses?" or coverage questions** → call `directory_facets`. Returns live listing counts by metro and category.

## How to search well

- **Lead with the service or cuisine**, not the business name, unless the user names one. "Ethiopian restaurants in Silver Spring" beats "restaurants in Silver Spring".
- **Use the user's city or metro** when given. The directory covers 131 metros; if the user's city isn't covered, `directory_facets` shows the nearest covered metro.
- **Try broader terms if a narrow search returns nothing**: "braiding" → "hair", "nigerian" → "african restaurant", "suya" → "nigerian".
- **Categories are loose**: use them as hints, not strict filters. "Catering & Events", "Restaurants & Food", "Beauty & Personal Care", "Retail & Grocery".

## Presenting results

- **Show the listing page link** (`page` or `url` field) so the user can open the full listing on nibiashara.com.
- **Include phone and website** when available — that's what most users want.
- **Mention claim status** when relevant: "This listing is unclaimed — the owner can claim it free at the listing page."
- **Never invent** phone numbers, addresses, hours, or owner names. If a field is empty, say it's not listed.
- **Don't overstate coverage**: if a search returns zero results in a city, say so and suggest browsing a nearby metro or the full directory at nibiashara.com/directory.

## Read-only boundary

The directory is read-only. If the user asks to book, message, pay, or modify a business, explain that the plugin only returns public business information and share the listing's public contact page (phone, website) as the safe fallback. Never claim to have taken an action outside the directory.

## Examples

- "Find Ethiopian restaurants in Silver Spring" → `search_directory(q="ethiopian restaurant", city="Silver Spring")`
- "Who does African hair braiding in Houston?" → `search_directory(q="hair braiding", city="Houston")`
- "Give me the phone for 5 Senses Nigerian Fusion in Dallas" → `search_directory(q="5 Senses Nigerian Fusion")` then `get_business(id)` → return phone, website, listing page
- "Which metros have the most diaspora businesses?" → `directory_facets()` → top metros by listing count
- "Book a table at Lagos Kitchen" → explain read-only, share the listing's phone and website
