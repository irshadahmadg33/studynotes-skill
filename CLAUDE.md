# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working
with code in this repository.

## Project Overview

This repository is for developing a Claude Code skill called
"Daily Skillset Refresher" that summarizes study notes and articles.
The skill helps users extract important information from documents while
reducing reading time by creating summaries that are 1/3 to 1/10 of the
original content length.

## Project Specification

The complete specification is in `skill-studynotes_prompt.md`.
Key requirements:

**Core Functionality:**

- Summarize content from various document formats
  (.docx, .pdf, .xsl, .pptx, .html)
- Support both local files and cloud/internet documents
- Generate summaries between 1/3 to 1/10 of original length based on
  content relevance
- Include word count comparison (original vs summary) at the end of
  summary
- Hint at proven theories and formulas rather than reproducing them

**User Interaction Flow:**

1. When invoked, prompt user to upload document or specify document
   address
2. After generating summary, ask user for output preference:
   - Present summary on CLI, or
   - Save to file on local machine
3. If saving to file, request:
   - Desired file format for summary
   - Folder address/path for saving
4. Generate README.txt documentation for the skill after completion

## Development Approach

**Skill Structure:**

- This should be implemented as a Claude Code skill
  (similar to /commit, /review-pr)
- The skill should integrate with MCP (Model Context Protocol) servers
  for document handling
- Use existing MCP tools for document reading
  (pdf, docx, xlsx, pptx skills are available)

**Implementation Strategy:**

- Leverage the `pdf`, `docx`, `pptx`, and `xlsx` skills that are
  already available in the Claude Code environment
- For HTML and web documents, use the `WebFetch` tool
- Use `AskUserQuestion` tool for interactive prompts
  (document source, output preferences, file format, save location)
- Use the `Write` tool to save summary files in requested formats

**Document Processing:**

- When processing documents, extract text content first
- Apply intelligent summarization focusing on key concepts,
  main arguments, and actionable insights
- Exclude or minimize reproduction of well-known theories/formulas
  (just reference them)
- Calculate word counts for both original and summary

## Repository Context

This is a Panaversity formal assignment project. The repository currently
contains only the specification document and will be populated with the
skill implementation.
