# OOP with C++ — Unit 4: Files and Streams

**Programme:** S.Y. B.Tech. Artificial Intelligence and Data Science
**Semester:** III
**Course:** Object-Oriented Programming with C++ (ADPC303)
**Unit:** 4 — Files and Streams
**Language Standard:** C++17 or later

## Overview

This unit covers file handling in C++ — reading, writing, appending, navigating, and managing structured/binary data using file streams.

Topics covered:
- Introduction to file handling
- Types of files (text vs binary)
- Streams and header files
- File operations (open, read, write, close)
- File pointers and navigation
- Error handling
- Structured records (text and binary)

## Learning Outcomes

1. Create, open, close, read, write, and append text files.
2. Use `ifstream`, `ofstream`, and `fstream` correctly.
3. Check file-opening and file-operation errors.
4. Process files line by line and word by word.
5. Store and retrieve structured records.
6. Use file pointers with `seekg()`, `seekp()`, `tellg()`, and `tellp()`.
7. Work with binary files using `read()` and `write()`.
8. Build basic file-based C++ applications.

## Compilation

**Linux/macOS**
```bash
g++ -std=c++17 filename.cpp -o program
./program
```

**Windows (MinGW)**
```bash
g++ -std=c++17 filename.cpp -o program.exe
program.exe
```

## Program Index

| # | Program Title | Main Concept |
|---|----------------|---------------|
| 1 | Write text to a file | `ofstream`, `open()`, `close()` |
| 2 | Read a file line by line | `ifstream`, `getline()` |
| 3 | Append data to a file | `ios::app` |
| 4 | Copy one file into another | File reading and writing |
| 5 | Count lines, words, and characters | File processing |
| 6 | Search a word in a file | Text search |
| 7 | Store student records in a text file | Structured text records |
| 8 | Read and search student records | File parsing |
| 9 | Update a record using a temporary file | File update workflow |
| 10 | File pointer navigation | `seekg()`, `seekp()`, `tellg()`, `tellp()` |
| 11 | Binary file record writing/reading | `write()`, `read()` |
| 12 | Random access in a binary file | Record navigation |
| 13 | File error handling | `fail()`, `eof()`, `bad()`, `good()` |
| 14 | File statistics mini-project | Text analysis |
| 15 | Student record manager mini-project | File-based CRUD operations |
| 16 | Library record mini-project | Object-oriented file application |

## File Streams at a Glance

| Stream Class | Header | Main Use |
|---|---|---|
| `std::ifstream` | `<fstream>` | Read from a file |
| `std::ofstream` | `<fstream>` | Write to a file |
| `std::fstream` | `<fstream>` | Read and write using the same stream |

## Common File Modes

| Mode | Meaning |
|---|---|
| `std::ios::in` | Open for reading |
| `std::ios::out` | Open for writing |
| `std::ios::app` | Append data at the end of the file |
| `std::ios::ate` | Open and initially move to the end; seeking allowed |
| `std::ios::trunc` | Discard existing file content when opening for output |
| `std::ios::binary` | Open file in binary mode |

## Quick Reference

**Create/write a file**
```cpp
std::ofstream outputFile("data.txt");
if (!outputFile) { /* handle error */ }
outputFile << "Text";
```

**Read a file**
```cpp
std::ifstream inputFile("data.txt");
std::string line;
while (std::getline(inputFile, line)) { /* process line */ }
```

**Append to a file**
```cpp
std::ofstream outputFile("data.txt", std::ios::app);
```

**Read and write with one stream**
```cpp
std::fstream file("data.txt", std::ios::in | std::ios::out);
```

**File positions**
```cpp
file.tellg();
file.tellp();
file.seekg(position, std::ios::beg);
file.seekp(position, std::ios::beg);
```

**Binary read/write**
```cpp
file.write(reinterpret_cast<const char*>(&record), sizeof(record));
file.read(reinterpret_cast<char*>(&record), sizeof(record));
```

**Stream state checks**
```cpp
file.good();
file.eof();
file.fail();
file.bad();
```

## Common Errors and Fixes

| Problem | Likely Cause | Fix |
|---|---|---|
| File does not open | Incorrect path or insufficient permission | Verify file name, folder, and permissions |
| Old content disappears | File opened in normal output/truncate mode | Use `std::ios::app` to append |
| Extra loop iteration | Using `while (!file.eof())` | Use `while (std::getline(file, line))` instead |
| File cannot be renamed | File stream still open | Close all streams before `remove()`/`rename()` |
| Search fails with punctuation | Exact word comparison | Normalize case and remove punctuation |
| Binary record is corrupted | Writing non-trivial objects (e.g. `std::string`) as raw bytes | Use fixed-size character arrays or proper serialization |
| Update did not work | Temporary file replacement failed | Check `remove()` and `rename()` return values |
| Read starts from wrong location | File pointer not reset | Use `clear()` and `seekg()` as needed |

## Program-by-Program Summary

1. **Write Text to a File** — Create/open a file with `ofstream` and write lines to it.
2. **Read a File Line by Line** — Read back content using `ifstream` + `getline()`.
3. **Append Data to a File** — Add new content at the end without erasing existing data (`ios::app`).
4. **Copy One File into Another** — Read from a source stream, write to a destination stream, line by line.
5. **Count Lines, Words, and Characters** — Character-by-character scanning with a word-boundary state flag.
6. **Search a Word in a File** — Tokenize file content with `>>` and count exact matches.
7. **Store Student Records** — Save structured data as pipe-delimited (`|`) text records.
8. **Read and Search Student Records** — Parse delimited lines using `stringstream` and search by field.
9. **Update a Record Using a Temporary File** — Safe update workflow: read → rewrite to temp file → replace original.
10. **File Pointer Navigation** — Move and inspect read/write positions with `seekg()`/`seekp()`/`tellg()`/`tellp()`.
11. **Binary File Writing and Reading** — Store/retrieve a fixed-size `struct` as raw bytes.
12. **Random Access in a Binary File** — Compute byte offsets to jump directly to any fixed-size record.
13. **File Error Handling** — Check `is_open()`, `eof()`, `bad()`, `fail()` to diagnose stream state.
14. **File Statistics Mini-Project** — Extend character scanning to count vowels, digits, and spaces too.
15. **Student Record Manager Mini-Project** — Menu-driven CRUD app combining Concepts 7–9.
16. **Library Record Mini-Project** — OOP + file persistence: a `Book` class serialized to/from a text file.

## Suggested Extension Ideas

- Add delete-record operations to the mini-projects.
- Validate input ranges (e.g., marks between 0–100).
- Prevent duplicate roll numbers / book IDs.
- Make text search case-insensitive and punctuation-aware.
- Add due-date/fine calculation to the library system.
- Save analysis reports (e.g., from Concept 14) into an output file.
