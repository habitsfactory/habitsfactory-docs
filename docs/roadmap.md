# Roadmap

This page outlines the planned features and enhancements for Habits Factory. The project is under active development, and priorities may shift based on community feedback.

## Current Status

Habits Factory is currently in **active development**. Core functionality is implemented:

- [x] Habit creation and management
- [x] Daily tracking interface
- [x] Category organization
- [x] Basic statistics
- [x] Correlation analysis
- [x] Weekly summaries
- [x] Data export (CSV)

## Short Term

Features planned for the next releases.

### Advanced Streak Logic

Enhanced streak tracking with configurable rules:

- **Forgiveness Rules** - Allow occasional misses without breaking streaks
- **Flexible Schedules** - Define which days count (weekdays only, specific days, etc.)
- **Streak Milestones** - Celebrate achievements at key milestones

### Insight-Driven Recommendations

AI-powered suggestions based on your data:

- "You're more likely to exercise on days you meditate"
- "Your reading habit drops on Fridays - consider scheduling shorter sessions"
- Pattern detection for optimal habit scheduling

### Goal Setting and Tracking

Define and track habit-related goals:

- Daily/weekly/monthly targets
- Progress visualization
- Achievement notifications
- Historical goal performance

### Customizable Summary Timeframes

Flexible date ranges for summaries:

- Custom date ranges
- Quarterly views
- Rolling 30/60/90 day windows
- Comparison between periods

## Medium Term

Features planned for future development cycles.

### Enhanced Visualizations

Improved charts and graphs:

| Feature | Description |
|---------|-------------|
| Visual Markers | Icons and colors for habit distinction |
| Category Filtering | Filter graphs by category or tag |
| Interactive Tooltips | Detailed information on hover |
| Zoom and Pan | Navigate large date ranges easily |
| Heatmaps | GitHub-style contribution graphs |

### Flexible Tagging System

Move beyond categories with a tag-based organization:

- Multiple tags per habit
- Tag-based filtering
- Smart tag suggestions
- Tag analytics

### Advanced Tracking Filters

Powerful filtering for the tracking interface:

- Filter by completion status
- Filter by streak status
- Multi-category selection
- Search by habit name
- Custom filter presets

### Docker Deployment

Simplified deployment with Docker:

```bash
# Planned one-command setup
docker-compose up
```

Goals:

- Single-command local development
- Production-ready configuration
- Environment parity
- Easy updates

## Long Term

Features being considered for future releases.

### Integrations

#### Garmin Connect

Sync fitness data from Garmin devices:

- Import activity data as habit entries
- Correlate Garmin metrics with habits
- Automatic tracking for fitness habits

#### Calendar Integration

Sync with calendar applications:

- Google Calendar
- Apple Calendar
- Outlook
- Schedule habits as calendar events

#### Health Apps

Connect with health platforms:

- Apple Health
- Google Fit
- Import sleep, activity, and wellness data

### Mobile Applications

Native mobile experience:

- iOS application
- Android application
- Offline support
- Push notifications
- Widgets

### Social Features

Optional community features:

- Share achievements
- Accountability partners
- Habit challenges
- Progress sharing

### Advanced Analytics

Machine learning-powered insights:

- Predictive completion likelihood
- Optimal scheduling recommendations
- Burnout detection
- Habit recommendation engine

## Community Wishlist

Features requested by the community (not yet scheduled):

- [ ] Recurring habits with complex schedules
- [ ] Habit templates library
- [ ] Public API for third-party apps
- [ ] Webhook support
- [ ] Multi-device sync
- [ ] Encrypted data storage
- [ ] Self-hosted authentication providers

## Contributing to the Roadmap

We welcome input on the roadmap! Here's how to participate:

### Suggest Features

1. Check existing [GitHub Issues](https://github.com/habitsfactory/habitsfactory-app/issues)
2. Open a new issue with the "feature request" label
3. Describe the use case and expected behavior

### Vote on Features

- React with a thumbs up on issues you want prioritized
- Comment with additional use cases or implementation ideas

### Discuss Architecture

For significant changes:

1. Open a discussion on GitHub Discussions
2. Propose your approach
3. Gather community feedback

### Implement Features

See the [Contributing Guide](contributing.md) for details on:

- Setting up the development environment
- Code style guidelines
- Pull request process

## Release Schedule

There is no fixed release schedule. Releases happen when:

- Significant features are complete
- Critical bugs are fixed
- Breaking changes need coordination

Follow the [GitHub repository](https://github.com/habitsfactory/habitsfactory-app) for release announcements.
