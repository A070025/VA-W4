# VA-W4
# Week 4: METADATA ANALYSIS REPORT

This repository documents the process of analyzing file metadata and identifying hidden information using various forensic tools.

## 🛠 Tools Learned
The following tools were utilized during this session:
1. `file` - To identify file types.
2. `strings` - To extract human-readable text from binary files.
3. `exiftool` - To read and write meta information.
4. `hexeditor` - To view and edit files in hexadecimal format.
5. `binwalk` - To search for and extract embedded files.

---

## 📋 Task Documentation

| Picture | Tools | Link / Command | Analysis |
| :--- | :--- | :--- | :--- |
| **Ocean.jpg** | `exiftool` | `exiftool Ocean.jpg` | Used to see all info in the image. Flags or hidden messages are often found in the comment section. |
| **Computer.jpg** | `hexeditor` | `hexeditor computer.jpg` | Used to analyze the document header. Helpful for verifying file signatures (e.g., JPEG starts with `FF D8`). |
| **Dog.jpg** | `binwalk` | `binwalk dog.jpg` <br> `binwalk -e dog.jpg` | Used for finding and extracting hidden files embedded within the main image file. |
| **Computer.jpg** | `strings` | `strings computer.jpg` | Extracted human-readable text from the binary file to find hidden strings or messages. |
| **Solitaire.exe**| `file` | `file solitaire.exe` | Revealed that the `.exe` file was actually a PNG image file in disguise. |
| **Rubiks.jpg** | `file` | `file rubiks.jpg` | Identified that the file was actually a PNG despite having a `.jpg` extension. |

---

## 🔍 Detailed Step-by-Step Breakdown

### 1. Extracting Metadata with Exiftool
By running the command below, we can see the technical details of the file:
```bash
exiftool Ocean.jpg
<img width="499" height="462" alt="image" src="https://github.com/user-attachments/assets/fc7524e0-0bf3-4ec5-9062-87858a090f24" />
```
### 2. Analyzing File Headers with Hexeditor
To check if a file is corrupted or intentionally renamed, we look at the magic bytes:
```bash
hexeditor computer.jpg
```
### 3. Finding Hidden Data with Binwalk
If an image contains a hidden zip or another image, binwalk will find it:
```bash
# To scan
binwalk dog.jpg

# To extract
binwalk -e dog.jpg
```
### 4. Reading Strings
Used when we need to find text clues without a hex editor:
```bash
strings dog_secret.jpg | tail
```

### 5. Verifying File Type
Never trust the file extension. Use the file command:
```bash
file solitaire.exe
```

## 💡 Conclusion
Understanding metadata is crucial in cybersecurity for identifying file manipulation and uncovering hidden data that is not visible through standard applications.
