## Database Definitions

This project uses **no database**. All state is persisted in JSON files committed to the Git repository.

### `models.json`

| Field | Type | Description |
|-------|------|-------------|
| (root) | `string[]` | Sorted array of OpenRouter free model IDs |

Example entry: `"google/gemma-3-4b-it:free"`

### `CHANGELOG.json`

| Field | Type | Description |
|-------|------|-------------|
| `changes` | `ChangeEntry[]` | Array of change records (max 100) |

#### `ChangeEntry`

| Field | Type | Description |
|-------|------|-------------|
| `timestamp` | `string` | ISO 8601 UTC timestamp |
| `added` | `string[]` | Model IDs added in this run |
| `removed` | `string[]` | Model IDs removed in this run |
| `total_models` | `number` | Total free models after this run |

## Migration History

- **2026-04-30**: Project initialized from `nvidia-nim-models-monitor` fork. All NVIDIA data cleared. OpenRouter free model schema adopted.
