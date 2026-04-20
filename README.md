# katex-svelte

Svelte 5 wrapper for [KaTeX](https://katex.org) — render LaTeX math and
chemistry equations using **mhchem** (`\ce{}` notation).

[![npm](https://img.shields.io/npm/v/katex-svelte)](https://www.npmjs.com/package/katex-svelte)
[![CI](https://github.com/makeez-labs/katex-svelte/actions/workflows/ci.yml/badge.svg)](https://github.com/makeez-labs/katex-svelte/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## Install

```bash
bun add katex-svelte
```

## Setup

Import KaTeX styles once in your root layout:

```svelte
<!-- src/routes/+layout.svelte -->
<script>
  import 'katex-svelte/styles'
</script>
```

---

## Chemistry components

### `ChemEquation` — inline chemistry

```svelte
<script>
  import { ChemEquation } from 'katex-svelte'
</script>

<!-- Water -->
<p>Water is <ChemEquation formula="H2O" />.</p>

<!-- Reaction -->
<p><ChemEquation formula="CH4 + 2O2 -> CO2 + 2H2O" /></p>

<!-- Ionic -->
<p><ChemEquation formula="Fe^{2+} + 2e^- -> Fe" /></p>

<!-- Equilibrium -->
<p><ChemEquation formula="N2 + 3H2 <=> 2NH3" /></p>

<!-- With condition above arrow -->
<p><ChemEquation formula="2H2 + O2 ->[\Delta] 2H2O" /></p>
```

### `ChemBlock` — display equation

```svelte
<ChemBlock
  formula="6CO2 + 6H2O ->[\text{light}][\text{chlorophyll}] C6H12O6 + 6O2"
  label="Photosynthesis"
  number={1}
/>
```

### `ChemAuto` — auto-render mixed text

```svelte
<ChemAuto
  text="Water (\ce{H2O}) has a molar mass of $18\text{ g/mol}$.
        The pH is defined as $$pH = -\log_{10}[\ce{H+}]$$"
/>
```

### `ChemNotation` — labelled notation card

```svelte
<ChemNotation
  formula="H2SO4"
  name="Sulfuric acid"
  desc="Strong diprotic acid — fully dissociates in water"
  type="formula"
/>

<ChemNotation
  formula="Fe2O3 + 3CO -> 2Fe + 3CO2"
  name="Reduction of iron(III) oxide"
  desc="Used in blast furnace extraction of iron"
  type="reaction"
/>
```

---

## Math components

```svelte
<!-- Inline math -->
<p>Energy: <LatexMath formula="E = mc^2" /></p>

<!-- Block math -->
<LatexBlock
  formula="\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}"
  label="Gaussian integral"
/>
```

---

## Chemistry utilities

```typescript
import {
  buildReaction,
  searchFormulas,
  searchReactions,
  getElement,
  toCe,
  COMMON_FORMULAS,
  COMMON_REACTIONS,
  ELEMENTS,
} from 'katex-svelte'

// Build reaction strings
buildReaction(['N2', '3H2'], ['2NH3'], '<=>') // → "N2 + 3H2 <=> 2NH3"

// Search by name
searchFormulas('acid')    // → [{ name, formula }, ...]
searchReactions('haber')  // → [{ name, equation }, ...]

// Element data
getElement('Fe')          // → { symbol: 'Fe', name: 'Iron', number: 26, ... }

// Common formulas
COMMON_FORMULAS['water']  // → 'H2O'
```

---

## mhchem `\ce{}` notation quick reference

| Input                                     | Renders as                  |
|-------------------------------------------|-----------------------------|
| `H2O`                                     | H₂O                         |
| `H2SO4`                                   | H₂SO₄                       |
| `CH4 + 2O2 -> CO2 + 2H2O`                | CH₄ + 2O₂ → CO₂ + 2H₂O     |
| `N2 + 3H2 <=> 2NH3`                       | N₂ + 3H₂ ⇌ 2NH₃             |
| `Fe^{2+} + 2e^- -> Fe`                    | Fe²⁺ + 2e⁻ → Fe             |
| `2H2 + O2 ->[\Delta] 2H2O`               | With heat condition          |
| `CaCO3 ->[\text{heat}] CaO + CO2`        | With text condition          |
| `Cl^{-}_{(aq)}`                           | Cl⁻(aq)                     |

---

## KaTeX quick reference

| Input                          | Renders as        |
|--------------------------------|-------------------|
| `E = mc^2`                     | E = mc²           |
| `\frac{a}{b}`                  | a/b (fraction)    |
| `\sqrt{x}`                     | √x                |
| `x_{n}`                        | xₙ (subscript)    |
| `x^{2}`                        | x² (superscript)  |
| `\int_{0}^{\infty}`            | ∫₀^∞              |
| `\sum_{n=1}^{\infty}`          | Σ from n=1 to ∞   |
| `\text{rate} = k[\text{A}]^m`  | text in math mode |

---

## Docs

[katex-svelte-docs.vercel.app](https://katex-svelte-docs.vercel.app)

## License

MIT © [Makeez Labs](https://github.com/makeez-labs)
