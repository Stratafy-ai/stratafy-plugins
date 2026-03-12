# /stratafy-team:capture

Capture external content — an article, tweet, report, or post — and connect it to your company's strategy. Turns passive reading into strategic intelligence.

## Input

Provide one of:
- **A URL** — "capture https://example.com/article"
- **A URL with context** — "capture https://example.com/article — this is relevant to our GTM strategy"
- **Pasted content** — "capture this: [pasted text]"
- **Multiple URLs** — "capture these: [url1] [url2] [url3]"

## Process

### Step 1: Log Usage
Call `log_activity` with `activity_type: "command_usage"`, `description: "capture"`.

### Step 2: Fetch the Content

**If a URL is provided:**

Check if the content fetch tool is available (`mcp__stratafy__fetch_content`).

If available:
- For auth-walled URLs (linkedin.com, facebook.com, instagram.com): use `force_grok: true`
- For X/Twitter URLs (x.com, twitter.com): use default — Cloudflare renders these successfully
- For all other URLs: use default (Cloudflare Browser Rendering with Grok fallback)

If not available:
- Use `WebFetch` to retrieve the page content
- If WebFetch fails, ask the user to paste the content

**If content was pasted:**
- Skip fetching, proceed directly to analysis

### Step 3: Gather Strategic Context

In parallel with content fetching:
- `get_workspace_snapshot` — Company context and foundation
- `list_strategies` — Active strategies for relevance matching
- `list_key_priorities` — Current focus areas
- `list_assumptions` — Active assumptions to check against
- `get_document_tree` — To check if a "Bookmarks" section already exists

### Step 4: Analyse and Extract

From the fetched content, extract the **strategic digest** — not the raw article, but what it means for us:

- **Title** — the headline
- **Author** — who wrote/posted it
- **Source** — publication, platform, domain
- **Date** — when it was published
- **Key claims** — the 3-5 most important assertions or data points
- **Strategic relevance** — why this matters to our strategy, which strategies it connects to
- **Implications** — what we should think about or do differently

**Do NOT store the full article text.** The URL is the source of truth. Store only the strategic analysis.

### Step 5: Determine Output Types

Based on the analysis, decide what to create:

**Always create a document** with the `::source-card` MDC component for rich source attribution.

**Create a signal if:**
- The content indicates a change in the market, competitive landscape, technology, or regulatory environment
- Something new is happening that wasn't happening before
- A competitor made a move, a regulation changed, a trend emerged

**Create an insight if:**
- The content reveals a pattern or validates/challenges a hypothesis
- There's a specific "aha" that's worth preserving beyond the raw content
- A data point changes how you think about an existing strategy or assumption

### Step 6: Create Artifacts and Connect

**Order matters.** Create artifacts in this sequence, then link them together:

#### 6a. Create the document

```
create_document:
  title: "[Article/post title]"
  category: "external_capture"
  tags: [relevant strategy areas, content type, source domain]
  metadata:
    source_url: "https://..."
    source_domain: "example.com"
    author: "Author Name"
    published_date: "2026-03-12"
    fetch_method: "cloudflare" | "grok" | "pasted"
    content_type: "article" | "social_media" | "blog" | "news" | "report" | "research"
  content: |
    ::source-card{url="https://..." author="Author Name" source="Publication" date="March 12, 2026" type="article"}
    ::

    ## Why This Matters

    [2-3 sentences connecting to our strategy. Be specific about which strategies are affected and why.]

    ## Key Claims

    1. **[Claim]** — [Strategic annotation: what this means for us]
    2. **[Claim]** — [Strategic annotation]
    3. **[Claim]** — [Strategic annotation]

    ## Implications for [Company]

    [What we should think about or do differently based on this content]
```

#### 6b. Create signal (if warranted)

Create via `create_signal` with the source URL. Get the signal ID from the response.

#### 6c. Create insight (if warranted)

Create via `create_insight` with the source URL. Get the insight ID from the response.

#### 6d. Link everything together

- `link_entities` — document↔signal, document↔insight
- `link_signal_to_strategy` — signal↔strategies (with impact description)

#### 6e. Place in document tree

Place the document under a **Bookmarks** section with intelligent sub-folders:

1. Check if a root-level section named "Bookmarks" exists in the document tree (from Step 3)
2. If not, create it: `create_tree_section` with `label: "Bookmarks"`, `icon: "i-lucide-bookmark"`
3. Decide the sub-folder based on the content topic. Look at existing sub-folders first — reuse one if it fits. Examples:
   - "AI & Architecture" for AI/tech architecture content
   - "Market & Competitors" for competitive intelligence
   - "Industry News" for general industry developments
   - "Product Ideas" for feature inspiration
   - "Regulatory & Compliance" for legal/regulatory changes
4. If no existing sub-folder fits, create a new one: `create_tree_section` with a descriptive label and appropriate icon
5. Place the document: `place_document_in_tree` with `document_id`, `parent_id` (the sub-folder ID)

### Step 7: Present Results

```
✅ CAPTURED

📄 Document: "[Title]"
   Source: [author] via [publication], [date]
   📁 Bookmarks → [Sub-folder name]
   [Link to document in Stratafy]

📡 Signal: "[Signal title]" (if created)
   Type: [market/competitive/regulatory/etc.]
   Urgency: [low/medium/high/critical]
   Linked to: [Strategy name]

💡 Insight: "[Insight title]" (if created)
   [One-sentence insight]

🔗 Connected to:
   → [Strategy 1]
   → [Strategy 2 if applicable]
```

### Step 8: Prompt for More

After capturing:
- "Anything else you'd like me to capture?"
- If the content raised questions: "This challenges our assumption that [X]. Want me to flag that for review?"
- If the content suggests action: "This looks like it needs attention from [team/person]. Want me to create a signal with high urgency?"

## Multiple URL Capture

When the user provides multiple URLs:
1. Fetch all URLs in parallel
2. Analyse each independently
3. Look for **patterns across captures** — do they all point to the same trend?
4. Place all documents in the same Bookmarks sub-folder if they share a topic
5. Present a summary:

```
✅ BATCH CAPTURE — [N] items

1. "[Title 1]" — [source] → [Strategy]
2. "[Title 2]" — [source] → [Strategy]
3. "[Title 3]" — [source] → [Strategy]

📁 Filed under: Bookmarks → [Sub-folder]

🔍 PATTERN DETECTED (if applicable)
[All three articles point to the same trend: ...]
[Created signal: "..." with high urgency]
```

## Rules

- **Speed matters.** Capture should feel instant. Don't over-analyse — create the document quickly, then offer deeper analysis.
- **Never store the full article.** The URL is the source of truth. Store only the strategic digest — key claims, why it matters, and implications.
- **Always attribute.** Include the source URL, author, and date in both the `metadata` field and the `::source-card` component.
- **Always link artifacts.** Every signal and insight created from a capture MUST be linked back to the document via `link_entities`.
- **Always place in tree.** Every captured document goes under Bookmarks with an intelligent sub-folder.
- **Don't over-classify.** Not everything is a signal. Not everything is an insight. Sometimes it's just a useful document to have on file. That's fine.
- **Ask about relevance, don't assume.** If you're unsure which strategy the content relates to, ask: "This looks like it could relate to [Strategy A] or [Strategy B] — which one?"
- **Respect the user's context.** If they said "this is relevant to GTM", don't second-guess them and link it to product strategy instead.
- **Handle failure gracefully.** If you can't fetch the URL, say so immediately and ask for a paste. Don't make the user wait 30 seconds to find out it failed.
- When referencing strategies or documents, use markdown links with the `urls.detail` URL from tool responses.
