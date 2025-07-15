# Advanced Flame Graph Analyzer

## Overview

The Advanced Flame Graph Analyzer is a web-based tool for visualizing and analyzing event-based logs from car simulations, drone flights, or similar time-based event data. It provides interactive flame graph visualizations, event filtering, search, statistics, pattern analysis, and export options.

## Features

- **Interactive Flame Graphs:** Visualize event durations and overlaps on a timeline.
- **Category Filtering:** Toggle event categories (e.g., maneuver, control, sensor) to focus your analysis.
- **Search:** Quickly find events by name, ID, or category.
- **Detailed Tooltips:** Hover over bars for event details and overlaps.
- **Analysis Tabs:**
  - **Statistics:** Event counts, durations, overlaps, and category breakdowns.
  - **Patterns:** Common event sequences and critical paths.
  - **Performance:** Longest events, concurrency, and timeline gaps.
- **Import/Export:**
  - Import JSON event logs.
  - Export data as JSON, CSV, or SVG image.
- **Responsive UI:** Works on desktop and tablets.

## Getting Started

1. **Open `flame-graph-light-v4.html` in your browser.**
2. **Import your event log:**
   - Click the **Import** button or drag and drop a `.json` file onto the page.
   - Use the sample data to explore features if you don't have your own log.
3. **Explore the visualization:**
   - Use category chips to filter events.
   - Search for specific events.
   - Zoom in/out or fit the timeline.
   - Click events or labels to select and analyze them.
4. **Export your analysis:**
   - Click **Export** to download the current data as JSON, CSV, or SVG.

## Supported Import JSON Format

The analyzer expects a JSON file containing an array of event objects. Each event represents a timestamped occurrence (start or end) of an event. Events with the same `event_id` are paired as start/end to form a span.

### Example

```json
[
  { "timestamp": 0.0, "event_id": "drone1-takeoff-init", "display_name": "Drone 1 – Takeoff Initialized", "category": "maneuver" },
  { "timestamp": 0.3, "event_id": "drone1-takeoff-init", "display_name": "Drone 1 – Takeoff Init Complete", "category": "maneuver" }
]
```

### Field Descriptions

| Field         | Type    | Description                                                                 |
|-------------- |---------|-----------------------------------------------------------------------------|
| `timestamp`   | number  | Time of the event in **seconds** (can be float, e.g., 1.23).                 |
| `event_id`    | string  | Unique identifier for the event type. Used to pair start/end events.         |
| `display_name`| string  | Human-readable name for the event (shown in UI and tooltips).                |
| `category`    | string  | Event category. Supported: `maneuver`, `control`, `sensor`, `navigation`, `safety`, `infrastructure`. |

#### Notes
- Each event span is defined by two events with the same `event_id`: the first is the start, the second is the end.
- Events must be ordered by timestamp for best results.
- Unpaired events will be logged as warnings and ignored in the visualization.

## Export Formats

- **JSON:** Full event data with metadata and statistics.
- **CSV:** Tabular data for spreadsheets (event_id, display_name, category, start_time, end_time, duration).
- **SVG:** Vector image of the current flame graph.

## Keyboard Shortcuts

- `Ctrl/Cmd + F` – Focus search
- `Ctrl/Cmd + O` – Import
- `Ctrl/Cmd + S` – Export
- `Ctrl/Cmd + +` / `-` – Zoom in/out
- `Ctrl/Cmd + 0` – Zoom to fit

## Troubleshooting

- If your data does not appear, check that your JSON matches the required format.
- Unpaired events (missing start or end) will be ignored and a warning will be shown in the browser console.
- For large logs, performance may vary depending on your browser and hardware.

## License

This tool is provided as-is for research and analysis purposes.

