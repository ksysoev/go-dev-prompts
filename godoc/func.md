# GoDoc Documentation Generator Prompt

Generate comprehensive GoDoc documentation for Go code following these guidelines:

## Function Documentation

### Basic Structure
```go
// FunctionName [action verb] [what it does] [additional context if needed].
// It [details about behavior, requirements, or important notes].
//
// Parameters:
//   - param1: description if not obvious from name/type
//   - param2: description if not obvious from name/type
//
// Returns:
//   - type1: what this return value represents
//   - error: conditions that trigger errors
//
```

### Key Points
1. Start with an action verb (creates, performs, validates, etc.)
2. Be concise but complete
3. Document only non-obvious parameters
4. Always document error conditions

### Common Documentation Patterns

Simple Function:
```go
// Sum adds two integers and returns their sum.
func Sum(a, b int) int
```

Complex Function:
```go
// ProcessData validates and transforms the input data according to the specified options.
// It applies each transformation sequentially and stops on the first error encountered.
//
// Parameters:
//   - data: raw input to be processed
//   - opts: configuration options that control the transformation
//
// Returns:
//   - processed data in the requested format
//   - error if validation fails or any transformation step errors
//
func ProcessData(data []byte, opts *Options) ([]byte, error)
```

Error Handling:
```go
// Divide performs division of two numbers.
// It returns an error if the denominator is zero.
//
// Returns:
//   - float64: the quotient of numerator/denominator
//   - error: if denominator is 0 or if division results in overflow
func Divide(numerator, denominator float64) (float64, error)
```

## Package Documentation

Place package documentation in a separate `doc.go` file:

```go
// Package calculator provides basic arithmetic operations
// and advanced mathematical calculations.
//
package calculator
```

## Interface Documentation

```go
// Reader is the interface that wraps the basic Read method.
//
// Read reads up to len(p) bytes into p. It returns the number of bytes
// read (0 <= n <= len(p)) and any error encountered.
type Reader interface {
    Read(p []byte) (n int, err error)
}
```

## Constants and Variables

```go
// Maximum number of retry attempts for network operations
const MaxRetries = 3

// DefaultTimeout is the default duration before operations timeout
var DefaultTimeout = 30 * time.Second
```

## Best Practices

1. Use Present Tense
   - Good: "ProcessData validates..."
   - Bad: "ProcessData will validate..."

2. Be Specific About Types
   - Good: "takes a slice of bytes"
   - Bad: "takes data"

3. Document Concurrency
   - Mention if function is safe for concurrent use
   - Document any synchronization requirements

4. Document Panics
   - If function can panic, document the conditions

5. Performance Implications
   - Document if function is computationally expensive
   - Mention memory usage for large inputs

Remember:
- Documentation is for users of your code
- Focus on behavior, not implementation
- Be concise but complete
- Document failure modes and edge cases
