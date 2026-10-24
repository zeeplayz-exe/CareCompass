# CareCompass

**A multilingual symptom guide that tells people what to do next.**
Built for the **CodeTheCure** hackathon on Devpost.

> CareCompass gives general health information only. It does not diagnose, and it is not a substitute for a doctor. In an emergency, call your local emergency number (103 / 112 in Uzbekistan, 112 in the EU, 911 in the US).

**Live demo:** https://claude.ai/artifact/HWbnmbwAU9JGM6oU61JX4e

---

## The problem

When something hurts, many people don't know whether to rest at home, buy a medicine, see a doctor, or go to the emergency room. Search results are confusing, and often frightening. Language barriers make it worse.

## What CareCompass does

1. **Welcome screen** explains how the app works.
2. **Accept screen** confirms the user understands it is not a diagnosis.
3. **Choose a condition** from 30 common conditions, from simple (cold, headache) to serious (high blood pressure, diabetes, possible heart problem, stroke warning). Users can filter by level or search by condition or symptom.
4. **Short questionnaire** about severity, duration, age group, specific symptoms and risk factors (pregnancy, medicine allergies, ulcer/kidney/liver disease, other medicines).
5. **Personal plan** with a clear verdict:
   - **Urgent:** an emergency warning sign was selected
   - **See a doctor soon**
   - **Self-care is likely fine**

   plus what to do, medicines to ask a pharmacist about, when to see a doctor, and emergency signs.

## Features

- 30 conditions with symptoms, self-care steps, medicine options, and doctor triggers
- Emergency signs override home-care advice and send users to urgent care
- Extra caution for children, people over 65, pregnancy, allergies and other risk factors
- **SOS button** on every screen with emergency numbers and first-aid steps
- **10 languages:** English, Uzbek, Russian, Spanish, French, German, Arabic (right-to-left), Chinese, Hindi, Turkish
- Light and dark mode, with a text-size toggle
- Recent checks stored on the user's device
- Copy summary, print or save, and links to nearby pharmacies and hospitals (Google Maps)
- Responsive design for phone and desktop

## How the languages work

- The main interface (welcome, buttons, verdicts, SOS window, disclaimer) is translated from built-in dictionaries.
- Condition content (names, symptoms, steps, medicines) is translated at runtime using the `sample` capability of the claude.ai artifact runtime. Results are cached in the browser.
- If that capability is unavailable (for example, when the file is hosted elsewhere or permission is declined), the interface still switches language and the condition content stays in English.
- Translations are generated, not reviewed by a medical translator. Have a native speaker or professional check them before real-world use.

## Run it locally

No build step and no dependencies.

```bash
# Option 1: open the file directly
open carecompass.html

# Option 2: serve it
python3 -m http.server 8000
# then visit http://localhost:8000/carecompass.html
```

You can also host it for free on GitHub Pages or Netlify Drop.

## Project structure

```
carecompass.html   # the whole app: HTML, CSS and JavaScript
README.md
```

Where to edit inside `carecompass.html`:

| What | Where |
| --- | --- |
| Conditions and medical content | the `C` array in the script |
| Interface translations | the `EN` and `TR` objects |
| Colors | CSS variables under `:root[data-theme]` |
| Result logic (urgent / doctor / self-care) | the `res()` function |

Each condition entry has: `n` name, `l` level (1 simple, 2 moderate, 3 serious), `s` symptoms (a leading `!` marks an emergency sign), `c` self-care steps, `m` medicines, `d` reasons to see a doctor.

## Safety design

- No diagnosis and no medicine doses. Users are told to follow the label and ask a pharmacist.
- Any selected emergency sign shows an urgent-care message and hides home-care advice.
- Prescription-only conditions (high blood pressure, diabetes, asthma) never suggest self-starting medicines.
- Data stays in the user's browser. No accounts, no tracking.

## Limitations and next steps

- Rule-based guidance, not a clinical tool, and it has not been reviewed by medical professionals
- Condition content is available in English first; other languages depend on runtime translation
- Planned: clinician review of all content, pre-translated content in more languages, medicine reminder timer, BMI and temperature tools, local emergency numbers by country

## Built with

HTML, CSS, vanilla JavaScript. Fonts: Inter and Source Serif 4.

## License

MIT. Change this if your team prefers another license.

## Team

Add your team members here.
