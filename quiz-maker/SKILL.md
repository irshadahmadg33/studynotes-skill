---
name: quiz-maker
description: Interactive quiz generator that creates multiple-choice quizzes from study materials, summaries, or any topic. Conducts quizzes interactively on CLI with configurable question count (1-10) and difficulty distribution (low/medium/high), then displays results and saves them to Excel file. Use when users want to test their knowledge, create quizzes from documents or summaries, or generate practice questions from any topic.
---

# Quiz Maker Skill

Generate and conduct interactive multiple-choice quizzes from study materials, summaries, or topics with automatic result tracking.

## Overview

This skill creates quizzes from various sources and conducts them interactively on the CLI. It supports customizable question counts, difficulty levels, and automatically saves results to Excel format.

## Workflow

Follow this workflow when the skill is invoked:

### 1. Gather Quiz Source Material

Ask the user for the source material using AskUserQuestion:

**Question**: "What would you like to base the quiz on?"
**Options**:
- File path (summary file, document, or notes on local machine)
- URL (article or document from internet)
- Direct topic (user will specify a topic/subject)

Based on the response:
- **File path**: Use the Read tool to load the content from the provided file path
- **URL**: Use the WebFetch tool to retrieve content from the URL
- **Direct topic**: Ask user to provide the topic/subject name

### 2. Configure Quiz Parameters

Ask the user for quiz configuration using AskUserQuestion:

**Question 1**: "How many questions would you like in the quiz?" (1-10)
Provide options: 5 (Recommended), 10, Custom number

**Question 2**: "How should questions be distributed across difficulty levels?"
**Options**:
- Balanced (equal distribution across low/medium/high)
- Progressive (start easy, get harder)
- Custom (user specifies exact distribution)

If user selects "Custom", ask for the specific distribution:
- Number of low difficulty questions
- Number of medium difficulty questions
- Number of high difficulty questions
(Ensure total equals the question count from Question 1)

### 3. Generate Quiz Questions

Generate the specified number of multiple-choice questions based on:
- The source material content
- The difficulty distribution requested
- MCQ format with 4 options (A, B, C, D) per question

**Question Structure**:
- Question text clearly stated
- Four distinct answer options labeled A, B, C, D
- Only one correct answer
- Options should be plausible and test understanding

**Difficulty Guidelines**:
- **Low**: Recall-based, direct facts from content
- **Medium**: Application and comprehension, requiring some analysis
- **High**: Analysis, synthesis, or evaluation requiring deeper understanding

Store the generated questions in a data structure that tracks:
- Question number
- Question text
- Four options (A, B, C, D)
- Correct answer
- Difficulty level

### 4. Conduct Quiz Interactively

Present questions one at a time to the user on the CLI:

For each question:
1. Display: "Question [N] of [TOTAL] (Difficulty: [LOW/MEDIUM/HIGH])"
2. Show the question text
3. Display all four options (A, B, C, D) with their text
4. Prompt: "Your answer (A/B/C/D):"
5. Wait for user input
6. Validate input (must be A, B, C, or D)
7. Store the user's answer
8. Move to next question (do NOT reveal if answer was correct yet)

Continue until all questions are answered.

### 5. Calculate and Display Results

After the last question is answered:

1. Calculate the score:
   - Total questions answered correctly
   - Total questions
   - Percentage score

2. Display results on CLI in this format:

```
=====================================
QUIZ COMPLETED!
=====================================

Your Score: [X] out of [Y] ([Z]%)

Results Breakdown:
Question 1: [Your Answer] | Correct: [Correct Answer] | ✓ Correct / ✗ Incorrect
Question 2: [Your Answer] | Correct: [Correct Answer] | ✓ Correct / ✗ Incorrect
...

Difficulty Breakdown:
Low: [X]/[Y] correct
Medium: [X]/[Y] correct
High: [X]/[Y] correct

=====================================
```

### 6. Save Results to Excel

Use the bundled script to save results:

1. Prepare quiz data in JSON format:
```json
{
  "topic": "[Quiz topic or source]",
  "timestamp": "[YYYY-MM-DD HH:MM:SS]",
  "score": {
    "correct": [number],
    "total": [number]
  },
  "questions": [
    {
      "question_num": 1,
      "user_answer": "[A/B/C/D]",
      "correct_answer": "[A/B/C/D]",
      "is_correct": true/false
    },
    ...
  ]
}
```

2. Ask user for save location using AskUserQuestion:
   - Default: Current working directory with filename "quiz_results_[timestamp].xlsx"
   - Custom: User specifies full path

3. Execute the save script:
```bash
python scripts/save_quiz_results.py [output_file_path] '[quiz_data_json]'
```

4. Confirm to user: "Quiz results saved to: [file_path]"

## Script Usage

### save_quiz_results.py

Generates a formatted Excel file with quiz results.

**Location**: `scripts/save_quiz_results.py`

**Usage**:
```bash
python scripts/save_quiz_results.py <output_file> <quiz_data_json>
```

**Parameters**:
- `output_file`: Path where Excel file should be saved (e.g., `results.xlsx`)
- `quiz_data_json`: JSON string containing quiz results (see format in step 6 above)

**Requirements**: openpyxl library (`pip install openpyxl`)

**Output**: Excel file with:
- Quiz title and topic
- Completion timestamp
- Score summary with percentage
- Detailed question-by-question results
- Color coding (green for correct, red for incorrect)
- Formatted headers and borders

## Important Notes

- Always present questions one at a time interactively
- Do NOT reveal correct answers until all questions are completed
- Validate user input for each answer (only accept A, B, C, D)
- Maintain question order throughout quiz and results
- Include timestamp in results for tracking
- If openpyxl is not installed, inform user and provide installation command
- Ensure Excel file path is valid and writable before executing script

## Example Invocation

**User**: "Create a quiz from my biology notes"

**Workflow**:
1. Ask for file path to biology notes
2. Read the file content
3. Ask: "How many questions? (5 recommended)"
4. Ask: "Difficulty distribution?" (Balanced recommended)
5. Generate 5 questions (balanced across difficulty levels)
6. Conduct quiz interactively, one question at a time
7. Display complete results on CLI
8. Ask: "Where should I save the results?" (default: ./quiz_results_[timestamp].xlsx)
9. Execute save_quiz_results.py script
10. Confirm: "Quiz results saved to: ./quiz_results_2024-01-15_14-30-45.xlsx"
