# AI Fire Calculator — Project Plan

## Agreed working approach
- Preserve the existing project and make changes in small, verifiable stages.
- The user should not be asked to perform technical setup or coding steps. Ask for a decision only when genuinely needed.
- Treat the supplied Oriental Insurance Company Limited fire tariff PDF (effective 01-04-2021) as the tariff source of truth. Do not silently invent or fill missing tariff rules.
- AI assists with customer conversation, discovery of missing facts, and occupancy matching. The deterministic calculation engine uses verified tariff data and explicit rules; the AI must never invent rates.
- Admin must be able to update the occupancy/rate master by uploading an Excel file.
- Build and test the website and core logic first. Connect the AI API and deploy only after the core flow is ready.

## Technology direction
- Frontend: existing HTML/CSS/JavaScript prototype, evolved without discarding the current project.
- Database: Supabase PostgreSQL free tier as the initial candidate; re-check plan limits before production.
- Conversational model: Gemini API free tier as the initial candidate; re-check rate limits and data terms before use.
- Backend: server-side API for secrets and controlled database access.
- Hosting/deployment: decide after the core app is tested.

## Stages
1. Extract and structure all 299 tariff occupancy entries from the supplied PDF, preserving row number, exact description, each sum-insured-band rate, STFI rate, and source notes. Validate extracted values against the PDF and flag ambiguity rather than guessing.
2. Design a searchable occupancy master and an AI-ready question/answer flow that asks only questions useful for distinguishing plausible tariff entries. The final question flow should be adaptive, not a fixed generic questionnaire.
3. Implement the deterministic premium calculation engine only from verified source-backed rules. Clearly identify missing rules requiring confirmation.
4. Implement real Admin Excel import, validation, preview, and safe update of the master.
5. Connect AI API through a protected backend; AI can guide fact-finding and suggest candidate occupancy entries, but must rely on the verified master.
6. Test edge cases and calculations, then configure deployment.

## Current state at planning time
- Existing index.html prototype is present in this repository and must be preserved.
- Prototype includes early questionnaire/help examples for solvent flash point and plastic calorific value, but is not yet the complete 299-entry tariff-driven application.
- Excel upload, full occupancy matching, verified calculation engine, live AI integration, and production deployment are still outstanding.

## Tariff source cautions
- The supplied ready reckoner is marked effective 01-04-2021 and contains occupancy rates and other tariff notes. Do not assume it alone resolves every policy condition or add-on calculation.
- Preserve the source's distinctions between sum-insured bands and STFI rates.
- Premium components, optional covers, discounts/loadings, taxes, and eligibility conditions must be implemented only when their rules are explicitly available and verified.
