# extract-apple-voice-memos-transcript

This script extracts transcript data from Apple Voice Memos `.m4a` files.

## Requirements

- Python 3

## Usage

```bash
./extract-apple-voice-memos-transcript [options] <filename>
```

Voice Memos recordings are stored at `~/Library/Group Containers/group.com.apple.VoiceMemos.shared/Recordings` if iCloud sync is enabled for Voice Memos.

### Options

- `--text`: print transcript as plain text (default)
- `--json`: print transcript data as JSON
- `--raw`: print raw transcript data

### Example output with `--json` flag

Examples below are formatted for readability. Actual output is compact (no whitespace or newlines).

There are two formats: in one, text and attributes are interleaved; in the other, they are separated.

```json
{
  "attributedString": [
    "This is",
    { "timeRange": [0, 0.42] },
    "the transcript text",
    { "timeRange": [0.42, 1.23] },
    "interleaved with attributes.",
    { "timeRange": [1.23, 2.00] }
  ],
  "locale": { "identifier": "en_US", "current": 0 }
}
```

```json
{
  "attributedString": {
    "attributeTable": [    
      { "timeRange": [0, 0.42] },
      { "timeRange": [0.42, 1.23] },
      { "timeRange": [1.23, 2.00] }
    ],
    "runs": [
      "In this format",
      0,
      "text is interleaved with",
      1,
      "indices of attributes",
      2
    ]
  },
  "locale": { "identifier": "en_US", "current": 0 }
}
```

## Transcript data format

Apple Voice Memos stores transcripts in `.m4a` files using the `tsrp` atom (box), which appears to be an Apple-proprietary extension. The atom hierarchy is:

```
moov
└── trak
    └── udta
        └── tsrp
```

The `tsrp` atom contains UTF-8 encoded JSON data. See the example output above for the structure.
