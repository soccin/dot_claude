# Global Claude Code Configuration

## Development Environment
- User: socci
- Shell: bash

## Preferences
- Keep responses concise and direct
- Follow existing code conventions
- Run linting/typechecking after code changes
- Only commit when explicitly requested
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
- Please make sure to read my ~/.Rprofile file to get my custom function/variable definitions

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
