# BP Energy Indicators
date: 2026-02-25

These indicators are part of [Systema Globalis](https://github.com/open-numbers/ddf--gapminder--systema_globalis).

* The indicators are updated to the latest 2025 BP release.

### Source datasets

* [`open-numbers/ddf--bp--energy`](https://github.com/open-numbers/ddf--bp--energy):
  - `coal_consumption_exajoules`
  - `electricity_generation_twh`
  - `gas_production_exajoules`
  - `gas_proved_reserves_history`
  - `oil_consumption_tonnes`
  - `oil_production_tonnes`
  - `oil_proved_reserves_history`
  - Country metadata
* [`open-numbers/ddf--gapminder--population`](https://github.com/open-numbers/ddf--gapminder--population):
  - `population` (used to derive per-person/per-capita indicators)
* [`open-numbers/ddf--open_numbers`](https://github.com/open-numbers/ddf--open_numbers) and [`open-numbers/ddf--gapminder--ontology`](https://github.com/open-numbers/ddf--gapminder--ontology):
  - Concepts and geo entities used for harmonization/metadata

### ETL computations (summary)

* Harmonizes country identifiers by translating BP country names via Gapminder synonyms.
* Renames keys to DDF conventions (`year -> time`, `country -> geo`, `population -> population_total`).
* Converts and scales source measures into totals:
  - `coal_consumption_total = coal_consumption_exajoules * 1e9 / 41.868`
  - `electricity_generation_total = electricity_generation_twh * 1e9`
  - `natural_gas_production_total = gas_production_exajoules * 1e9 / 41.868`
  - `oil_consumption_total = oil_consumption_tonnes * 1e6`
  - `oil_production_total = oil_production_tonnes * 1e6`
  - `oil_proved_reserves_total = oil_proved_reserves_history * 136400000`
  - `natural_gas_proved_reserves_total = gas_proved_reserves_history * 900000000`
* Merges population and computes per-person/per-capita indicators by dividing totals by `population_total`.
