# Roast Engine — Pattern Recognition for Boss Roasts

This document defines the roast pattern library used by `/boss-roast`.

## Pattern Detection

### 1. Overengineering Detection

**Signal**: More abstractions than use cases.

Check for:
- Interface/abstract class with only one implementation
- Factory pattern for a single object type
- Config files with more options than callers
- Generic type parameters used once
- Middleware chains with one middleware

**Roast Template**: "You wrote a {pattern} for a problem that needs a {simpler_alternative}."

### 2. Scope Creep Detection

**Signal**: Changes touch more files than the ticket warrants.

Check for:
- PR touches >10 files for a "small fix"
- Unrelated refactoring mixed with feature work
- New dependencies added for tangential improvements
- Test files for code paths unrelated to the change

**Roast Template**: "The ticket said '{ticket_summary}'. You {what_actually_happened}."

### 3. Premature Optimization Detection

**Signal**: Performance work without evidence of a problem.

Check for:
- Caching without hit rate metrics
- Parallelization of small workloads
- Database indexing without query analysis
- Lazy loading of small payloads

**Roast Template**: "You optimized {what} before proving {what} is slow."

### 4. Abstraction Astronaut Detection

**Signal**: Code that is harder to understand than the problem it solves.

Check for:
- More than 3 levels of indirection for a simple operation
- Design patterns used as a goal rather than a tool
- Code that requires documentation to understand (and the documentation is also complex)

**Roast Template**: "A junior could not debug this. That is not a compliment to the code."

### 5. Dependency Inflation Detection

**Signal**: New dependencies for trivial functionality.

Check for:
- npm packages for left-pad-level operations
- Frameworks imported for a single utility function
- Libraries that add >100KB for <10 lines of saved code

**Roast Template**: "You introduced a dependency to save {N} lines of code."

## Severity Scale

- **Mild**: Good instinct, slightly overbuilt. "Ship it but simplify next time."
- **Medium**: Clear overengineering. "Revise: remove {specific_thing}."
- **Spicy**: Fundamental approach problem. "This needs a different approach entirely."

## Anti-Patterns for Roasts

Do NOT roast:
- Reasonable error handling (even if verbose)
- Tests (more tests are almost never bad)
- Documentation (unless it is wrong)
- Accessibility improvements
- Security hardening
