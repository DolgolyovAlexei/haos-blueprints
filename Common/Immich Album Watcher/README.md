# Immich Album Watcher Blueprint

This blueprint monitors Immich album changes and sends notifications when assets (photos/videos) are added to specified albums. Designed to be used in pair with the `Immich Album Watcher` integration.

## Features

- Filter by hub/instance name (for multi-hub setups)
- Monitor specific albums by name (whitelist)
- Filter by asset type (track images only, videos only, or both)
- Send notifications to multiple targets simultaneously
- Customizable notification messages with template variables
- Separate templates for image and video assets
- Optional: include people detected in photos
- Optional: include detailed asset list with per-item formatting
- Support for multiple change types (assets added, removed, changed)
- Optional: send photos/videos as Telegram media attachments
- Optional: periodic summary notifications with album list and share URLs

## Event Data from Immich

### Assets Added/Removed/Changed Events

| Field | Description |
|-------|-------------|
| `hub_name` | Name of the Immich hub/instance that sent the event |
| `album_id` | Album ID |
| `album_name` | Album name |
| `album_url` | Public URL to view the album (only if album has shared link) |
| `change_type` | Type of change (assets_added, assets_removed, changed) |
| `added_count` | Number of assets added |
| `removed_count` | Number of assets removed |
| `added_assets` | List of added assets (see Added Assets Fields below) |
| `removed_assets` | List of removed asset IDs |
| `people` | List of all people detected in the album |

### Album Renamed Event

| Field | Description |
|-------|-------------|
| `hub_name` | Name of the Immich hub/instance that sent the event |
| `album_id` | Album ID |
| `old_name` | Previous album name |
| `new_name` | New album name |
| `album_url` | Public URL to view the album (only if album has shared link) |

### Album Deleted Event

| Field | Description |
|-------|-------------|
| `hub_name` | Name of the Immich hub/instance that sent the event |
| `album_id` | Album ID |
| `album_name` | Album name that was deleted |

## Added Assets Fields

Each item in `added_assets` contains:

| Field | Description |
|-------|-------------|
| `id` | Unique asset ID |
| `type` | Type of asset (IMAGE or VIDEO) |
| `filename` | Original filename of the asset |
| `created_at` | Date/time when the asset was originally created |
| `owner` | Display name of the user who owns the asset |
| `owner_id` | Unique ID of the user who owns the asset |
| `description` | Description/caption (user-added in Immich, or EXIF fallback) |
| `is_favorite` | Whether the asset is marked as favorite (true or false) |
| `rating` | User rating of the asset (1-5 stars, or null if not rated) |
| `url` | Public URL to view the asset (only if album has shared link) |
| `download_url` | Direct download URL for the original file (if shared link exists) |
| `playback_url` | Video playback URL (for VIDEO assets only, if shared link exists) |
| `photo_url` | Photo preview URL (for IMAGE assets only, if shared link exists) |
| `people` | List of people detected in this specific asset |

## Message Template Variables

All message templates support these placeholder variables (use single braces):

| Variable | Description |
|----------|-------------|
| `{album_name}` | Name of the album |
| `{album_url}` | Public URL to view the album (empty if no shared link) |
| `{added_count}` | Number of assets added |
| `{removed_count}` | Number of assets removed |
| `{people}` | Comma-separated list of people detected |
| `{assets}` | Formatted list of added assets (using asset item template) |
| `{video_warning}` | Warning about video size limits (Telegram only, empty otherwise) |
| `{common_date}` | Common date formatted with template if all assets share same date, empty otherwise |

## Asset Item Template Variables

These variables can be used in the image and video asset templates. Also used for Telegram media captions.

