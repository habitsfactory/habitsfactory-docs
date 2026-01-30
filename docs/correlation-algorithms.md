# Correlation Algorithms

Habits Factory employs three sophisticated algorithms to identify relationships between your habits. This page explains how each algorithm works and how to interpret the results.

## Overview

The correlation engine automatically analyzes your historical habit data to discover:

- Which habits tend to be completed together
- Which habits may compete for your time or energy
- Time-shifted patterns where one habit influences another

## Algorithm 1: Pearson Correlation

### What It Measures

Pearson correlation measures the **linear relationship** between two habits. It answers: "When I complete Habit A more, do I also complete Habit B more?"

### How It Works

The algorithm computes the correlation coefficient using:

$$
r = \frac{\sum_{i=1}^{n}(x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum_{i=1}^{n}(x_i - \bar{x})^2}\sqrt{\sum_{i=1}^{n}(y_i - \bar{y})^2}}
$$

Where:

- $x_i$ and $y_i$ are daily completion values for habits X and Y
- $\bar{x}$ and $\bar{y}$ are the mean completion values

### Result Range

| Value | Interpretation |
|-------|----------------|
| +1.0 | Perfect positive correlation |
| +0.5 to +1.0 | Strong positive correlation |
| 0 | No linear correlation |
| -0.5 to -1.0 | Strong negative correlation |
| -1.0 | Perfect negative correlation |

### Best For

- Detecting habits that consistently move together
- Identifying habits that may conflict
- Simple, intuitive interpretation

### Limitations

- Only detects linear relationships
- Sensitive to outliers
- Requires sufficient data points for reliability

## Algorithm 2: Spearman Rank Correlation

### What It Measures

Spearman correlation measures **monotonic relationships** - whether habits consistently increase or decrease together, even if not linearly.

### How It Works

1. Rank the completion values for each habit
2. Calculate Pearson correlation on the ranks

$$
\rho = 1 - \frac{6\sum d_i^2}{n(n^2-1)}
$$

Where:

- $d_i$ is the difference between ranks for each day
- $n$ is the number of observations

### Result Range

Same as Pearson: -1.0 to +1.0

### Best For

- Detecting non-linear but consistent relationships
- More robust to outliers than Pearson
- Works well with ordinal data

### Example

If you track "Energy Level" (1-10) and "Workout Intensity" (1-5):

- Pearson might miss the relationship if it's not perfectly linear
- Spearman will catch it if higher energy consistently means higher intensity

## Algorithm 3: Dynamic Time Warping (DTW)

### What It Measures

DTW detects **time-shifted patterns** between habits. It finds similarities even when one habit's effect appears days later.

### How It Works

DTW aligns two time series to find the optimal match:

```
Habit A: ─────╱╲─────────
Habit B: ────────╱╲──────  (2 days delayed)

DTW finds this relationship despite the time shift
```

The algorithm:

1. Creates a distance matrix between all points
2. Finds the optimal warping path
3. Returns the minimum distance

### Result Range

| Value | Interpretation |
|-------|----------------|
| 0 | Perfect match (identical patterns) |
| 0 to 0.3 | Very similar patterns |
| 0.3 to 0.6 | Moderate similarity |
| 0.6 to 1.0 | Weak similarity |
| > 1.0 | Dissimilar patterns |

!!! note
    Lower DTW values indicate stronger similarity (inverse of correlation coefficients).

### Best For

- Finding delayed cause-effect relationships
- Detecting habits that influence each other over time
- Analyzing habits with irregular patterns

### Example Use Cases

- Does morning meditation affect evening stress levels?
- Does exercise today correlate with better sleep tonight?
- Does poor sleep correlate with reduced productivity the next day?

## Correlation Strength Classification

All algorithms map to a unified strength scale:

| Classification | Pearson/Spearman | DTW |
|----------------|------------------|-----|
| Very Strong | 0.8 - 1.0 | 0 - 0.2 |
| Strong | 0.6 - 0.8 | 0.2 - 0.4 |
| Moderate | 0.4 - 0.6 | 0.4 - 0.6 |
| Weak | 0.2 - 0.4 | 0.6 - 0.8 |
| Very Weak | 0 - 0.2 | 0.8 - 1.0 |

## Interpreting Results

### Positive Correlations

When two habits show positive correlation:

- They tend to be completed together
- Completing one may make the other easier
- They might share common triggers or contexts

**Action**: Consider bundling these habits or ensuring both get attention.

### Negative Correlations

When two habits show negative correlation:

- Completing one often means skipping the other
- They may compete for time, energy, or resources
- One might satisfy the need the other addresses

**Action**: Schedule these habits at different times or on alternate days.

### Time-Shifted Correlations (DTW)

When DTW reveals a delayed pattern:

- One habit may enable or inhibit the other
- Effects accumulate over time
- There may be a cause-and-effect relationship

**Action**: Experiment with timing to optimize the beneficial effects.

## Data Requirements

For reliable correlations:

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| Days of data | 14 | 30+ |
| Completion rate | 20% | 40%+ |
| Consistency | Regular tracking | Daily tracking |

!!! warning
    Correlations with less than 14 days of overlapping data are not computed to avoid misleading results.

## Technical Implementation

### Computation Frequency

Correlations are recalculated:

- When viewing the analytics dashboard
- After significant new data is added
- Results are cached for performance

### Performance Considerations

- Calculations are performed server-side
- Large datasets use efficient numpy/scipy implementations
- Results are paginated by correlation strength

## Limitations

### Correlation vs. Causation

!!! important
    Correlation does not imply causation. Two habits may be correlated due to a third factor.

For example, "Exercise" and "Healthy Eating" might correlate because both happen on days you're feeling motivated—not because one causes the other.

### Data Quality

Results depend on:

- Consistent tracking
- Sufficient data points
- Accurate completion logging

### External Factors

The algorithms don't account for:

- Weekday vs. weekend patterns
- Seasonal variations
- Life events affecting multiple habits
