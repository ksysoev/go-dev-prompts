# Go Unit Test Generator Prompt

Generate comprehensive Go unit tests using testify framework and mockery for mocks. Follow these guidelines:

## Core Testing Structure

### Basic Test
```go
import (
    "testing"
    "github.com/stretchr/testify/assert"
    "github.com/stretchr/testify/require"
)

func TestFunction(t *testing.T) {
    // Arrange
    assert := assert.New(t)
    require := require.New(t)
    
    // Act
    result, err := Function()

    // Assert
    require.NoError(err)
    assert.Equal(expected, result)
}
```

### Table Test
```go
func TestFunction(t *testing.T) {
    tests := []struct {
        name    string
        input   string
        want    string
        wantErr error
    }{
        {"valid case", "input", "expected", nil},
        {"error case", "invalid", "", ErrInvalid},
    }

    for _, tt := range tests {
        t.Run(tt.name, func(t *testing.T) {
            got, err := Function(tt.input)
            if tt.wantErr != nil {
                assert.ErrorIs(t, err, tt.wantErr)
                return
            }
            assert.NoError(t, err)
            assert.Equal(t, tt.want, got)
        })
    }
}
```

## Best Practices

1. Assertions
   - Use assert for normal checks
   - Use require for critical checks that should stop test
   - Use mock.Anything for irrelevant arguments

2. Mocking
   - Use mockery to generate mocks
   - Define interfaces for dependencies
   - Verify all expectations with AssertExpectations

3. Test Organization
   - Use table-driven tests for multiple cases
   - Use testify/suite for related tests
   - Keep tests next to the code they test

Remember:
- Write tests before implementation (TDD)
- Test behavior, not implementation
- Keep tests simple and focused
