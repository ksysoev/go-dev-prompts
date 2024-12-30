# Go Code Generator Prompt

Generate idiomatic Go code following these guidelines:

## Project Structure

### Basic Layout
```
project/
├── cmd/                    # Main applications
│   └── app/               # Application-specific code
│       └── main.go        # Application entry point
├── internal/              # Private code
│   ├── domain/           # Business logic and types
│   ├── service/          # Business operations
│   └── repository/       # Data access layer
├── pkg/                   # Public libraries
└── api/                   # API definitions
```

## Code Style

### Package Names
```go
// Use single, lowercase words
package user

// For multi-word packages, no underscores or mixedCaps
package imageutil
```

### Variable Names
```go
// Use short names for short variable scopes
for i := 0; i < len(items); i++ {}

// Use meaningful names for larger scopes
var customerRepository Repository
var orderService Service
```

### Interface Definition
```go
// Single method interfaces use method name + 'er'
type Reader interface {
    Read(p []byte) (n int, error)
}

// Use clear, descriptive names for larger interfaces
type UserRepository interface {
    Create(ctx context.Context, user *User) error
    Get(ctx context.Context, id string) (*User, error)
    Update(ctx context.Context, user *User) error
    Delete(ctx context.Context, id string) error
}
```

## Common Patterns

### Constructor Functions
```go
// Use New + Type name for constructors
func NewUserService(repo UserRepository, logger Logger) *UserService {
    return &UserService{
        repo:   repo,
        logger: logger,
    }
}
```

### Error Handling
```go
// Define custom errors
var (
    ErrNotFound = errors.New("not found")
    ErrInvalid  = errors.New("invalid input")
)

// Return early for errors
func ProcessUser(user *User) error {
    if user == nil {
        return ErrInvalid
    }
    
    if err := validate(user); err != nil {
        return fmt.Errorf("validate user: %w", err)
    }
    
    return nil
}
```

### Context Usage
```go
// Always pass context as first parameter
func (s *Service) ProcessData(ctx context.Context, data []byte) error {
    // Use context for cancellation
    select {
    case <-ctx.Done():
        return ctx.Err()
    default:
        return s.process(data)
    }
}
```

### Configuration
```go
// Use struct for configuration
type Config struct {
    ServerAddr string
    Timeout    time.Duration
    MaxRetries int
}

// Provide sensible defaults
func DefaultConfig() Config {
    return Config{
        ServerAddr: ":8080",
        Timeout:    5 * time.Second,
        MaxRetries: 3,
    }
}
```

## Best Practices

1. Code Organization
   - Keep packages focused and cohesive
   - Use internal/ for private implementation
   - Place shared code in pkg/

2. Error Handling
   - Return errors rather than using panic
   - Wrap errors with context
   - Use custom error types for specific cases

3. Dependency Injection
   - Pass dependencies in constructors
   - Use interfaces for flexibility
   - Keep interfaces small and focused

4. Concurrency
   - Use channels for communication
   - Pass context for cancellation
   - Handle goroutine cleanup

5. Testing
   - Write tests alongside code
   - Use table-driven tests
   - Mock external dependencies

## Common Components

### HTTP Handler
```go
type Handler struct {
    service Service
    logger  Logger
}

func NewHandler(service Service, logger Logger) *Handler {
    return &Handler{
        service: service,
        logger:  logger,
    }
}

func (h *Handler) HandleGet(w http.ResponseWriter, r *http.Request) {
    ctx := r.Context()
    
    result, err := h.service.Get(ctx)
    if err != nil {
        h.logger.Error("get failed", "error", err)
        http.Error(w, "internal error", http.StatusInternalServerError)
        return
    }
    
    json.NewEncoder(w).Encode(result)
}
```

### Service Layer
```go
type Service struct {
    repo   Repository
    logger Logger
}

func NewService(repo Repository, logger Logger) *Service {
    return &Service{
        repo:   repo,
        logger: logger,
    }
}

func (s *Service) Process(ctx context.Context, input Input) (*Output, error) {
    // Validate input
    if err := input.Validate(); err != nil {
        return nil, fmt.Errorf("validate input: %w", err)
    }
    
    // Process using repository
    result, err := s.repo.Process(ctx, input)
    if err != nil {
        return nil, fmt.Errorf("process in repository: %w", err)
    }
    
    return result, nil
}
```

### Repository Layer
```go
type Repository struct {
    db     *sql.DB
    logger Logger
}

func NewRepository(db *sql.DB, logger Logger) *Repository {
    return &Repository{
        db:     db,
        logger: logger,
    }
}

func (r *Repository) Get(ctx context.Context, id string) (*Entity, error) {
    var entity Entity
    err := r.db.QueryRowContext(ctx, "SELECT * FROM entities WHERE id = $1", id).
        Scan(&entity.ID, &entity.Name)
    if err == sql.ErrNoRows {
        return nil, ErrNotFound
    }
    if err != nil {
        return nil, fmt.Errorf("query entity: %w", err)
    }
    return &entity, nil
}
```

Remember:
- Follow standard Go formatting (gofmt)
- Use consistent naming conventions
- Write clear, concise comments
- Handle errors appropriately
- Use dependency injection
- Keep functions focused and small