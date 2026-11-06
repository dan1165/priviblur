# Product

<!-- impeccable:product-schema 1 -->

## Platform

web

## Users

Two audiences whose needs future work must both serve:

- **Anonymous Tumblr readers.** People who want to browse blogs, tags, search, and
  explore without a Tumblr account, without being tracked, and on slow connections
  or privacy-hardened browsers. Their job is to read and follow Tumblr content the
  way they would on Tumblr itself, with no login wall and no surveillance.
- **Instance operators.** People who deploy, host, and upgrade Priviblur for
  themselves or a community. Their job is a repeatable Docker or manual deployment,
  a configurable instance, and an easy path to stay current with upstream.

## Product Purpose

Priviblur is an alternative frontend and proxy for Tumblr. It requests Tumblr on the
visitor's behalf, so content can be read without an account and without exposing the
visitor to Tumblr's tracking. It works without JavaScript, remains lightweight, and
aims to reproduce the browsing experience of modern Tumblr rather than a bare
read-only mirror. Success means a reader forgets they are on an alternative frontend,
and an operator can run a current, capable instance with little effort.

## Positioning

A privacy-preserving Tumblr proxy that does not trade away the modern browsing
experience: no account, no tracking, no JavaScript requirement, and no separate
"lite" mode — blog pages, posts, tags, search, explore, notes, polls, and settings all
behave like a contemporary product. Forks and modified instances are explicitly part
of the model, under the AGPLv3 and a public instance list.

## Operating Context

- Readers arrive from links to Tumblr blogs, tags, posts, and search results, often on
  mobile, and often on connections where heavy JavaScript is costly.
- Each deployment is an independent instance; there is no official instance and no
  central account system. Preferences are stored in a cookie (theme, language,
  expand-truncated-posts) rather than a login.
- Operators deploy via the published Docker image or manual Python setup, configure a
  TOML file, optionally enable Redis caching, and choose a language and theme default.
- Translation is community-run through Weblate; instance maintainers are expected to
  keep deployments within a month of the latest commit or release and to disclose
  modifications.

## Capabilities and Constraints

- Tumblr blog timelines, individual posts, blog search, tag pages, search, and explore
  (today, trending), plus post notes (likes, reblogs, replies) and RSS feeds.
- Tumblr NPF posts rendered through `npf_renderer`; media is proxied through the
  instance. Polls fetch results through the instance API.
- Server-rendered Jinja pages with progressive enhancement: core browsing works with
  JavaScript disabled; JS adds poll results, expansion, and settings conveniences.
- Stack is fixed by the existing codebase: Python, Sanic, Jinja2, aiohttp, optional
  Redis. Templates and CSS are first-party; Inter is self-hosted.
- Localization: 11 supported locales, English as fallback, all UI strings through
  gettext/Weblate; adding a language must stay a content change, not a code fork.
- Deployment constraints: Docker image and compose files, TOML configuration,
  cookie-based preferences with versioned compatibility, AGPLv3 licensing and source
  disclosure for modified instances.
- Privacy constraints: no accounts, no third-party trackers or analytics, no
  referrer leakage, media and API traffic proxied rather than exposed to Tumblr.

## Brand Commitments

- The name **Priviblur** and its light/dark/auto logo variants are fixed.
- Voice is plain, friendly, and non-technical for readers; instance docs speak
  directly to operators. Copy avoids surveillance fear-mongering and stays factual.
- The product presents itself as a modern frontend, not a retro or minimal "text
  mode" tool. Visual work should match that ambition.
- AGPLv3 and the Weblate translation community are permanent commitments.

## Evidence on Hand

- `screenshots/example.png` — current visual reference of a rendered timeline.
- `instances.md` — live public instance list including a Tor onion service.
- `locales/` — real translations for 11 locales.
- `config.example.toml` — the operator-facing configuration surface.
- No user testimonials, usage metrics, benchmarks, or press coverage exist; future
  work must not invent them.

## Product Principles

1. **Privacy is architectural, not a setting.** Proxying, no account, and no tracking
   are the default state; features must not reintroduce exposure.
2. **Modern experience is a hard requirement.** "Works without JavaScript" never
   justifies a degraded look or feel; parity with contemporary Tumblr browsing is the
   bar, and this is the claim future work must never weaken.
3. **The reader's page comes first.** Reading speed, scanability, and content fidelity
   outrank decoration, novelty, or operator-facing cleverness.
4. **Operators are first-class.** Configuration, deployment, upgrades, and modified
   forks stay documented and practical.
5. **Open and translatable by default.** New user-facing strings ship through gettext,
   and the AGPLv3 and instance-list model stay intact.

## Accessibility & Inclusion

- Core content and navigation must remain usable without JavaScript.
- Preferences expose theme (auto/light/dark) and language; auto follows the OS color
  scheme. These are the only accessibility-adjacent settings confirmed today.
- No formal accessibility standard has been declared; treat WCAG 2.2 AA as the working
  floor for contrast, focus, semantics, and keyboard use, and label any stricter
  requirement as an open decision rather than a confirmed product fact.
