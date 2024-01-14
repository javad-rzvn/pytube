<div align="center">
  <p>
    <a href="#"><img src="https://assets.nickficano.com/gh-pytube.min.svg" width="456" height="143" alt="pytube logo" /></a>
  </p>
</div>

# pytube

*pytube* is a genuine, lightweight, dependency-free Python library (and command-line utility) for downloading YouTube videos.

## Documentation

Detailed documentation about the usage of the library can be found at [pytube.io](https://pytube.io). This is recommended for most cases. If you want to hastily download a single video, the [quick start](#Quickstart) guide below might be what you're looking for.

## Features

- Support for both progressive & DASH streams
- Support for downloading the complete playlist
- Easily register ``on_download_progress`` & ``on_download_complete`` callbacks
- Command-line interfaced included
- Caption track support
- Outputs caption tracks to .srt format (SubRip Subtitle)
- Ability to capture thumbnail URL
- Extensively documented source code
- No third-party dependencies
- Proxy support
- Suport for bulk downloading channel videos

## Quickstart

This guide covers the most basic usage of the library. For more detailed information, please refer to [pytube.io](https://pytube.io).

### Installation

Pytube requires an installation of Python 3.6 or greater, as well as pip. (Pip is typically bundled with Python [installations](https://python.org/downloads).)

To install using github:

```bash
$ python -m pip install git+https://github.com/javad-rzvn/pytube
```

## Usage

If you have internet problem, you should use proxy. To do that, you better setup a ``v2ray`` connection, then use its proxy to download videos.

### Download single video from youtube channel

```python
from pytube import YouTube
from pytube.cli import on_progress

YouTube("https://youtu.be/2lAe1cqCOXo").streams.first().download()
proxies = {"http": "socks5://127.0.0.1:2080"}
yt = YouTube(
    "http://youtube.com/watch?v=2lAe1cqCOXo",
    on_progress_callback=on_progress,
    # on_complete_callback=complete_func,
    proxies=proxies,
)
yt.streams.filter(progressive=True, file_extension="mp4").order_by(
    "resolution"
).desc().first().download()
```

### Download all channel's videos

In the example below, it downloads only 3 videos of the channel.

```python
from pytube import Channel

proxies = {"http": "socks5://127.0.0.1:2080"}
c = Channel('https://www.youtube.com/c/FalcomMusicChannel/videos', proxies=proxies)

print(f'Downloading videos by: {c.channel_name}')
print(f'Channel URLs: {c.video_urls[:3]}')

for i, video in enumerate(c.videos[:3]):
    print(c.video_urls[i])
    video.streams.first().download()
```
