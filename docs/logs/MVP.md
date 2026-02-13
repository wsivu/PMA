# MVP Overview for Personal Media Aggregator

## Goal
Create a functional prototype that allows a user to search for movies, series, and anime across multiple sources, select the best source, and stream it with basic playback controls and user personalization.

## Development Phases

### Phase 1 – Core Functionality (4‑6 weeks)
1. **Project scaffolding** – initialise backend (FastAPI + SQLAlchemy) and frontend (Next.js + TypeScript). 
2. **User authentication** – simple JWT based sign‑up / login.
3. **TMDB integration** – fetch metadata (title, poster, description, etc.).
4. **Basic media search** – keyword search with autocomplete and filtering (genre, year, rating, type).
5. **Basic player** – embed Video.js for direct file/URL playback.

### Phase 2 – Source Aggregation (4‑6 weeks)
1. **Source parser framework** – modular system to query external APIs / scrape sites.
2. **Torrent support** – integrate WebTorrent for magnet‑link streaming.
3. **Quality & source selection** – evaluate sources (quality, speed, availability, subtitles) and automatically pick the best.
4. **Playback progress** – store and restore watching position per user.

### Phase 3 – Enhanced User Experience (4 weeks)
1. **Watch history** – persist per‑user viewing history.
2. **Bookmarks & playlists** – allow users to save titles and create custom playlists.
3. **Personalisation** – basic recommendation logic based on watch history and ratings.
4. **Recommendations** – expose an endpoint that returns personalized suggestions.

### Phase 4 – optimisation & scaling (2‑3 weeks)
1. **Caching** – Redis cache for frequent API calls and search results.
2. **Performance tweaks** – lazy‑load UI components, virtualised lists, CDN for static assets.
3. **PWA functionality** – offline support, installable web app.
4. **Documentation** – update README, API docs (Swagger/OpenAPI), ADRs and deployment scripts.

## Summary
By the end of Phase 4 the MVP will provide:
- Unified browsing of movies/series/anime.
- Automatic source discovery and best‑quality streaming.
- Persistent user data (auth, history, bookmarks, progress).
- A production‑ready codebase with caching, scalability considerations and documentation.

---
*Generated from the project specification in `docs/TZ.md`.*