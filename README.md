# PhotoPaw

**PhotoPaw** is a simple Bash script to organize photos and videos by their capture date. The script automatically moves your RAW, JPEG, and video files into a date-based folder structure using EXIF metadata.

## Features

* Supports RAW, JPEG, and popular video formats.
* Creates a directory structure based on capture date (YYYY/MM-DD).
* Optionally processes files recursively.
* Automatically generates a configuration file.
* Chooses the move method (`mv` or `rsync`) based on the filesystem.

## Installation

The script doesn’t require installation—just clone the repository and make it executable:

```bash
git clone <repo-url>
cd <repo-directory>
chmod +x photopaw.sh
```

**Requirements:**

* Bash 4.0 and later (POSIX-compatible shell)
* `exiftool`
* (optional) `rsync` for moving files across different drives

## Usage

```bash
./photopaw.sh [options] <source_dir>
```

### Options

* `-s, --set-media-dir <path>` — set the media directory (`MEDIA_DIR`) and exit.
* `-q, --quiet` — suppress log output.
* `-r, --recursive` — process files in subdirectories.
* `-h, --help` — show the help message.

### Example

```bash
./photopaw.sh -r ~/Downloads
```

Moves all supported files from `~/Downloads` and its subfolders to `MEDIA_DIR`, creating a date-based folder structure.

## Configuration

By default, the script creates a configuration file at:

```
~/.config/photopaw/config
```

Example content:

```bash
MEDIA_DIR="$HOME/photos"
RAW_EXTENSIONS=( "arw" "cr2" "dng" ... )
MOV_EXTENSIONS=("mov" "mp4")
JPEG_EXTENSIONS=("jpg" "jpeg")
```

You can change `MEDIA_DIR` using the `--set-media-dir` option.

## Example Directory Structure

After running PhotoPaw, your media directory might look like this:

```
photos/
├── 2025/
│   ├── 11-09/
│   │   ├── jpg/
│   │   │   ├── photo1.jpg
│   │   │   └── photo2.jpg
│   │   ├── arw/
│   │   │   └── raw_photo1.arw
│   │   └── mp4/
│   │       └── video1.mp4
└── 2026/
    └── 06-08/
        └── jpg/
            └── photo3.jpg
```

Each file type is placed in its own folder under the date of capture.

## License

MIT License
