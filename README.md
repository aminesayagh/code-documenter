# code-documenter

A lightweight, flexible bash script to generate Markdown documentation of your codebase with automatic tree structure generation and code content extraction.

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Bash](https://img.shields.io/badge/bash-5.0%2B-green.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## Features

- 📁 Automatic project structure visualization using `tree`
- 🔍 Regex pattern matching for file selection
- 📊 File statistics (size, lines of code)
- 💻 Code content with line numbers
- ⚡ Fast and lightweight
- 🔧 Highly configurable
- 📝 Markdown output

## Requirements

- Bash 5.0+
- `tree` command (automatically installed if missing)
- Standard Unix tools (`find`, `stat`, `nl`)

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/code-documenter.git

# Make the script executable
chmod +x code-documenter/doc-generator.sh

# Optional: Move to a directory in your PATH
sudo mv code-documenter/doc-generator.sh /usr/local/bin/code-documenter
```

## Usage

### Basic Usage

```bash
# Document all files in current directory
./doc-generator.sh

# Document specific file types using regex
./doc-generator.sh '.*\.ts$'  # TypeScript files
./doc-generator.sh '.*\.py$'  # Python files
```

### Advanced Options

```bash
./doc-generator.sh [options] [pattern]

Options:
  -d, --dir <directory>     Directory to search (default: current directory)
  -o, --output <file>       Output file (default: documentation.md)
  -e, --exclude <pattern>   Exclude pattern (default: node_modules|.git|...)
  -m, --max-size <bytes>    Maximum file size to process (default: 1MB)
  -h, --help               Show this help message
```

### Examples

Document TypeScript files excluding tests:
```bash
./doc-generator.sh -d ./src -o typescript-docs.md -e 'node_modules|test|\.spec\.ts' '.*\.ts$'
```

Document Python files with custom size limit:
```bash
./doc-generator.sh -m 2097152 -o python-docs.md '.*\.py$'  # 2MB limit
```

## Output Format

The script generates a Markdown file with:

1. Project header with timestamp
2. Total file count
3. Project tree structure
4. For each file:
   - File metadata (name, path, size, extension)
   - Line count
   - Full content with line numbers

Example output:
```markdown
# Code Documentation
Generated on: 2024-12-13T12:00:00.000Z
Total files: 42

## Project Structure
...

## File: example.ts
- Path: `src/example.ts`
- Size: 1.2 KB
- Extension: .ts
- Lines of code: 45
- Content:

```ts
1 | import { Example } from './types';
2 | 
3 | export class ExampleClass {
...
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
