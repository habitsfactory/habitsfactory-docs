# Architecture

Habits Factory follows a modern API-first architecture with clear separation between the frontend and backend layers.

## Design Principles

### API-First Approach

The application is built around a RESTful API that serves as the single source of truth:

- **Independent Evolution** - Frontend and backend can be developed and deployed separately
- **Explicit Contracts** - API endpoints define clear, versionable data contracts
- **Stateless Communication** - Each request contains all necessary information
- **Testable Logic** - Business logic is isolated and easy to test

### Data Flow

```
┌─────────────┐     ┌─────────────────┐     ┌────────────────┐
│   Vue.js    │────▶│  Axios Client   │────▶│  Django REST  │
│  Frontend   │     │  HTTP Requests  │     │  Framework     │
└─────────────┘     └─────────────────┘     └────────────────┘
       ▲                                            │
       │                                            ▼
       │            ┌─────────────────┐     ┌────────────────┐
       └────────────│  JSON Response  │◀────│   PostgreSQL   │
                    │                 │     │   Database     │
                    └─────────────────┘     └────────────────┘
```

The flow ensures:

- Clear layer boundaries
- Predictable data movement
- Independent component evolution

## Backend Architecture

### Technology Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| Framework | Django | High-level Python web framework |
| API Layer | Django REST Framework | Serialization, validation, authentication |
| Database | PostgreSQL (prod) / SQLite (dev) | Data persistence |
| CORS | django-cors-headers | Cross-origin communication |

### Layer Structure

```
backend/
├── api/                  # API configuration and routing
│   ├── urls.py          # URL patterns
│   └── views.py         # API viewsets
├── habits/              # Core domain logic
│   ├── models.py        # Data models
│   ├── serializers.py   # Data transformation
│   └── views.py         # Business logic
├── analytics/           # Correlation engine
│   ├── correlations.py  # Algorithm implementations
│   └── services.py      # Analytics services
└── core/                # Project settings
    └── settings.py      # Django configuration
```

### Key Design Decisions

**Model-Serializer-View Pattern**

```python
# models.py - Data structure
class Habit(models.Model):
    name = models.CharField(max_length=100)
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    created_at = models.DateTimeField(auto_now_add=True)

# serializers.py - Data transformation
class HabitSerializer(serializers.ModelSerializer):
    class Meta:
        model = Habit
        fields = ['id', 'name', 'category', 'created_at']

# views.py - Business logic
class HabitViewSet(viewsets.ModelViewSet):
    queryset = Habit.objects.all()
    serializer_class = HabitSerializer
```

**Separation of Concerns**

- Models define data structure and database schema
- Serializers handle validation and transformation
- Views orchestrate business logic
- Services encapsulate complex operations

## Frontend Architecture

### Technology Stack

| Component | Technology | Purpose |
|-----------|------------|---------|
| Framework | Vue.js 3 | Reactive UI framework |
| Build Tool | Vite | Fast development and bundling |
| Styling | Tailwind CSS v4 | Utility-first CSS |
| HTTP Client | Axios | Promise-based API calls |
| Icons | Lucide Vue Next | Modern icon system |

### Component Structure

```
frontend/src/
├── api/                 # API client configuration
│   └── client.js       # Axios instance
├── components/          # Reusable UI components
│   ├── common/         # Generic components
│   ├── habits/         # Habit-specific components
│   └── analytics/      # Analytics visualizations
├── views/              # Page-level components
│   ├── Dashboard.vue   # Main dashboard
│   ├── Habits.vue      # Habit management
│   └── Analytics.vue   # Analytics view
├── stores/             # State management
│   └── habits.js       # Habit store
└── composables/        # Reusable logic
    └── useHabits.js    # Habit operations
```

### Composition API Pattern

Vue 3's Composition API with `<script setup>` provides:

```vue
<script setup>
import { ref, computed, onMounted } from 'vue'
import { useHabits } from '@/composables/useHabits'

const { habits, fetchHabits, createHabit } = useHabits()
const newHabitName = ref('')

const activeHabits = computed(() =>
  habits.value.filter(h => h.isActive)
)

onMounted(() => {
  fetchHabits()
})
</script>
```

Benefits:

- Better TypeScript support
- Logical code organization
- Reusable composables
- Cleaner component files

## Database Schema

### Core Entities

```
┌─────────────┐       ┌─────────────────┐
│   Category  │       │      Habit      │
├─────────────┤       ├─────────────────┤
│ id          │◀──────│ category_id     │
│ name        │       │ id              │
│ color       │       │ name            │
│ created_at  │       │ description     │
└─────────────┘       │ created_at      │
                      └─────────────────┘
                              │
                              │
                      ┌───────▼───────┐
                      │  HabitEntry   │
                      ├───────────────┤
                      │ id            │
                      │ habit_id      │
                      │ date          │
                      │ completed     │
                      │ value         │
                      └───────────────┘
```

### Relationships

- A **Category** contains many **Habits**
- A **Habit** has many **HabitEntries** (daily records)
- **HabitEntries** store completion status and optional values

## Security Considerations

### Backend Security

- CSRF protection enabled
- CORS configured for allowed origins only
- Input validation through serializers
- SQL injection prevention via ORM

### Frontend Security

- Environment variables for sensitive config
- XSS protection through Vue's template system
- Secure HTTP-only cookies for authentication

## Performance Optimizations

### Backend

- Database query optimization with `select_related` and `prefetch_related`
- Pagination for list endpoints
- Efficient correlation calculations

### Frontend

- Vite's Hot Module Replacement for fast development
- Component lazy loading
- Reactive state updates (no full page refreshes)

## Extensibility

The architecture supports easy extension:

- **New Analytics** - Add algorithms to the analytics service
- **New Features** - Create new Django apps and Vue components
- **Integrations** - Add external services through the API layer
- **Themes** - Tailwind configuration allows custom styling

See the [Roadmap](roadmap.md) for planned enhancements.
