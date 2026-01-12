---
name: studynotes
description: "Document summarization tool for creating concise study notes from various file formats. Use when users need to: (1) Summarize articles, documents, or study materials, (2) Extract key information from PDFs, DOCX, PPTX, XLSX, or HTML files, (3) Save reading time by condensing lengthy content, (4) Create study notes that are 1/3 to 1/10 of the original length. Triggers include requests like 'summarize this document', 'create study notes from', 'extract key points', or 'condense this article'."
---

# Study Notes Summarizer

This skill helps users create concise summaries of documents and articles
to save reading time while retaining important information.

## Core Functionality

**Supported Formats:**

- PDF documents (.pdf)
- Word documents (.docx)
- PowerPoint presentations (.pptx)
- Excel spreadsheets (.xlsx, .xls)
- HTML documents (local or web URLs)

**Summary Characteristics:**

- Length: 1/3 to 1/10 of original content
- Focus on key concepts, main arguments, and actionable insights
- Exclude verbose explanations of well-known theories and formulas
  (just reference them)
- Include word count comparison at the end

## Workflow

### 1. Document Input

When the skill is invoked, ask the user to provide the document:

```text
How would you like to provide the document?
1. Upload a local file (provide the file path)
2. Provide a web URL for an online document
```

Use the AskUserQuestion tool with options:

- "Upload local file" - User will provide a file path
- "Provide web URL" - User will provide a URL

After receiving the choice, prompt for the specific path or URL.

### 2. Document Reading

Based on the file type, use the appropriate tool:

**PDF files**: Use the `pdf` skill

```text
Read the PDF file at [path] and extract all text content
```

**Word documents (.docx)**: Use the `docx` skill

```text
Read the DOCX file at [path] and extract all text content
```

**PowerPoint files (.pptx)**: Use the `pptx` skill

```text
Read the PPTX file at [path] and extract all text content from slides
```

**Excel files (.xlsx, .xls)**: Use the `xlsx` skill

```text
Read the spreadsheet at [path] and extract all data
```

**HTML/Web documents**: Use the `WebFetch` tool

```text
Fetch and extract content from [URL]
```

### 3. Content Summarization

Apply intelligent summarization following these guidelines:

**Include:**

- Main thesis or purpose of the document
- Key concepts and core arguments
- Important findings, conclusions, or recommendations
- Actionable insights or practical applications
- Critical data points or statistics

**Exclude or Minimize:**

- Verbose explanations of well-known theories
  (just reference: "Uses Newton's Laws of Motion")
- Common formulas that don't need reproduction
  (just hint: "Applies the quadratic formula")
- Repetitive examples or redundant explanations
- Excessive background information
- Filler words and unnecessary elaboration

**Length Guidelines:**

- Short documents (<2000 words): Aim for 1/3 of original length
- Medium documents (2000-5000 words): Aim for 1/4 of original length
- Long documents (>5000 words): Aim for 1/5 to 1/10 of original length
- Adjust based on content density and relevance

### 4. Word Count Calculation

After creating the summary:

1. Count words in the original document
2. Count words in the summary
3. Calculate the ratio

Format: `(Original: [X] words | Summary: [Y] words)`

### 5. Output Delivery

Ask the user for their output preference using AskUserQuestion:

```text
How would you like to receive the summary?
```

Options:

- "Display on CLI" - Show the summary in the terminal
- "Save to file" - Save the summary to a local file

**If "Display on CLI":**
Display the summary followed by the word count on a new line.

**If "Save to file":**
Ask two follow-up questions:

1. **File format**: Use AskUserQuestion with options:
   - "Text file (.txt)"
   - "Markdown file (.md)"
   - "Word document (.docx)"
   - "PDF document (.pdf)"

2. **Save location**: Ask the user to provide the folder path where they
   want to save the file.

Generate a filename using the pattern:
`summary_[original-filename]_[date].[extension]`

Use the appropriate tool to create the file:

- Text/Markdown: Use the `Write` tool
- Word document: Use the `docx` skill
- PDF document: Use the `pdf` skill

Confirm the file has been saved with the full path.

## Example Usage

**User:** "Summarize this PDF about machine learning"

**Response:**

1. Ask for document location (local file or URL)
2. User provides: `/path/to/ml-paper.pdf`
3. Read PDF using pdf skill
4. Create summary (e.g., 5000 word paper → 1000 word summary)
5. Add word count: `(Original: 5000 words | Summary: 1000 words)`
6. Ask output preference
7. User chooses "Save to file"
8. Ask file format → User chooses "Markdown file (.md)"
9. Ask save location → User provides `/path/to/summaries/`
10. Save as `/path/to/summaries/summary_ml-paper_2026-01-12.md`
11. Confirm completion

## Tips for Effective Summaries

- Maintain the logical flow and structure of the original content
- Use bullet points or numbered lists for clarity when appropriate
- Preserve important terminology and domain-specific language
- Ensure the summary is self-contained and understandable without the original
- For technical content, keep critical formulas but remove derivation steps
- For research papers, focus on methodology, results, and conclusions
