# Fuzzy Inference System (Mamdani) for Epidemiological Risk Analysis

Implementation of a fuzzy inference system by Mamdani’s method, using only `numpy` , `matplotlib` and `cipy.integrate` - without ready libraries of fuzzy logic (such as `scikit-fuzzy`). The system is applied to an epidemiological decision-making scenario, demonstrating how fuzzy logic can translate uncertain variables (effective reproduction number, saturation of the hospital infrastructure) into interpretable risk recommendations and to guide intervention.

> ⚠️ **This repository contains material from third parties.** See the section [Credits and Code Provenance] before reusing, redistributing or quoting this project.

---

## 📌 Motivation

Public health decisions rarely deal with 100% accurate data - "transmission is high" or "hospitals are near the limit" are naturally vague claims. Fuzzy logic models exactly this kind of uncertainty, allowing:

- Combine continuous variables (e.g., actual reproduction number, hospital occupation) in linguistic terms (`low`, `high`, `critical`...);
- Apply a rule base of the type `IF ... AND ... THEN ...` written in language close to human;
- Obtain a numerical output (epidemiological risk) and a linguistic classification, useful for both dashboards and decision reports.

## 🙏 Credits and Code Provenance

This project combines material from two distinct origins, and it is important that this distinction is clear:

| Notebook section | Content | Authorship |
|---|---|
| 1 to 7 (libraries, relevance functions, `Term`, `Condition`, `Variable`, `Rule`, `MamdaniFIS`) | Generic fuzzy inference engine | **Provided by Prof. Dr. Moiseis Cecconello** (Federal University of Mato Grosso - UFMT), in the mini-course *"Fuzzy Sets and Artificial Intelligence: Fundamentals and Applications"*, taught at the **VII Brazilian Congress of Fuzzy Systems (CBSF)** |
| 8 em diante (`compute_inference_grid`, `plot_inference_surface`, `plot_inference_heatmap`, `classify_output`, `simulate_scenarios`, `plot_scenarios`, `probabilidade_controle`, `plot_probabilidade_controle`) e a definição das variáveis/regras do cenário epidemiológico | Extensão aplicada: simulation of epidemiological scenarios, visualizations (surface, heat map, comparison of scenarios) and control probability model | Developed by **[his name]** as adaptation and extension of the above material |

**This repository is published for educational purposes**, with due credit to the author of the original material. The license stated below covers exclusively the extensions listed in the second row of the table - **not** the fuzzy inference engine itself, whose rights remain with the original author. If Prof. Dr. Moiseis Cecconello or the CBSF organization have any objections to how the material has been reproduced here, please open an *issue* in this repository or contact us directly - the content will be promptly adjusted or removed as requested.

If you intend to reuse the part of the fuzzy engine (sections 1-7) in another project, look for the original source of the mini-course and quote the author directly, rather than quoting this repository.

## ✨ Features

- **Generic fuzzy motor** (original course material):
  - Relevance functions: triangular, trapezoidal, gaussian, sigmoid and generalized bell (`trimf`, `trapmf`, `gaussmf`, `sigmf`, `gbellmf`);
  - Linguistic variables with multiple terms (`Variable`);
  - Rule composition with `AND` (`&`) and `OR` (`|`) via operator overload (`Condition`);
  - Complete inference engine (`MamdaniFIS`): fuzzification activation of the rules implication (minimum)   aggregation (maximum)   defuzzification by centroid (via `scipy.integrate.quad`).
- **Visualizations and simulations** (extension of this repository):
  - 3D inference surface and 2D heat map, both in the `viridis` palette;
  - Simulation of named epidemiological scenarios (e.g., *Hospital Collapse*, *Mass Vaccination*), with automatic classification in the most relevant linguistic term and a comparative graph between them;
  - Probability model of control of the epidemic over time, considering interventions (vaccination, lockdown) and adverse events (hospital collapse, emergence of a new variant), with colored background by risk range and indication of events on the axis of time.

## 🧠 How the fuzzy system is modeled

| Paper | Variable | Universe | Linguistic terms |
|---|---|--|--|--|
| Entry | Susceptibility (Rt) | `[-1.0, 1.0]` | low, threshold, high |
| Entrance | Hospital infrastructure saturation | `[0.6, 1.1]` | normal, alert, critical, extreme |
| Exit | Epidemiological Risk | `[-1.0, 1.0]` | my_low, low, moderate, high, my_high |

The rule base crosses the terms of the two inputs (e.g.: `IF Susceptibility is high AND Saturation is critical THEN Risk is very high`), covering the input space.

## 📂 Notebook structure

`
1. Libraries
2. Relevance functions (trimf, trapmf, gaussmf, sigmf, gbellmf)
3. Linguistic term (Term)   material of the
4. Logical Operators (Condition)   minicurso
5. Fuzzyfication (Variable)   (Prof. Cecconello)
6. Fuzzy rules (Rule)
7. Mamdani Inference System (MamdaniFIS)
8. Simulations using MamdaniFIS
   Inference mesh (compute_inference_grid)
   Inference surface (plot_inference_surface)
   Heat map (plot_inference_heatmap)   extension
   Output classification (classify_output)   (this repository)
   Scenario simulation (simulate_scenarios)
   Scenario plotting (plot_scenarios)
   Probability of controlling the epidemic
      (probabilida_controle / plot_probabilida_controle)
9. Definition of variables, rules and execution (main block)

## 🚀 How to run

### Requirements

- Python 3.9+
- `numpy`, `matplotlib`, `scipy`

`s bash
pip install -r requirements.txt
`

### Running

Open `inferencia_mamdani.ipynb` in Jupyter/Colab and run the cells in order - the main block (section 9) defines the variables, the rules and generates all visualizations automatically.

## 👩‍🏫 Author

- **Fuzzy inference engine (sections 1-7):** Prof. Dr. Moiseis Cecconello (UFMT), mini-course "Fuzzy Sets and Artificial Intelligence: Fundamentals and Applications", 7th Brazilian Congress of Fuzzy Systems.
- **Epidemiological extension (section 8 onwards):** Luisa de Melo Carneiro (UNICAMP), as work applied from the above material.

## 📄 License

The extensions of this repository (section 8 onwards) are made available under license [define here, e.g. MIT]. The fuzzy inference engine (sections 1-7) **is not covered by this license** - its rights belong to the original author; see section [Credits and Code Provenance](#-credits-e-source-of-code) before reusing it.
