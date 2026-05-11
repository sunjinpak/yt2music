# yt2music

A macOS command-line utility that extracts audio from a video URL, embeds metadata and thumbnail, and adds the resulting MP3 to the Apple Music app library with caption-derived lyrics.

## Intended use

**This tool is intended for use with content that you have the legal right to download and reproduce**, including:

- Videos you created and own the rights to
- Content licensed under Creative Commons (CC-BY, CC-BY-SA, etc.)
- Public domain works
- Content for which you have obtained explicit permission from the rights holder

Downloading copyrighted material without authorization may violate the platform's Terms of Service and applicable copyright law in your jurisdiction (including, but not limited to, the U.S. Copyright Act, the DMCA, and the Korean Copyright Act). Users are solely responsible for ensuring their use complies with all applicable laws and platform terms.

This project does not endorse, encourage, or facilitate copyright infringement.

## Requirements

- macOS (uses AppleScript to interact with the Music app)
- [`yt-dlp`](https://github.com/yt-dlp/yt-dlp)
- [`ffmpeg`](https://ffmpeg.org/)
- Python 3 (standard library only)

Install dependencies via Homebrew:

```sh
brew install yt-dlp ffmpeg
```

## Installation

```sh
git clone https://github.com/<your-username>/yt2music.git
cd yt2music
cp yt2music ~/.local/bin/yt2music   # ensure ~/.local/bin is in PATH
chmod +x ~/.local/bin/yt2music
```

## Usage

```sh
yt2music <video_url> [playlist_name]
```

The optional second argument adds the imported track to a named Music app playlist (the playlist must already exist).

### Examples

```sh
# Add to library only
yt2music "https://example.com/your-own-or-CC-licensed-video"

# Also copy into an existing playlist (e.g. "CCM")
yt2music "https://example.com/your-own-or-CC-licensed-video" CCM
```

## What it does

1. Reads video metadata (including detected language)
2. Extracts audio as MP3 at highest available quality
3. Embeds thumbnail and metadata into the MP3
4. Downloads captions in the detected video language first (Korean videos prefer Korean captions; otherwise English is preferred), and converts them to plain-text lyrics
5. Adds the MP3 to the macOS Music app library
6. Sets the lyrics field on the track via AppleScript
7. If a playlist name was supplied, duplicates the track into that playlist

## Limitations

- macOS only (relies on the Music app and AppleScript)
- Lyrics are imported as plain text; the macOS Music app does not time-sync locally imported lyrics
- Lyrics are derived from caption tracks and may be inaccurate, machine-generated, or absent
- Designed for single-file workflows, not bulk operations

## What this tool does NOT do

- It does not circumvent DRM, geographic restrictions, age gates, or paid content barriers
- It does not bundle, distribute, or include any third-party copyrighted media
- It does not enable downloading of content that the user does not otherwise have the right to access and reproduce

The following `yt-dlp` options are intentionally **not** wrapped by this script: `--cookies`, `--cookies-from-browser`, `--geo-bypass`, and similar access-circumvention flags.

## License

MIT License. See [LICENSE](LICENSE).

## Disclaimer

This software is provided "as is", without warranty of any kind. The author is not responsible for any misuse of this tool. Users assume full legal responsibility for their use of this software.
