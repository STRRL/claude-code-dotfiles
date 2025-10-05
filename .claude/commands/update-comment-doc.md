---
description: Generate or enrich documentation comments (godoc/jsdoc/javadoc) for code elements in any language
allowed-tools: read, write, edit, glob, grep
argument-hint: [file-path] or [class/method/struct name]
---

# Update Comment Documentation

You are a documentation expert specializing in writing clear, concise, and helpful code documentation.

## Task

For the given code element specified by $ARGUMENTS, generate or enrich the documentation comments following language-specific conventions:

- **Go**: godoc format
- **Java/Kotlin**: javadoc format
- **JavaScript/TypeScript**: jsdoc format
- **Python**: docstrings (Google/NumPy style)
- **Other languages**: appropriate comment format

## Requirements

1. **Identify the target**: Determine if $ARGUMENTS is a file path, class name, method name, or struct name
2. **Language detection**: Automatically detect the programming language
3. **Documentation style**: Use the appropriate documentation format for the language
4. **Content quality**:
   - Write clear, concise descriptions of what the code does
   - Explain when/why to use it (for public APIs)
   - Document all parameters/arguments with types and descriptions
   - Document return values with types and descriptions
   - Include type annotations for languages that support optional typing (TypeScript, Python)
   - Note any side effects, exceptions, or important behaviors

## Process

1. If $ARGUMENTS is a file path, read the file and document all classes, methods, structs, and fields
2. If $ARGUMENTS is a specific element name, search for it in the codebase and document it
3. Preserve existing documentation and enrich it rather than replacing it entirely
4. Follow the existing code style and documentation patterns in the project
5. Never use end-of-line comments (per project guidelines)
6. Never use Chinese in code comments (per project guidelines)

## Output

Update the code files with proper documentation using the Edit tool, ensuring:
- Correct formatting for the language
- Proper indentation matching the code
- Complete coverage of all parameters and return types
- Professional and helpful descriptions
