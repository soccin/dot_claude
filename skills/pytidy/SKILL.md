---
description: Tidy and refactor Python script with clarity-first approach
allowed-tools: Read, Edit, Bash
---

# Tidy Python Script

Reformat and refactor the Python script `$1` with a **clarity-first approach** that prioritizes human comprehension over strict rule compliance:

## Core Philosophy: Clarity Over Compliance
- **Human comprehension first**: Code should tell a clear story to humans
- **Style serves clarity**: Formatting rules help readability, not hinder it
- **Simple over sophisticated**: Use the simplest construct that accomplishes the goal
- **The 30-second test**: Can a collaborator understand this code in 30 seconds?

## 1. Formatting Workflow
First attempt to use Black formatter, then fall back to manual formatting if unavailable:

```bash
# Try to format with Black first
python -m black --line-length 88 $1
```

If Black is not available, apply Black-style formatting principles manually.

## 2. Code Style: Consistent Formatting
Apply PEP 8 and Black conventions that enhance readability:
- Proper spacing around operators and after commas
- Consistent indentation (4 spaces)
- Line length limit (88 characters)
- snake_case for variable and function names
- PascalCase for class names
- UPPER_CASE for constants
- Clear function definitions with proper parameter spacing
- Remove trailing whitespace

## 3. Import Organization
Organize imports in three groups, separated by blank lines:
```python
# Standard library imports
import os
from pathlib import Path

# Third-party imports
import pandas as pd
import numpy as np

# Local application imports
from .utils import helper_function
```

- Remove unused imports
- One import per line (except multiple names from same module)
- Alphabetize within each group for consistency

## 4. Type Hints: Pragmatic Approach
Add type hints where they enhance clarity:
- **Always add** to public functions and methods
- **Add** where complexity benefits from explicit types
- **Skip** obvious cases (simple helpers, internal utilities)
- Use modern syntax for Python 3.9+ (`list[str]` not `List[str]`)

```python
# GOOD: Clear type hints for public function
def parse_data(file_path: Path, delimiter: str = ",") -> pd.DataFrame:
    """Parse data from file."""
    ...

# GOOD: Complex function benefits from hints
def merge_results(
    data: dict[str, list[float]],
    weights: dict[str, float]
) -> list[tuple[str, float]]:
    """Merge and weight results."""
    ...

# OK: Skip obvious internal helpers
def _calculate_mean(values):
    """Calculate mean - type obvious from context."""
    return sum(values) / len(values)
```

## 5. Clear Logic Flow
Structure code for obvious progression:
```python
# GOOD: Linear, readable progression
results = (
    load_data(input_file)
    .filter(lambda x: x.value > threshold)
    .transform(normalize)
    .aggregate(by_group)
)

# GOOD: Clear comprehension
valid_items = [item for item in items if item.is_valid()]

# AVOID: Complex nested comprehension
coords = [c for row in data for c in parse(row[4]) if c[0] > 0]
# Better: Use nested loops or separate steps for clarity
```

## 6. Meaningful Names Throughout
- Function names should describe what they do: `parse_peak_coordinates()` not `extract_data()`
- Variable names should be immediately clear: `lesions_file` not `input_path`
- Avoid cryptic indexing like `data[4]` - use named attributes or dict keys
- Use descriptive variable names in comprehensions when logic is complex

## 7. Documentation: Clarify, Don't Obscure
Use **Google-style docstrings for all public functions and classes**:
```python
def process_file(input_path: Path, threshold: float = 0.05) -> pd.DataFrame:
    """Process data file and filter by threshold.

    Args:
        input_path: Path to input CSV file.
        threshold: Minimum value threshold for filtering.

    Returns:
        Filtered DataFrame with processed results.

    Raises:
        FileNotFoundError: If input file doesn't exist.
        ValueError: If threshold is negative.
    """
```

**Guidelines:**
- Keep function documentation concise and purpose-focused
- Add brief comments only for complex logic
- Don't document obvious operations
- Write comments for the original author's future reference

## 8. Keep Functions Focused and Simple
- One clear purpose per function
- Minimal abstraction unless there's real benefit
- Prefer obvious implementations over "clever" ones
- Extract complex logic into named helper functions

## 9. Minimize Cognitive Load
- Avoid introducing multiple new concepts simultaneously
- Keep the main logic visible, not buried in abstractions
- Progressive complexity: start simple, add only when necessary
- Group related operations with clear section breaks only when they aid comprehension

## 10. Python Best Practices
**String Formatting:**
- Use f-strings for readability: `f"Result: {value}"` not `"Result: %s" % value`

**Resource Management:**
- Use context managers for files, connections, locks:
  ```python
  with open(file_path) as f:
      data = f.read()
  ```

**Function Arguments:**
- Avoid mutable default arguments:
  ```python
  # BAD
  def add_item(item, items=[]):
      items.append(item)
      return items

  # GOOD
  def add_item(item, items: list | None = None) -> list:
      if items is None:
          items = []
      items.append(item)
      return items
  ```

**Comprehensions:**
- Use when they enhance clarity
- Break complex comprehensions into loops or multiple steps
- Consider generator expressions for large datasets

## 11. Selective Error Handling
- Add error handling **only when failure is likely or consequences are severe**
- Use specific exceptions, not bare `except:`
- **Fail fast with clear messages**:
  ```python
  if threshold < 0:
      raise ValueError(f"Threshold must be non-negative, got {threshold}")
  ```
- Don't add defensive programming for every edge case

## 12. Anti-Patterns to Avoid
- Over-documentation that obscures simple logic
- Complex lambda functions when named functions are clearer
- Premature abstraction and generalization
- Defensive programming for every edge case
- "Clever" one-liners that require mental decoding
- Excessive abstraction layers
- Complex nested comprehensions that hurt readability

---

**Guiding Principle**: Apply these guidelines while preserving all functionality. Focus on making the code immediately comprehensible to future readers, including the original author. When in doubt, choose clarity over compliance with any single rule.

Please read the file `@$1` and apply these clarity-first guidelines, ensuring the code tells a clear story while maintaining Python best practices.
