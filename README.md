# Fuzzy Inference System (Mamdani) for Epidemiological Risk Analysis

Implementation of a fuzzy inference system by Mamdani’s method, using basic Python libraries without ready libraries of fuzzy logic (such as `scikit-fuzzy`). The system is applied to an epidemiological crisis scenarios, demonstrating how fuzzy logic can translate uncertain variables (effective reproduction number, saturation of the hospital infrastructure) into interpretable risk recommendations and to guide intervention.

## Motivation

Public health decisions rarely deal with 100% accurate data - "transmission is high" or "hospitals are near the limit" are naturally vague claims. Fuzzy logic models exactly this kind of uncertainty, allowing:

- Combine continuous variables (e.g., effective reproduction number, hospital occupation) in linguistic terms (`low`, `high`, `critical`...);
- Apply a rule base of the type `if ... and ... then ...` written in language close to human;
- Obtain a numerical output (e.g., epidemiological risk) and a linguistic classification, useful for both dashboards and decision reports.

## How the System is Modeled

This work integrates the SIR model to the fuzzy logic of Mamdani, aiming to broaden the interpretation of epidemiological scenarios. 

### SIR Model
This modeldivides the population according to the following functions/stage in relation to the disease: susceptible, infected and removed. Its system of equations is described by
$$
\begin{cases}
    \dfrac{ \partial S}{ \partial t} = - \beta SI   \\[10pt]
    \dfrac{ \partial I}{ \partial t} = ( \beta S -  \gamma) I   \\[10pt]
    \dfrac{ \partial R}{ \partial t} =  \gamma I
\end{cases}
$$

where $\beta$ is the transmission rate and $\gamma$ is the recovery rate. From the second equation, the **Effective Reproduction Number**, $R_t = \frac{\beta S}{\gamma}$, is defined, allowing it to be rewritten as:

$$
\begin{cases}
    \dfrac{ \partial S}{ \partial t} = - \beta SI   \\[10pt]
    \dfrac{ \partial I}{ \partial t} = (R_t - 1) \gamma I \\[10pt]
    \dfrac{ \partial R}{ \partial t} =  \gamma I
\end{cases}
$$

Thus, only with the second equation is it possible to evaluate the disease growth trend through the values of $R_t$. This term will be used as a fuzzy system input variable along with another variable related to the saturation of hospital infrastructure, both being represented qualitatively by adjectives and will be quantitatively mapped by relevance functions. In other words, they will be transformed into fuzzy numbers.

The fuzzy inference system based on fuzzy rules of mamdani and simulation tools will be used to evaluate the response of the system to the change of its activation degrees, culminating in an output variable that measures the epidemiological risk of the system.

##  Notebook Structure and Tools
1. Fuzzy Inference System - Mamdani’s method
    - Libraries
    - Fuzzy Sets
    - Linguistic term
    - Logical Operators
    - Fuzzyfication
    - Fuzzy Rules
    - Mamdani Inference System
2. Simulations using MamdaniFIS
    - Inference Mesh
    - Inference Surface
    - Heatmap
    - Output Classification
    - Scenario Simulation
      - Scenario Plotting
    - Probability of Controlling the Epidemic
3. Definitions and Execution (main block)

### Running

The prerequisites for compilation are `Python 3.9+`, `numpy`, `matplotlib` and `scipy`. Given these requirements, open `inferencia_mamdani.ipynb` in Jupyter/Colab and run the cells in order - the main block (section 3) defines the variables, the rules and generates all visualizations automatically.

## Credits and Code Provenance

This project combines material from two distinct origins and it is important that this distinction is clear:

1. Section 1
   - **Provided by Prof. Dr. Moiseis dos Santos Cecconello** (Federal University of Mato Grosso - UFMT), in the mini-course *"Fuzzy Sets and Artificial Intelligence: Fundamentals and Applications"*, taught at the VII Brazilian Congress of Fuzzy Systems (CBSF).
2. Sections 2-3 
   - **Developed by Luisa de Melo Carneiro** (State University of Campinas - UNICAMP) as adaptation and extension of the above material.

**This repository is published for educational purposes**, with due credit to the author of the original material. The license stated below covers exclusively the extensions listed in the second and third section of the document - **not** the fuzzy inference engine itself, whose rights remain with the original author. If Prof. Dr. Moiseis Cecconello or the CBSF organization have any objections to how the material has been reproduced here, please open an *issue* in this repository or contact me directly - the content will be promptly adjusted or removed as requested.

### 📄 License

The extensions of this repository (section 2 onwards) are made available. The fuzzy inference engine (section 1) **is not covered by this license** - its rights belong to the original author; see section <ins>Credits and Code Provenance</ins> and look for the original source of the mini-course and quote the author directly, rather than quoting this repository.
