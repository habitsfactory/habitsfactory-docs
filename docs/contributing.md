# Contributing

Thank you for your interest in contributing to Habits Factory! This guide will help you get started.

## Ways to Contribute

### Code Contributions

- Bug fixes
- New features
- Performance improvements
- Test coverage

### Non-Code Contributions

- Documentation improvements
- Bug reports
- Feature suggestions
- Architectural discussions
- Translations

## Getting Started

### 1. Fork the Repository

Fork [habitsfactory-app](https://github.com/habitsfactory/habitsfactory-app) to your GitHub account.

### 2. Clone Your Fork

```bash
git clone https://github.com/YOUR_USERNAME/habitsfactory-app.git
cd habitsfactory-app
```

### 3. Set Up Development Environment

Follow the [Getting Started](getting-started.md) guide to set up:

- Python virtual environment
- Django backend
- Node.js and Vue.js frontend

### 4. Create a Branch

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/bug-description
```

## Development Workflow

### Before You Start

1. **Check existing issues** - Someone may already be working on it
2. **Open an issue first** - For significant changes, discuss before implementing
3. **Understand the architecture** - Read the [Architecture](architecture.md) documentation

### Code Style

#### Python (Backend)

Follow PEP 8 with these specifics:

```python
# Use descriptive names
def calculate_habit_streak(habit_id: int, end_date: date) -> int:
    """Calculate the current streak for a habit."""
    pass

# Type hints encouraged
def get_correlations(
    habits: list[Habit],
    min_strength: str = "moderate"
) -> list[Correlation]:
    pass

# Docstrings for public functions
class HabitViewSet(viewsets.ModelViewSet):
    """
    ViewSet for managing habits.

    Supports CRUD operations and statistics retrieval.
    """
    pass
```

#### JavaScript/Vue (Frontend)

Follow the Vue.js style guide:

```vue
<script setup>
// Composition API with script setup
import { ref, computed, onMounted } from 'vue'

// Props definition
const props = defineProps({
  habitId: {
    type: Number,
    required: true
  }
})

// Emits definition
const emit = defineEmits(['update', 'delete'])

// Reactive state
const isLoading = ref(false)

// Computed properties
const isComplete = computed(() => /* ... */)
</script>

<template>
  <!-- Single root element -->
  <div class="habit-card">
    <!-- kebab-case for component names in templates -->
    <habit-header :title="habit.name" />
  </div>
</template>
```

### Testing

#### Backend Tests

```bash
cd backend
python manage.py test
```

Write tests for:

- Model methods
- API endpoints
- Business logic

```python
class HabitModelTest(TestCase):
    def test_streak_calculation(self):
        habit = Habit.objects.create(name="Test")
        # Add entries...
        self.assertEqual(habit.current_streak, 5)
```

#### Frontend Tests

```bash
cd frontend
npm run test
```

Write tests for:

- Component rendering
- User interactions
- API integration

### Commit Messages

Follow conventional commits:

```
feat: add weekly summary export
fix: correct streak calculation for skipped days
docs: update API reference with new endpoints
refactor: simplify correlation algorithm
test: add integration tests for habit creation
```

Format:

```
<type>: <description>

[optional body]

[optional footer]
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

## Pull Request Process

### 1. Update Your Branch

```bash
git fetch upstream
git rebase upstream/main
```

### 2. Run Tests

Ensure all tests pass:

```bash
# Backend
cd backend
python manage.py test

# Frontend
cd frontend
npm run test
npm run lint
```

### 3. Create Pull Request

Push your branch and create a PR:

```bash
git push origin feature/your-feature-name
```

Then open a PR on GitHub with:

- Clear title describing the change
- Description of what and why
- Link to related issues
- Screenshots for UI changes

### 4. Code Review

- Address review feedback
- Keep the PR focused (one feature/fix per PR)
- Respond to comments promptly

### PR Checklist

- [ ] Tests added/updated
- [ ] Documentation updated
- [ ] Follows code style guidelines
- [ ] Commits are clean and descriptive
- [ ] PR description is complete

## Issue Guidelines

### Bug Reports

Include:

1. **Description** - What happened?
2. **Expected behavior** - What should happen?
3. **Steps to reproduce** - How can we see it?
4. **Environment** - OS, browser, versions
5. **Screenshots** - If applicable

### Feature Requests

Include:

1. **Use case** - Why do you need this?
2. **Proposed solution** - How might it work?
3. **Alternatives considered** - Other approaches?
4. **Additional context** - Mockups, examples

## Architecture Decisions

For significant changes, follow this process:

1. **Open a Discussion** - GitHub Discussions for early feedback
2. **Write a Proposal** - Document the approach
3. **Gather Feedback** - Allow time for community input
4. **Implement** - Once consensus is reached

## Community Guidelines

### Be Respectful

- Constructive feedback only
- Assume good intentions
- Welcome newcomers

### Be Collaborative

- Share knowledge
- Help others learn
- Celebrate contributions

### Be Patient

- Maintainers are volunteers
- Reviews take time
- Large changes need discussion

## Recognition

Contributors are recognized in:

- GitHub contributors list
- Release notes for significant contributions
- Special thanks in documentation

## Questions?

- Open a [GitHub Discussion](https://github.com/habitsfactory/habitsfactory-app/discussions)
- Check existing issues and discussions
- Review the documentation

Thank you for contributing to Habits Factory!
