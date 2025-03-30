# Coding Guideline

## Formatting and Style

- Use gofmt automatically; avoid manual formatting.
- Control statements (if, for, switch) never need parentheses (if x < 0 {} not if (x < 0)).
- Opening braces { must appear on the same line, never the next line.

## Naming Conventions

- Package names: concise, lowercase, no underscores (base64 not base_64).
- Exported identifiers start uppercase (Exported), unexported lowercase (internal).
- Avoid redundancy: bufio.Reader, not bufio.BufReader.
- Use camelCase (mixedCase) for local names, MixedCaps for exported names.
- Single-method interfaces typically named with -er suffix (Reader, Writer).
- Avoid Get prefix in getter methods: use Owner(), not GetOwner().

## Documentation

- Comments immediately precede declarations, acting as documentation.
- Document why, not what. Avoid redundant comments.
- Package-level comments should clearly describe the purpose and usage.

## Functions and Return Values

- Return multiple values for error handling: (value, err).
- Use named returns sparingly; beneficial for documentation.
- Ensure resources (files, locks) are released with defer, ensuring release regardless of how a function exits.

## Data Types and Memory Management

- new(T) allocates zeroed memory, returning pointer (\*T); make initializes slices, maps, channels (make([]int, 5)).
- Prefer slices ([]T) over arrays ([N]T) for dynamic data. Slices are references; arrays copy.
- Always check map existence with two-value form: val, ok := m["key"].

## Error Handling

- Handle errors explicitly: return error type, check every error (if err != nil).
- Error messages start lowercase, no ending punctuation ("file not found").
- Reserve panic for exceptional, unrecoverable states; use error returns for standard failures.
- Use recover() to handle panics gracefully within a controlled scope; never let panics cross API boundaries.

## Concurrency and Goroutines

- Share memory by communicating, not communicating by shared memory. Prefer channels over shared variables.
- Goroutines are lightweight; create freely, but manage lifecycles carefully.
- Channels synchronize goroutines: use buffered channels (make(chan int, 10)) to avoid blocking.
- Avoid data races: use sync.Mutex to protect shared state when necessary.
- Leverage select for multiple concurrent channel operations.

⸻

# Go Review Guidelines

Format and Style

- Ensure the code passes gofmt without diffs.
- Check brace placement and no parentheses around control structures.

Naming

- Package names short, singular, lowercase.
- Verify visibility (exported vs. unexported) correctness.
- Ensure concise, non-redundant names. Check for unnecessary Get prefixes.

Comments and Documentation

- Check exported functions/types have descriptive comments.
- Remove trivial or misleading comments; clarify complex logic.

Control Flow

- Prefer early returns to reduce nesting; avoid deep if/else chains.
- Use switch over complex if-else chains.

Functions and Error Handling

- Ensure multiple-return-value style ((value, error)) is followed consistently.
- Verify that every returned error is checked explicitly.
- Confirm proper use of defer to release resources safely.
- Inspect use of panic carefully; confirm recovery within controlled scope.

Data Types

- Verify correct use of new (zero value pointers) vs. make (slices, maps, channels).
- Check for correct slice operations (append, slicing, length vs capacity).
- Validate existence checks (\_, ok := m[key]) in map operations.

Concurrency

- Verify proper synchronization and no data races (consider running with -race).
- Ensure goroutines have defined lifecycles (avoid leaks).
- Inspect channel usage for deadlocks or incorrect close patterns.
