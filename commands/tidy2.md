---
description: Tidy and refactor R script with clarity-first approach
allowed-tools: Read, Edit, WebFetch
---

# Tidy R Script

Reformat and refactor the R script `$1` with a **clarity-first approach** that prioritizes human comprehension over strict rule compliance:

## Core Philosophy: Clarity Over Compliance
- **Human comprehension first**: Code should tell a clear story to humans
- **Style serves clarity**: Formatting rules help readability, not hinder it  
- **Simple over sophisticated**: Use the simplest construct that accomplishes the goal
- **The 30-second test**: Can a collaborator understand this code in 30 seconds?

## 1. Code Style: Consistent Formatting
Apply tidyverse formatting conventions that enhance readability:
- Proper spacing around operators and after commas
- Consistent indentation (2 spaces)
- Line length limits (80 characters)
- Snake_case for variable and function names
- **However**, variables that are in all caps (eg GLOBAL) have external scope and should *NOT* be changed in any way
- Clear function definitions with proper parameter spacing
- Remove any trailing white space

## 2. Clear Logic Flow
Structure code for obvious progression:
```r
# GOOD: Linear, obvious progression
data |>
  read_tsv() |>
  clean_names() |>
  filter(condition) |>
  mutate(new_col = transformation) |>
  select(final_columns)

# AVOID: Complex nested operations that require mental parsing
data %>% mutate(coords = map(.[[4]], complex_parser))
```

## 3. Meaningful Names Throughout
- Function names should describe what they do: `parse_peak_strings()` not `extract_coords()`
- Variable names should be immediately clear: `lesions_file` not `input_path`
- Avoid cryptic references like `.[[4]]` - use named columns

## 4. Documentation: Clarify, Don't Obscure
- Use standard **roxygen2 documentation for all functions** (@param, @return)
- Keep function documentation **concise and purpose-focused**
- Add **brief comments only for complex logic**
- Don't document obvious operations
- Write comments for the original author's future reference

## 5. Keep Functions Focused and Simple
- One clear purpose per function
- Minimal abstraction unless there's real benefit
- Prefer obvious implementations over "clever" ones
- Place utility functions near where they're used

## 6. Minimize Cognitive Load
- Avoid introducing multiple new concepts simultaneously
- Keep the main logic visible, not buried in abstractions
- Progressive complexity: start simple, add only when necessary
- Group related operations with clear section breaks only when they aid comprehension

## 7. Tidyverse Usage: Simple and Clear
- Use **`|>` (native pipe) over `%>%`** for R compatibility, but fall back to `%>%` when needed for advanced functionality (magrittr-specific functionality needed):
  ```r
  # Needs %>% - this won't work with |>
  y = x %>% split(.$group)
  ```
- Prefer standard dplyr verbs (`select()`, `filter()`, `mutate()`) over base R equivalents for consistency
- **Avoid overly functional approaches** (excessive `map()`, `purrr`) when simple solutions exist
- Prefer tidyverse functions over base R equivalents where it enhances clarity

## 8. Selective Error Handling
- Add error handling **only when failure is likely or consequences are severe**
- Use simple checks rather than comprehensive validation for internal functions
- **Fail fast with clear messages** using:
  - `cat("\nERROR: Clear description\n\n")` followed by `quit(status = 1)` for user-facing errors
  - `rlang::abort()` with concise messages for severe/unexpected errors
- Don't add defensive programming for every edge case

## 9. Compatibility Requirements
Ensure no conflicts with functions defined in `~/.Rprofile`:
- Avoid redefining: `cc()`, `len()`, `DATE()`, `write.xls()`, `getSDIR()`, `get_script_dir()`, `halt()`, `appendList()`, `suppress()`
- Check for any custom functions in the ndsLib environment

## 10. Anti-Patterns to Avoid
- Over-documentation that obscures simple logic
- Complex functional programming when procedural is clearer  
- Premature abstraction and generalization
- Defensive programming for every edge case
- "Clever" code that requires mental decoding
- Excessive abstraction layers

---

**Guiding Principle**: Apply these guidelines while preserving all functionality. Focus on making the code immediately comprehensible to future readers, including the original author. When in doubt, choose clarity over compliance with any single rule.

Please read the file `@$1` and apply these clarity-first guidelines, ensuring the code tells a clear story while maintaining tidyverse best practices.
