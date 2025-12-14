# Question Evasion (ConvoKit-formatted)

**What this is.**  
A ConvoKit corpus converted from `QAEvasion.csv`, which is political interview Q–A pairs annotated for response clarity / evasion.

## Source
- Source CSV: `QAEvasion.csv`
- Source Paper: Thomas, Filandrianos, Lymperaiou, Zerva, and Stamou (2024), "I Never Said That": A dataset, taxonomy and baselines on response clarity classification. arXiv:2409.13879

## Mapping to ConvoKit
- **One conversation per single sub-question**
- **Two utterances per conversation**:
  1) Interviewer asks
  2) President answers
- **Conversation ID = the first utterance ID** (the question). The answer’s `reply_to` points to the question.
- **Conversation meta:** `title`, `date`, `url`, `president`, `question_order`
- **Question utterance meta:** `type` (= "question"), `question_order`, `interview_question_raw`, `gpt35_summary`, `title`, `date`, `url`
- **Answer utterance meta:** `type` (= "answer"), `question_order`, `label`, `annotator_id`, `inaudible`, `multiple_questions`, `affirmative_questions`, `interview_answer_raw`, `gpt35_prediction`

## Folder contents
- `utterances.jsonl`  (one JSON per line)
- `speakers.json`     (speaker-id to metadata)
- `conversations.json` (conversation-id to metadata)
- `corpus.json`       (top-level corpus meta)
- `index.json`        (type index)
- `README.md`
- `conversion_and_analysis.ipynb` (the notebook that produced this conversion)

## Basic stats
- Conversations: 3448
- Utterances: 6896
- Speakers: 5

Label distribution:
- Claims ignorance        119
- Clarification            92
- Declining to answer     145
- Deflection              381
- Dodging                 706
- Explicit               1052
- General                 386
- Implicit                488
- Partial/half-answer      79

Flags:
- inaudible = 45
- multiple_questions = 86
- affirmative_questions = 772
