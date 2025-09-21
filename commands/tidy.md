---
description: Tidy and refactor R script according to tidyverse style guide
allowed-tools: Read, Edit, WebFetch
---

# Tidy R Script

Reformat and refactor the R script `$1` to conform to the tidyverse style guide:

1. **Code Style**: Apply tidyverse formatting conventions including:
   - Proper spacing around operators and after commas
   - Consistent indentation (2 spaces)
   - Line length limits (80 characters)
   - Snake_case for variable and function names
   - Clear function definitions with proper parameter spacing

2. **Documentation**: Add comprehensive comments that:
   - Explain the purpose of each major code section
   - Document function parameters and return values
   - Provide context for complex operations
   - Follow roxygen2-style comments where appropriate; especially for functions
   - Are written for the original author's future reference

3. **Code Structure**: Improve organization by:
   - Grouping related operations
   - Adding clear section breaks
   - Ensuring logical flow from data loading to output

4. **Tidyverse Principles**: Apply tidyverse best practices:
   - Use pipe operators (`|>`) for readable data transformations but remember its limitations and fail back to `%>%` when needed.
   - Prefer tidyverse functions over base R equivalents where appropriate
   - Use consistent naming conventions
   - Implement clear, functional programming patterns

5. **Compatibility**: Ensure no conflicts with functions defined in `~/.Rprofile`:
   - Avoid redefining: `cc()`, `len()`, `DATE()`, `write.xls()`, `getSDIR()`, `get_script_dir()`, `halt()`, `appendList()`, `suppress()`
   - Check for any custom functions in the ndsLib environment

6. **General Style Rules**: Clean things up by:
   - Remove any trailing white space

7. **Error Handling**
  - Use `cat()` for clear, user-friendly error messages with proper spacing
  - Use `quit(status = 1)` for fatal errors instead of `stop()`
  - Format: `cat("\nERROR: Clear description\n\n")` followed by `quit(status = 1)`
  - For severe errors where it is not clear what is happening or a state that should never be seen, use `rlang::abort()` with concise messages


Please read the file `@$1` and apply these tidyverse style guidelines while preserving all functionality. Focus on readability and maintainability for future reference by the original author.