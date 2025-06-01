# extract-apple-voice-memos-transcript

This script extracts transcript data from Apple Voice Memos `.m4a` files.

## Usage

```bash
./extract-apple-voice-memos-transcript [options] <filename>
```

Voice Memos recordings are stored at `~/Library/Group Containers/group.com.apple.VoiceMemos.shared/Recordings` if iCloud sync is enabled for Voice Memos.

### Options

- `--text`: print transcript as plain text (default)
- `--json`: print transcript data as JSON
- `--raw`: print raw transcript data

## Requirements

- Python 3

## Notes

Transcript data is in JSON format and usually looks like the following:

```js
{
  "attributedString": [
    "This is",
    { "timeRange": [0, 0.42] },
    "the transcript text",
    { "timeRange": [0.42, 1.23] },
    "interleaved with time ranges."
  ],
  "locale": { "identifier": "en_US", "current": 0 }
}
```
