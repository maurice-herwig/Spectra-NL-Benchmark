# Spectra–Natural-Language Requirements Dataset

This dataset pairs formal specifications written in the Spectra language with
natural-language requirements describing the intended system behavior.

## Dataset structure

- `spec/public/` contains 123 publicly sourced Spectra specifications.
- `spec/handcrafted/` contains 12 independently authored reference specifications.
- `nl-requirements/public/` contains the natural-language requirements paired with the public specifications.
- `nl-requirements/handcrafted/` contains the natural-language requirements paired with the handcrafted specifications.
- `metadata/public.jsonl` and `metadata/handcrafted.jsonl` contain one record per specification.

The same identifier is used for a specification, its natural-language
requirement, and its metadata record. Public identifiers use the form
`public_001` through `public_123`; handcrafted identifiers use the form
`task_01` through `task_12`.

Each metadata record contains the identifier, the original repository, the
topic, and the structural complexity score.

## Structural complexity score

For a specification `s`, the structural complexity score is calculated as:

```text
C(s) = number of environment variables
     + number of system variables
     + number of assumptions
     + number of guarantees
```

The score is a coarse measure of specification size and structure. It does not
account for the internal complexity of individual temporal formulas.
