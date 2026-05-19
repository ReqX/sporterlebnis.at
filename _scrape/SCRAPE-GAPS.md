# Scrape Gaps — sporterlebnis.at

Pages and URL patterns discovered during scraping but intentionally or unavoidably excluded from the content archive.

---

## 1. Dead Links (Broken on Live Site)

These URLs are referenced from internal links on sporterlebnis.at but return HTTP 403 or 404 on the live server. Content was never retrieved.

| URL | HTTP Status | Referenced From |
|-----|-------------|-----------------|
| `/klettersteige` | 403 | `/sportaktivitaten` (activity listing) |
| `/rafting-wildwasserarena` | 403/404 | `/rafting-canyoning` (overview page) |
| `/wildwasserarena-moelltal` | 403/404 | Multiple rafting/canyoning pages |

**Impact:** These are real activity pages that existed on the Drupal 7 site but are currently broken. Content may have been removed or unpublished by the site owner. If the content still exists in the Drupal backend, it should be recovered before migration.

**Action for rebuild:** Either recreate this content from source material (brochures, owner knowledge) or confirm with Marko/Martina that these activities are no longer offered and the links should not be carried forward.

---

## 2. URL Aliases (Redirects to Already-Scraped Pages)

These clean URLs redirect or alias to pages already in the archive. No unique content — listed here so redirect mapping can be configured in the new site.

| Alias URL | Canonical (Already Scraped) |
|-----------|----------------------------|
| `/chalet` | `/familien-chalet-hutte-karnten` |
| `/motorikpark-kaernten-moelltal` | `/motorikpark-r-kaernten-moelltal` |
| `/home2` | `/` (homepage, paginated news at `/home2?page=N`) |

---

## 3. Drupal Node IDs (/node/N)

Drupal 7 assigns numeric node IDs that serve as canonical/shortlink URLs. These are **aliases of already-scraped clean URL pages**. Listed here for redirect mapping during migration.

Only `/node/12` was scraped (maps to a page already in the archive). The remaining 46+ node references are internal Drupal paths that resolve to clean URLs already captured.

| Node URL | Likely Maps To | Notes |
|----------|---------------|-------|
| `/node/1` | Unknown | Drupal internal |
| `/node/2` | Unknown | Drupal internal |
| `/node/6` | `/camping` | Based on Drupal node ordering |
| `/node/7` | `/rafting-canyoning` | Based on Drupal node ordering |
| `/node/8` | `/bar-restaurant` | Based on Drupal node ordering |
| `/node/12` | `/schulsport` | Only node page scraped |
| `/node/{3-5,9-11,13-47}` | Various | All resolve to already-scraped clean URLs |

**Impact:** No content loss. Node URLs should be mapped to the corresponding clean URL via 301 redirects in the new site's routing.

**Action for rebuild:** If Drupal database access is available, extract the exact `node/N → path-alias` mapping table (`url_alias` table) for precise redirect rules. Otherwise, configure catch-all `/node/:id` → 404 or manual redirect map.

---

## 4. Category Pages (/kategorie/)

Drupal 7 taxonomy listing pages — auto-generated index pages that list articles tagged with each category. **No unique content** beyond links to already-scraped article pages.

| Category URL | Articles Listed |
|-------------|----------------|
| `/kategorie/camping` | Camping-related articles |
| `/kategorie/restaurant-bar` | Restaurant/Bar articles |
| `/kategorie/sport` | All sport articles |
| `/kategorie/sport/canyoning` | Canyoning articles |
| `/kategorie/sport/hochseilgarten` | Hochseilgarten articles |
| `/kategorie/sport/klettern-klettersteige` | Climbing articles |
| `/kategorie/sport/rafting` | Rafting articles |
| `/kategorie/sport/riverbug` | Riverbug articles |
| `/kategorie/sport/wandern-bergsteigen` | Hiking articles |

**Impact:** No unique content. These are Drupal Views-generated listing pages.

**Action for rebuild:** If category/tag browsing is desired in the new site, implement it natively in the new CMS/framework. Do not attempt to migrate these Drupal-generated pages.

---

## 5. Tag Pages (/tags/)

Drupal 7 taxonomy tag listing pages — same as categories above, auto-generated lists of articles by tag. **No unique content.**

| Tag URL | Topic |
|---------|-------|
| `/tags/bar` | Bar |
| `/tags/camping` | Camping |
| `/tags/canyoning` | Canyoning |
| `/tags/catering` | Catering |
| `/tags/chalet` | Chalet |
| `/tags/driving-range` | Driving Range |
| `/tags/familie` | Family |
| `/tags/golf` | Golf |
| `/tags/grillen` | Grilling |
| `/tags/hochseilgarten` | Hochseilgarten |
| `/tags/kajak` | Kayak |
| `/tags/kinder` | Children |
| `/tags/klettern` | Climbing |
| `/tags/klettersteig` | Via Ferrata |
| `/tags/mini-raft` | Mini Raft |
| `/tags/mobilheim` | Mobile Home |
| `/tags/moelltal` | Mölltal |
| `/tags/motorikpark` | Motorikpark |
| `/tags/obervellach` | Obervellach |
| `/tags/rafting` | Rafting |
| `/tags/restaurant` | Restaurant |
| `/tags/riverbug` | Riverbug |
| `/tags/schulsport` | School Sport |
| `/tags/sommer` | Summer |
| `/tags/sport` | Sport |
| `/tags/team` | Team |
| `/tags/tiny-house` | Tiny House |
| `/tags/wandern` | Hiking |
| `/tags/wohnwagen` | Caravan |

**Impact:** No unique content.

**Action for rebuild:** If tag-based navigation is desired, implement natively. The tag taxonomy above can serve as the basis for a tag system in the new site.

---

## 6. Non-Scrapable Pages

| URL | Reason |
|-----|--------|
| `/user/login` | Drupal admin login — requires authentication, no public content |

---

## Summary

| Gap Category | Count | Content Loss? | Migration Action |
|---|---|---|---|
| Dead links (403/404) | 3 | ⚠️ Possibly — content may exist in Drupal backend | Recover from backend or confirm removed |
| URL aliases/redirects | 3 | ❌ No — already scraped via canonical URL | Configure 301 redirects |
| Node ID aliases | ~47 | ❌ No — already scraped via clean URLs | Configure 301 redirects or catch-all |
| Category listing pages | 9 | ❌ No — auto-generated, no unique content | Rebuild natively if needed |
| Tag listing pages | 29 | ❌ No — auto-generated, no unique content | Rebuild natively if needed |
| Auth pages | 1 | ❌ No — admin-only | N/A |

**Net unique content gaps: 3 dead-linked pages** (content may still exist in Drupal backend).

---

*Documented: May 17, 2026*
*Source audit: explorer session exp-1*
