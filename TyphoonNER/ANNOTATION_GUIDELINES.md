# TyphoonNER Annotation Guideline (Public Summary)

This document summarizes the frozen B014 annotation schema used for the public
research release.

## General principles

1. Entity spans use character-level `start` (inclusive) and `end` (exclusive)
   offsets.
2. The substring `text[start:end]` must match the entity mention exactly.
3. Use the shortest continuous span that independently expresses the intended
   semantic role.
4. A single span should not receive multiple labels.
5. Do not absorb adjacent predicates, direction/distance expressions, units, or
   unrelated semantic roles into an entity unless they are part of the entity
   definition itself.
6. Annotation candidates must pass deterministic validation and QC before they
   are considered part of the frozen release.

## Labels

### DISASTER
Specific typhoons / tropical cyclones and hazardous weather or disaster
processes, including typhoons, tropical depressions, heavy rain, floods,
waterlogging, landslides, and related hazard processes.

### TIME
Dates, time points, periods, durations, and other temporal expressions.

### LOCATION
Administrative regions, natural geographic regions, sea areas, and concrete
affected locations. Pure movement directions are not LOCATION.

### ORGANIZATION
Real institutions, departments, agencies, established working groups, expert
groups, and emergency-response teams. Generic groups of people are not
automatically ORGANIZATION.

### AFFECTED_OBJECT
People, infrastructure, industries, transport systems, power systems, crops,
buildings, roads, and other objects affected by the disaster.

### DAMAGE
Damage outcomes and consequences, including casualties, destruction, damage,
service interruption, traffic disruption, and economic loss. The hazard itself
is DISASTER rather than DAMAGE.

### QUANTITY
Numeric or quantitative expressions, including counts, proportions, grades,
distances, wind-force levels, and approximate quantities. Include the complete
unit/measure when appropriate.

### RESPONSE
Emergency actions that have been carried out, such as evacuation, rescue,
deployment, shutdown, control, repair, restoration, and related response
operations. Future plans or general recommendations are not automatically
RESPONSE.

### WARNING
Warning signals, warning levels, explicit warning messages, and risk alerts.
Hazard names mentioned inside warning text remain DISASTER where appropriate.

## Boundary examples

The examples in this public document are synthetic and are not part of the
TyphoonNER corpus.

- `道路` → AFFECTED_OBJECT; `中断` → DAMAGE
- `发布` → RESPONSE; `台风黄色预警` → WARNING
- `某市气象局` → ORGANIZATION, rather than labeling only `气象局`
- `受某岛影响` should not be labeled as one LOCATION span; the location core is
  `某岛`

## Difficult / ambiguous cases

Malformed model output, rule conflicts, or repeatedly ambiguous annotations are
placed into a higher-risk review path. LLM output is treated as a candidate
annotation, not automatic gold.