| Variable | Description |
|----------|-------------|
| `{filename}` | Original filename of the asset |
| `{description}` | Description/caption (user-added in Immich, or EXIF fallback) |
| `{type}` | Asset type (IMAGE or VIDEO) |
| `{created}` | Creation date/time (always shown) |
| `{created_if_unique}` | Creation date/time formatted with template if dates differ, empty if all same |
| `{owner}` | Owner display name |
| `{url}` | Public URL to view the asset (empty if no shared link) |
| `{download_url}` | Direct download URL for the original file |
| `{photo_url}` | Photo preview URL (for IMAGE assets only) |
| `{playback_url}` | Video playback URL (for VIDEO assets only) |
| `{people}` | People detected in this asset |
| `{album_name}` | Name of the album |
| `{is_favorite}` | Favorite indicator (using template) if asset is favorite, empty otherwise |
| `{rating}` | User rating (1-5) or empty if not rated |

## Telegram Media Attachments

When enabled, photos/videos are sent as media attachments to Telegram using the `immich_album_watcher.send_telegram_notification` service.

### Supported Recipients

1. **Notify Entities**: Select Telegram notify entities. Chat ID is extracted from the friendly name. Format: `"Name (123456789)"`
2. **Input Text Entities**: Select input_text entities containing chat IDs for groups/channels.

### Requirements

- Immich Album Watcher integration must be configured with Telegram bot token
- Immich album must have a shared link (to generate public asset URLs)

### Behavior

- First sends a text notification message to each Telegram chat
- Then sends photos/videos as media groups (albums) as replies to that message
- Media is downloaded from Immich and uploaded to Telegram (bypasses CORS)
- Large media lists are automatically split into multiple groups (2-10 items per group)

### Limitations

- Only assets with valid public URLs will be sent
- Telegram has a 50 MB file size limit for media
- Optional video warning can be shown when videos are present
- Media captions use the Image/Video Asset Templates

## Periodic Summary

Sends a summary notification of tracked albums at regular intervals. Album names and share URLs are automatically read from the Album ID Entity's `album_name` and `share_url` attributes (if available).

### Summary Message Template Variables

| Variable | Description |
|----------|-------------|
| `{albums}` | Formatted list of albums (using album item template) |
| `{album_count}` | Number of tracked albums |

### Album Item Template Variables

| Variable | Description |
|----------|-------------|
| `{album_name}` | Name of the album |
| `{album_url}` | Share URL for the album |

### Testing Periodic Summary

To test the periodic summary without waiting for the scheduled time, fire this event from Developer Tools > Events:

- **Event type**: `immich_album_watcher_test_periodic_summary`

To target a specific automation, set its Automation ID in config and include it in the event data:

- **Event data**: `{"automation_id": "your-automation-id"}`

## Scheduled Assets

Sends scheduled notifications with existing assets from tracked albums. Uses the `immich_album_watcher.get_assets` service to fetch assets.

### Album Modes

| Mode | Description |
|------|-------------|
| `per_album` | Send separate notifications for each tracked album |
| `combined` | Fetch assets from all albums into one notification |
| `random` | Pick one random album each time |

### Asset Filter Options

| Option | Description |
|--------|-------------|
| `limit` | Maximum number of assets to fetch (1-100) |
| `favorite_only` | Only fetch favorite assets |
| `asset_type` | Filter by type (all, photo, video) |
| `order_by` | Sort by (random, date, rating, name) |
| `order` | Sort direction (ascending, descending) |
| `filter_min_rating` | Minimum rating filter (1-5, 0 = no filter) |
| `min_date` | Assets created on or after this date (YYYY-MM-DD) |
| `max_date` | Assets created on or before this date (YYYY-MM-DD) |

### Scheduled Assets Message Template Variables

| Variable | Description |
|----------|-------------|
| `{album_name}` | Name of the album |
| `{album_url}` | Share URL for the album |
| `{asset_count}` | Number of assets fetched |
| `{assets}` | Formatted list of assets (using asset item template) |

### Testing Scheduled Assets

To test without waiting for the scheduled time, fire this event:

- **Event type**: `immich_album_watcher_test_scheduled_assets`

To target a specific automation, set its Automation ID in config and include it in the event data:

- **Event data**: `{"automation_id": "your-automation-id"}`

## Author

Alexei Dolgolyov (dolgolyov.alexei@gmail.com)
