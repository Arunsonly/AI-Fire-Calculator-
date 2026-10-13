# AI Fire Calculator

First working prototype for the AI Fire Calculator project.

## Current prototype
- Mobile-friendly customer questionnaire that progressively asks about premises, business activity, products, processes, flammable materials, and storage details.
- Review step that avoids automatically confirming an occupancy when evidence is incomplete.
- Admin Rate Master preview with the proposed Excel import columns.
- No premium is calculated and no AI provider is called in this first stage.

## Planned next stages
1. Convert the full occupancy tariff in the provided reference PDF into a structured occupancy master.
2. Implement Excel upload validation, preview, versioning, and safe activation of rate changes.
3. Match questionnaire answers to the tariff occupancy descriptions with an explicit uncertain/manual-review path.
4. Implement the premium engine using the selected active rate table.
5. Add a secure backend and compare OpenAI API against locally hosted Qwen/Llama.

## Important
The reference PDF supplied for design work states an effective date of 1 April 2021. The rate master must be administratively maintainable and current rates must be verified before any real quote is issued. Do not put API keys in public frontend files.
