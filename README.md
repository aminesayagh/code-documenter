# code-documenter

A lightweight, flexible bash script that generates comprehensive Markdown documentation of your codebase, featuring automatic tree structure generation, file analysis, and intelligent file exclusion patterns.

![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)
![Bash](https://img.shields.io/badge/bash-5.0%2B-green.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## Features

- 📁 Automatic project structure visualization using `tree`
- 🔍 Intelligent file filtering with `.docignore` support
- 📊 Detailed file statistics (size, lines of code)
- 💻 Code content extraction with line numbers
- ⚡ Fast and lightweight
- 🔧 Highly configurable
- 📝 Markdown output with syntax highlighting

## Requirements

- Bash 5.0+
- `tree` command (automatically installed if missing)
- Standard Unix tools (`find`, `stat`, `nl`, `bc`)

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

### Using .docignore

The script supports a `.docignore` file similar to `.gitignore`. Create a `.docignore` file in your project root:

```gitignore
# Dependencies
node_modules/
vendor/

# Build outputs
dist/
build/
*.min.js

# IDE and Editor files
.idea/
.vscode/
*.swp
*.swo
.DS_Store

# Test files
**/*.test.ts
**/*.spec.ts
__tests__/
test/
coverage/

# Other
.git/
.env
*.log
tmp/
```

Patterns in `.docignore` follow the same format as `.gitignore`:
- Simple file/directory names (`output.md`, `node_modules/`)
- Wildcards (`*.log`, `**/*.test.ts`)
- Directory indicators (`/`)
- Comments (`#`)

### Examples

Document TypeScript files excluding tests:
```bash
./doc-generator.sh -d ./src -o typescript-docs.md '.*\.ts$'
```

Document Python files with custom size limit:
```bash
./doc-generator.sh -m 2097152 -o python-docs.md '.*\.py$'  # 2MB limit
```

## Output Format

The script generates a Markdown file containing:

1. Documentation Header
   - Generation timestamp
   - Total file count

2. Project Structure
   - Tree view of the project
   - Respects `.docignore` patterns

3. File Documentation (for each file):
   - File metadata
     - Name and path
     - Size (human-readable format)
     - Extension
     - Lines of code
   - Full content with:
     - Line numbers
     - Syntax highlighting based on extension

Example output:
```markdown
# Code Documentation
Generated on: 2024-12-13T12:00:00.000Z
Total files: 42

## Project Structure
.
├── src/
│   ├── cli/
│   ├── core/
│   └── utils/
└── tests/

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

## Technical Details

### Pattern Handling

The script handles three types of patterns:
1. Include patterns (command line argument)
2. Exclude patterns (--exclude option)
3. .docignore patterns

Pattern conversion flow:
1. Glob patterns → Regex patterns
2. Multiple patterns → Composite find command
3. Special handling for tree command patterns

### File Processing

Files are processed in three stages:
1. Tree structure generation using `tree`
2. File discovery using `find`
3. Content extraction and formatting

Size formatting uses dynamic units (B, KB, MB, GB) with proper rounding.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

Key areas for contribution:
- Pattern matching improvements
- Performance optimizations
- Additional output formats
- Better error handling

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- `tree` command for directory visualization
- Git for inspiration on ignore patterns
- The Bash community for scripting best practices
