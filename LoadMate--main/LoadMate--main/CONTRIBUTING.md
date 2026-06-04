# Contributing to LoadMate

Thank you for your interest in contributing to LoadMate! This document provides guidelines and instructions for contributing.

## Code of Conduct

This project and everyone participating in it is governed by our [Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.

## Getting Started

1. **Fork the repository** on GitHub
2. **Clone your fork** locally
3. **Create a feature branch** from `develop`
4. **Make your changes** with clear, descriptive commits
5. **Push to your fork** and create a Pull Request

## Development Setup

### Prerequisites
- Android Studio Giraffe or later
- JDK 17+
- Android SDK 28+
- Git

### Local Setup
```bash
# Clone the repository
git clone https://github.com/KalahariCargo/LoadMate-.git
cd LoadMate-

# Setup Android environment
./scripts/setup-android-env.sh

# Build the project
./gradlew build

# Run tests
./gradlew test

# Run the app
./gradlew installDebug
```

## Coding Standards

### Kotlin Style Guide
- Follow [Kotlin official style guide](https://kotlinlang.org/docs/coding-conventions.html)
- Use 4 spaces for indentation
- Max line length: 120 characters
- Prefer val over var
- Use when instead of if/else chains
- Meaningful variable and function names

### Architecture Patterns
- **MVVM**: Model-View-ViewModel pattern
- **Clean Architecture**: Separation of concerns
- **Repository Pattern**: Data abstraction
- **Dependency Injection**: Hilt for DI

### Naming Conventions
- Classes: PascalCase
- Functions: camelCase
- Constants: UPPER_SNAKE_CASE
- Private members: prefix with underscore

### Code Organization
```kotlin
// 1. Imports
// 2. Class declaration
// 3. Companion object
// 4. Properties
// 5. Constructor
// 6. Lifecycle methods
// 7. Public methods
// 8. Private methods
// 9. Nested classes/interfaces
```

## Testing Requirements

### Test Coverage
- Minimum 80% code coverage
- 100% coverage for business logic
- Integration tests for Firebase operations
- UI tests for critical user flows

### Running Tests
```bash
# Unit tests
./gradlew test

# Integration tests
./gradlew connectedAndroidTest

# Coverage report
./gradlew testDebugUnitTest --coverage
```

### Test Examples
```kotlin
class UserRepositoryTest {
    @get:Rule
    val instantExecutorRule = InstantTaskExecutorRule()

    private val firebase = mockk<FirebaseAuth>()
    private val repository = UserRepository(firebase)

    @Test
    fun testLoginSuccess() {
        // Given
        coEvery { firebase.signIn(any(), any()) } returns flowOf(Result.success(user))

        // When
        val result = repository.login("email", "password")

        // Then
        assertEquals(Result.success(user), result)
    }
}
```

## Commit Message Guidelines

Use clear, descriptive commit messages following this format:

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Type
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code restructuring
- `perf`: Performance improvement
- `test`: Adding tests
- `chore`: Build, dependencies, etc.
- `ci`: CI/CD changes
- `security`: Security improvements

### Scope
- `auth`: Authentication related
- `marketplace`: Marketplace features
- `tracking`: Tracking related
- `payment`: Payment/Escrow related
- `ai`: AI/ML related
- `ui`: User interface
- `db`: Database/Firestore
- `api`: API related

### Examples
```
feat(marketplace): Add load search filtering

Implement advanced filtering options for load search including:
- Distance range
- Price range
- Delivery date
- Cargo type
- Vehicle requirements

Closes #123

fix(tracking): Fix GPS accuracy on Android 14

Correctly handle approximate location permission on Android 14+

docs(readme): Update setup instructions

security(auth): Add rate limiting to login endpoint
```

## Pull Request Process

### Before Submitting
1. **Run all tests**: `./gradlew test`
2. **Check code quality**: `./gradlew detekt`
3. **Run security scan**: `./gradlew dependencyCheck`
4. **Update documentation** if needed
5. **Ensure no merge conflicts** with `develop`

### PR Title Format
```
[TYPE] Description of changes

Examples:
[FEATURE] Add real-time bid notifications
[BUG FIX] Fix GPS tracking crash on Android 10
[DOCS] Update API documentation
```

### PR Description Template
```markdown
## Description
Brief description of what this PR does.

## Related Issues
Closes #123

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## How Has This Been Tested?
Describe the tests and how to reproduce.

## Screenshots (if applicable)
Add screenshots for UI changes.

## Checklist
- [ ] Code follows style guidelines
- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] No new warnings generated
- [ ] Changes don't break existing functionality
```

## Code Review Process

### Reviewers will check
- Code quality and style
- Test coverage
- Documentation completeness
- Security implications
- Performance impact
- Architecture compliance

### Feedback Loop
1. Reviewer provides feedback
2. Author makes requested changes
3. Reviewer approves or requests further changes
4. Maintainer merges PR

## Documentation

### Required Documentation
- Code comments for complex logic
- README updates for new features
- API documentation for new endpoints
- Troubleshooting guides for common issues

### Documentation Format
```kotlin
/**
 * Calculates optimal transporter for given load using AI matching.
 *
 * @param load The load to match
 * @return Transporter details with matching score (0-100)
 * @throws NetworkException if API call fails
 *
 * Algorithm:
 * 1. Filter transporters by vehicle capacity
 * 2. Score by distance, rating, availability
 * 3. Apply fraud detection
 * 4. Return top 5 matches
 */
fun findOptimalTransporter(load: Load): Transporter
```

## Reporting Issues

### Bug Reports
Include:
- Clear description of the bug
- Steps to reproduce
- Expected behavior
- Actual behavior
- Device/OS information
- Logs if available

### Feature Requests
Include:
- Clear description of feature
- Use case and benefits
- Possible implementation approach
- Any alternatives considered

## Questions?

- Check [Documentation](docs/)
- Review [Issues](../../issues)
- Ask in Pull Request discussions
- Email: support@loadmate.com

## Recognition

Contributors will be recognized in:
- CONTRIBUTORS.md file
- GitHub contributors page
- Release notes (for significant contributions)

Thank you for contributing to LoadMate! 🚀
