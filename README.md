# Tkallem (تكلّم)

Cut the dead air out of your recordings. Tkallem finds the long pauses in an audio file and removes them, right in your browser. Nothing is uploaded; your audio never leaves your device.

*Tkallem* means "speak" in Arabic.

## Features

- Drag and drop an MP3, or choose a file
- Interactive waveform with the pauses to be removed highlighted; click to seek
- Three controls:
  - **Silence level**: −80 to −20 dB (default −45)
  - **Shortest pause to remove**: 0.2 to 3.0 s (default 0.7)
  - **Padding at each cut**: 0 to 400 ms (default 150), so words aren't clipped
- 10 ms fades at every splice to avoid clicks and pops
- Live stats: original length, trimmed length, time saved, pauses removed
- Preview the original or the trimmed audio before exporting
- Export as MP3 (128 or 192 kbps) or lossless WAV, with `_trimmed` added to the filename

## How it works

1. The file is decoded to raw PCM with the Web Audio API.
2. Loudness is measured in 10 ms windows (RMS, loudest channel).
3. Any stretch below the silence level that lasts at least the minimum pause length becomes a cut, shortened by the padding on each side.
4. The remaining segments are joined with short fades.
5. The result is encoded to MP3 with [lamejs](https://github.com/zhuker/lamejs) or to 16-bit WAV.

## Usage

Tkallem is a single HTML file with no build step. Open `index.html` in a browser, or host it with GitHub Pages.

MP3 export loads lamejs from a CDN, so it needs an internet connection. WAV export works offline.

## Tips

- If pauses aren't being detected, raise the silence level. Steady background noise louder than the threshold doesn't count as silence.
- Files are decoded fully into memory, so multi-hour recordings may be slow.

## Built with

HTML, CSS, vanilla JavaScript, the Web Audio API and lamejs.