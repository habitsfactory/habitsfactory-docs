# Features

Habits Factory provides a comprehensive set of features for tracking, analyzing, and optimizing your daily habits.

## Habit Management

### Create and Organize Habits

- **Custom Habits** - Define habits with names, descriptions, and tracking preferences
- **Categories** - Organize habits into logical groups (Health, Productivity, Learning, etc.)
- **Visual Hierarchy** - Color-coded categories for quick identification

### Daily Tracking

Track your habits with flexible options:

- **Binary Completion** - Simple yes/no tracking
- **Value-Based Tracking** - Track quantities (e.g., glasses of water, pages read)
- **Quick Entry** - Fast daily check-ins through an intuitive interface

## Analytics and Insights

### Weekly Summaries

Get a bird's-eye view of your week:

- Completion rates per habit
- Category performance breakdown
- Week-over-week comparison

### Statistics Dashboard

Comprehensive statistics including:

| Metric | Description |
|--------|-------------|
| Completion Rate | Percentage of days a habit was completed |
| Current Streak | Consecutive days of completion |
| Longest Streak | Best historical streak |
| Total Completions | All-time completion count |

### Yearly Retrospective

Annual analysis providing:

- Year-long trend visualization
- Monthly breakdown charts
- Year-over-year comparisons
- Best performing habits

## Habit Correlations

One of Habits Factory's most powerful features is automatic correlation detection between habits.

### How It Works

The system analyzes your historical data to identify relationships:

- **Positive Correlations** - Habits that tend to be completed together
- **Negative Correlations** - Habits that may compete for time/energy
- **Time-Shifted Patterns** - Habits that influence each other over time

### Correlation Strength

Correlations are ranked by strength:

| Level | Description |
|-------|-------------|
| Very Strong | Highly predictable relationship |
| Strong | Clear relationship |
| Moderate | Notable relationship |
| Weak | Slight relationship |
| Very Weak | Minimal relationship |

See [Correlation Algorithms](correlation-algorithms.md) for technical details.

## Data Export

### CSV Export

Export your habit data for external analysis:

```
date,habit_name,completed,value
2024-01-01,Morning Exercise,true,1
2024-01-01,Read 30 minutes,true,45
2024-01-01,Meditation,false,0
```

Use exported data with:

- Spreadsheet applications (Excel, Google Sheets)
- Data analysis tools (Python, R)
- Personal dashboards

## Internationalization (i18n)

Habits Factory supports multiple languages:

- **English** - Default language
- **Additional Languages** - Community contributions welcome

Language can be changed in user settings.

## User Experience

### Modern Interface

- **Clean Design** - Distraction-free interface focused on your habits
- **Visual Hierarchy** - Important information is always prominent
- **Responsive Layout** - Works on desktop and mobile devices

### Tailwind CSS v4

The UI is built with utility-first CSS providing:

- Consistent styling across components
- Dark mode support (system preference detection)
- Fast, maintainable style development

### Icon System

Lucide Vue Next icons provide:

- Modern, consistent iconography
- Accessibility compliance
- Lightweight SVG-based rendering

## Planned Features

These features are on the roadmap:

### Coming Soon

- [ ] Advanced streak logic with forgiveness rules
- [ ] Insight-driven recommendations
- [ ] Goal setting and progress tracking
- [ ] Customizable summary timeframes

### Future Enhancements

- [ ] Visual markers for habit distinction
- [ ] Category/tag filtering in graphs
- [ ] Interactive tooltips on charts
- [ ] Zoom and pan on visualizations
- [ ] Flexible tagging system
- [ ] Advanced tracking filters
- [ ] Garmin Connect integration

See the full [Roadmap](roadmap.md) for details.

## Feature Comparison

How Habits Factory compares to typical habit trackers:

| Feature | Basic Trackers | Habits Factory |
|---------|----------------|----------------|
| Simple Tracking | Yes | Yes |
| Categories | Sometimes | Yes |
| Statistics | Basic | Comprehensive |
| Correlations | No | Yes |
| Data Export | Rarely | Yes |
| Open Source | Rarely | Yes |
| Self-Hosted | No | Yes |
| Privacy | Varies | Full Control |
