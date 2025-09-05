# AI Usage Documentation

## Tools Used
- **ChatGPT (OpenAI)**: for generating README/RESULTS structure, circuit explanations, and SOC derivation.
- **Perplexity AI**: used for quick queries on CubeSat EPS assumptions.
- **Falstad Simulator**: official tool for building & testing the EPS.

---

## Prompts / Query Themes
1. "How to model CubeSat EPS in CircuitJS?"
2. "How to simulate sun/eclipse with PWL or pulse source?"
3. "How to calculate SOC from capacitor?"
4. "Help in formatting README and RESULTS for GitHub challenge."

---

## Adaptation of AI Outputs
- Initial AI suggestion used wrong capacitor values (µF scale).  
  → Corrected to **3000 µF** after checking CubeSat battery analogies.  
- AI proposed PWL current source (not visible in Falstad).  
  → Replaced with **pulse voltage source**.  
- Waveform misinterpretations were clarified by **manual scope checks**.

---



