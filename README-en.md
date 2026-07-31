[English] [한국어](README.md)

# Hankookilbo MCP

An MCP (Model Context Protocol) server that provides the public homepage data of
Hankookilbo (<https://www.hankookilbo.com>), focused on **metadata**.

- Provides titles, publication dates, sections, byline information, canonical article links, and part of the article body.

## What you can do

- List today's top headlines, timely picks, most-read news, and the latest articles
- List editor-recommended articles by section, and list the available sections
- Search for related articles with a natural-language query (AI)
- Get today's horoscope and the MBTI horoscope

For the full tool list with inputs and outputs, see [`docs/tools.md`](docs/tools.md).

## Connect

**MCP server endpoint** (streamable HTTP, no authentication):

```
https://mcp.hankookilbo.com/mcp
```

- Register the URL as-is in any standard MCP client.
- For per-client setup steps, see [`docs/connect.md`](docs/connect.md).

## Output policy (no full-text redistribution)

**Provided** — metadata only:

- Article title, canonical Hankookilbo article URL, thumbnail URL
- Publication date, section, reporter/byline
- Article type (regular / exclusive / breaking), article accessibility (public / login required)
- Part of the article body — included for some tools only

**Not provided**:

- Full article text
- AI-generated answers and summaries (`search_news`)
- Horoscope content (the horoscope tools return title, publication date, and link only)
