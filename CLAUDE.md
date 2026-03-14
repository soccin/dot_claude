# Global Claude Code Configuration

## Development Environment
- User: socci
- Shell: bash

## Preferences
- Keep responses concise and direct
- Follow existing code conventions
- Run linting/typechecking after code changes
- Only commit when explicitly requested
- Never chain bash commands with `&&`, `;`, or `|` — always run each as a separate tool call. Chaining bypasses `allowed-tools` pattern matching in slash command frontmatter.
- DO NOT USE emoji in commit messages
- Do NOT use emoji in any commit, release notes, docs, comments, ...
- Do **NOT** use emoji every!!
- 
## Project Notes
- Git workflow: work on branches, merge to master
- I like short names for branchs; e.g., feat/updates-01
- Follow standard commit message format: 50 char subject, 72 char body lines
- DO NOT USE EMOJI IN COMMIT MESSAGES
- Create draft commit messages in /tmp and let me edit them first
- STOP USING EMOJI

## R Information
- Always read `~/.Rprofile` for custom function/variable definitions:
  `cc()`, `len()`, `DATE()`, `halt()`, `getSDIR()`, `suppress()`, etc.

### Coding style — ALWAYS follow these rules for R code

**Tidyverse first**
- Always prefer tidyverse idioms over base R equivalents
- Use `dplyr` verbs (`mutate`, `filter`, `select`, `summarize`, etc.)
  instead of `[`, `[[`, `$` subsetting chains or `apply` family
- Use `purrr` (`map`, `map_dfr`, etc.) instead of `lapply`/`sapply`
- Use `tibble`/`read_csv` instead of `data.frame`/`read.csv`
- Write data transformations as pipelines, not nested calls
- Prefer the base pipe `|>` over `%>%` in all new code
- Use `%>%` only when necessary for lambda-style tricks that `|>`
  cannot express, e.g. `%>% split(.$col)` (since `dplyr::group_split`
  is broken for this use case)

**String operations — stringr + glue, never base R**
- Use `stringr` functions exclusively for string manipulation:
  - `str_detect` not `grepl`
  - `str_subset` not `grep(..., value=TRUE)`
  - `str_remove`/`str_remove_all` not `sub`/`gsub`
  - `str_replace`/`str_replace_all` not `sub`/`gsub`
  - `str_extract` not `regmatches`/`regexpr`
  - `str_c` not `paste`/`paste0` (for general concatenation)
  - `str_glue` or `glue::glue` not `paste0` for building strings
    with interpolated values (especially regex patterns)
  - `str_trim`/`str_squish` not `trimws`
  - `str_split_1`/`str_split` not `strsplit`
- Use `glue("{var}")` syntax for constructing regex patterns and
  any string that embeds a variable — never `paste0("^", x, ":")`

**Misc**
- Prefer `readr` (`read_csv`, `read_tsv`) over base `read.csv`/`read.table`;
  always pass `show_col_types=FALSE`
- Use `fs` package for file system operations (`dir_ls`, `file_exists`, etc.)
  instead of `list.files`, `file.exists`
- Use `forcats` for factor manipulation instead of base `factor()`/`levels<-`

## Python Documentation Standards

### Docstring Format
- Use Google-style docstrings for all functions, classes, and methods
- Include type hints on all function signatures
- Document Args, Returns, and Raises sections as needed
- Keep docstrings concise but complete

### Template Format
```python
def function_name(param1: str, param2: Optional[int] = None) -> str:
    """One line summary.

    Optional longer description.

    Args:
        param1: Description of first parameter.
        param2: Description of optional parameter.

    Returns:
        Description of return value.

    Raises:
        ExceptionType: When this exception is raised.
    """
```

### Example
```python
def query(prompt: str, options: ClaudeCodeOptions = None) -> AsyncIterator[str]:
    """Send a query to Claude Code and stream the response.
    
    Args:
        prompt: The input prompt to send to Claude.
        options: Optional configuration for the query.
        
    Returns:
        An async iterator yielding response chunks.
        
    Raises:
        ClaudeCodeError: If the query fails.
    """
- Stop adding trailing white space when you edit R code
