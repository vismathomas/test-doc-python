# Contributing to test-doc-python

Thank you for your interest in contributing to test-doc-python! This document provides guidelines and instructions for contributing.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Process](#development-process)
- [Submitting Changes](#submitting-changes)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)

## Code of Conduct

This project adheres to a Code of Conduct that all contributors are expected to follow. Please read [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) before contributing.

## Getting Started

### Setting Up Your Development Environment

1. Fork the repository on GitHub
2. Clone your fork locally:
   ```bash
   git clone https://github.com/YOUR-USERNAME/test-doc-python.git
   cd test-doc-python
   ```

3. Create a virtual environment:
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

4. Install development dependencies:
   ```bash
   pip install -e ".[dev]"
   ```

5. Install pre-commit hooks:
   ```bash
   pre-commit install
   ```

### Creating a Branch

Create a new branch for your feature or bugfix:

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b bugfix/your-bugfix-name
```

## Development Process

1. **Make your changes** - Write your code following our coding standards
2. **Write tests** - Add tests for any new functionality
3. **Run tests** - Ensure all tests pass
4. **Update documentation** - Update relevant documentation
5. **Commit your changes** - Write clear, concise commit messages

### Running Tests

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=src --cov-report=html

# Run specific test file
pytest tests/test_module.py
```

### Code Quality Checks

```bash
# Format code with black
black src/ tests/

# Run flake8
flake8 src/ tests/

# Run mypy
mypy src/

# Run all pre-commit hooks
pre-commit run --all-files
```

## Submitting Changes

### Pull Request Process

1. Update the README.md with details of changes if applicable
2. Update the CHANGELOG.md with a note describing your changes
3. Ensure all tests pass and code quality checks succeed
4. Push your branch to GitHub:
   ```bash
   git push origin feature/your-feature-name
   ```
5. Open a Pull Request on GitHub

### Pull Request Guidelines

- **Title**: Use a clear and descriptive title
- **Description**: Provide a detailed description of your changes
- **Reference Issues**: Link to any related issues
- **Screenshots**: Include screenshots for UI changes
- **Tests**: Ensure your PR includes appropriate tests
- **Documentation**: Update documentation as needed

### Commit Message Guidelines

We follow conventional commit messages:

```
type(scope): subject

body

footer
```

Types:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks

Example:
```
feat(api): add new data processing endpoint

Implemented a new endpoint for processing user data with validation
and error handling.

Closes #123
```

## Coding Standards

### Python Style Guide

- Follow PEP 8 style guidelines
- Use type hints for function signatures
- Maximum line length: 88 characters (Black default)
- Use docstrings for all public modules, functions, classes, and methods

### Code Organization

- Keep functions small and focused
- Use meaningful variable and function names
- Avoid deep nesting (max 3-4 levels)
- Add comments for complex logic

### Example Code Style

```python
from typing import List, Optional


def process_data(
    items: List[str],
    filter_empty: bool = True,
    max_length: Optional[int] = None
) -> List[str]:
    """
    Process a list of string items with optional filtering.
    
    Args:
        items: List of strings to process
        filter_empty: Whether to remove empty strings
        max_length: Maximum length for items, None for no limit
    
    Returns:
        Processed list of strings
    
    Raises:
        ValueError: If items is None or invalid
    """
    if items is None:
        raise ValueError("items cannot be None")
    
    result = items.copy()
    
    if filter_empty:
        result = [item for item in result if item.strip()]
    
    if max_length is not None:
        result = [item[:max_length] for item in result]
    
    return result
```

## Testing Guidelines

### Writing Tests

- Write tests for all new features
- Maintain or improve code coverage
- Use descriptive test names
- Follow AAA pattern: Arrange, Act, Assert

### Test Structure

```python
import pytest
from mymodule import process_data


class TestProcessData:
    """Tests for process_data function."""
    
    def test_process_data_basic(self):
        """Test basic data processing."""
        # Arrange
        items = ["hello", "world"]
        
        # Act
        result = process_data(items)
        
        # Assert
        assert result == ["hello", "world"]
    
    def test_process_data_filters_empty(self):
        """Test that empty strings are filtered."""
        # Arrange
        items = ["hello", "", "world"]
        
        # Act
        result = process_data(items, filter_empty=True)
        
        # Assert
        assert result == ["hello", "world"]
    
    @pytest.mark.parametrize("items,expected", [
        (["a", "b"], ["a", "b"]),
        ([], []),
        (["test"], ["test"]),
    ])
    def test_process_data_parametrized(self, items, expected):
        """Test data processing with various inputs."""
        result = process_data(items)
        assert result == expected
```

## Documentation

### Updating Documentation

- Update relevant `.md` files in the `docs/` directory
- Update docstrings for code changes
- Add examples for new features
- Keep documentation clear and concise

### Documentation Structure

- Use Markdown format
- Include code examples
- Add diagrams where helpful
- Link to related documentation

## Questions?

If you have questions about contributing, please:
- Check existing issues and discussions
- Open a new issue with the "question" label
- Reach out to the maintainers

Thank you for contributing to test-doc-python! 🎉
