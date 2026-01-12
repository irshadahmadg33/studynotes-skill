# Study Notes Summarizer Skill

## Project Overview Video

https://github.com/user-attachments/assets/project-overview.mp4

*A quick 60-second overview of the Study Notes Summarizer skill for
Claude Code*

## Overview

The Study Notes Summarizer is a Claude Code skill that helps users create
concise summaries of documents and articles to save reading time while
retaining important information.

This skill can process various document formats including PDF, DOCX, PPTX,
XLSX, and HTML files (both local and web-based), and generate summaries
that are 1/3 to 1/10 of the original content length.

## Installation

1. Copy the studynotes.skill file to your Claude Code skills directory
2. The skill will be automatically detected and loaded by Claude Code
3. You can verify installation by checking if the skill appears in your
   skills list

## Usage

To use the skill, simply invoke it with natural language commands such as:

- "Summarize this document"
- "Create study notes from [file/URL]"
- "Extract key points from this PDF"
- "Condense this article"
- "Help me make summary notes of this file"

## Workflow

When you invoke the skill, it will guide you through the following steps:

### 1. Document Input

You'll be asked to provide the document either by:

- Uploading a local file (provide the file path)
- Providing a web URL for an online document

### 2. Document Processing

The skill will automatically read the document using the appropriate tool
based on file type (PDF, DOCX, PPTX, XLSX, or HTML)

### 3. Summarization

The skill creates an intelligent summary that:

- Focuses on key concepts, main arguments, and actionable insights
- Excludes verbose explanations of well-known theories and formulas
- Maintains logical flow and structure
- Is self-contained and understandable without the original
- Length adjusts based on document size (1/3 to 1/10 of original)

### 4. Word Count

After summarization, you'll see a comparison:

```text
(Original: X words | Summary: Y words)
```

### 5. Output Delivery

You can choose to:

- Display the summary in the CLI/terminal
- Save to a file (you'll be asked for format and location)

Supported output formats:

- Text file (.txt)
- Markdown file (.md)
- Word document (.docx)
- PDF document (.pdf)

## Example Session

**User:** "Summarize this PDF about machine learning"

**Claude:** "How would you like to provide the document?"
[Options: Upload local file / Provide web URL]

**User:** "Upload local file"
Path: /documents/ml-research-paper.pdf

**Claude:** [Reads and processes the PDF]
[Creates summary]

Summary appears with word count:
(Original: 5000 words | Summary: 1000 words)

"How would you like to receive the summary?"
[Options: Display on CLI / Save to file]

**User:** "Save to file"

**Claude:** "What file format would you like?"
[Options: Text file / Markdown file / Word document / PDF document]

**User:** "Markdown file"

**Claude:** "Where would you like to save the file?"

**User:** "/documents/summaries/"

**Claude:** "Summary saved to:
/documents/summaries/summary_ml-research-paper_2026-01-12.md"

## Supported File Formats

- PDF documents (.pdf)
- Word documents (.docx)
- PowerPoint presentations (.pptx)
- Excel spreadsheets (.xlsx, .xls)
- HTML documents (local files or web URLs)

## Summarization Guidelines

The skill follows these principles when creating summaries:

### Includes

- Main thesis or purpose of the document
- Key concepts and core arguments
- Important findings, conclusions, or recommendations
- Actionable insights or practical applications
- Critical data points or statistics

### Excludes or Minimizes

- Verbose explanations of well-known theories
- Common formulas that don't need reproduction
- Repetitive examples or redundant explanations
- Excessive background information
- Filler words and unnecessary elaboration

### Length Adjustment

- Short documents (<2000 words): ~1/3 of original length
- Medium documents (2000-5000 words): ~1/4 of original length
- Long documents (>5000 words): ~1/5 to 1/10 of original length
- Adjusts based on content density and relevance

## Tips for Best Results

1. Ensure document files are accessible and not corrupted
2. For web documents, verify the URL is publicly accessible
3. For technical documents, the summary preserves critical terminology
4. For research papers, expect focus on methodology, results, and
   conclusions
5. Save summaries in Markdown format for easy editing and formatting

## Technical Details

- **Skill name**: studynotes
- **Version**: 1.0
- **Package file**: studynotes.skill
- **Compatible with**: Claude Code with MCP and skills support
- **Dependencies**: pdf, docx, pptx, xlsx skills (included in Claude Code)

## Troubleshooting

If you encounter issues:

### File not found error

- Verify the file path is correct and accessible
- Use absolute paths rather than relative paths

### Web URL not accessible

- Check that the URL is publicly accessible
- Verify you have internet connectivity
- Some websites may block automated access

### Unsupported file format

- Ensure your file is one of the supported formats
- Check file extension matches actual file type

### Summary too long/short

- The skill automatically adjusts based on content
- Length varies based on document complexity and relevance

## Feedback and Support

This skill was developed as part of a Panaversity formal assignment.
For questions or feedback about the skill, refer to the project repository.

## License

This skill is provided as-is for educational and personal use.
