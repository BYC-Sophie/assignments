# MentalManip Corpus

A converted version of the Hugging Face [audreyeleven/MentalManip](https://huggingface.co/datasets/audreyeleven/MentalManip) dataset, formatted as a ConvoKit Corpus with conversation-level annotations.

The dataset contains dialogues regarding techniques (when present) of mental manipulation (i.e. "using language to influence, alter, or control an individual’s psychological state or perception for the manipulator’s benefit"), as well as the targeted vulnerabilities.
There are three separate files in the MentalManip repo: mentalmanip_detailed.csv, mentalmanip_con.csv, and mentalmanip_maj.csv.
Here, we use the mentalmanip_con.csv version which contains final gold labels processed by the authors.

Original Paper Link: [MentalManip: A Dataset For Fine-grained Analysis of Mental Manipulation in Conversations](https://arxiv.org/abs/2405.16584)
Citation: Wang, Y., Yang, I., Hassanpour, S., & Vosoughi, S. (2024). MentalManip: A dataset for fine-grained analysis of mental manipulation in conversations. arXiv preprint arXiv:2405.16584.


## Dataset Details

### Speaker-level information
- Speakers in original dataset are labeled generally as `Person1`, `Person2`, etc.  
  To distinguish across different conversations, each speaker is uniquely identified by prefixing with the conversation ID  `<row_id>__<speaker_label>`, e.g. `85514414__Person1`, where `<row_id>` is the original row ID of the conversation in the original dataset.
  Each speaker has:
  - `id`: ID for this speaker
  - `role_label`: Person1 or Person2 in this conversation

### Utterance-level information
For each utterance, we provide:
  - `id`: constructed as `<row_id>__u<turn_index>` (conversation ID + u for utterance, turn index for "which turn in the conversation", e.g. 85514414__u0)
  - `speaker`: speaker ID as above of the utterance
  - `conversation_id`: set to the ID of the first utterance in the conversation (i.e., `<row_id>__u0`)
  - `reply_to`: points to the previous utterance in the same conversation
  - `timestamp`: here replaced with turn index as pseudo timestamp
  - `text`: utterance content

Metadata for utterances include:
  - `parsed`: parsed version of the utterance text, represented as a SpaCy Doc

### Conversation-level information

Conversations are indexed by the ID of the first utterance that makes the conversation. (`<row_id>__u0`)
Each conversation is annotated with metadata:

- `manipulative`: indicator (0 or 1)
- `technique`: list of manipulation techniques (parsed from comma-separated string)
- `vulnerability`: list of vulnerabilities (parsed from comma-separated string)


### Corpus-level Metadata

Additional information about the corpus includes:

- `name`: `"MentalManip_con"`



## Usage Example

### Load the Corpus

```python
from convokit import Corpus

# Assuming corpus is saved as "./mentalmanip-corpus"
corpus = Corpus(filename="./mentalmanip-corpus")

corpus.print_summary_stats()
```
Basic Stats:
 - Number of Speakers: 5830
 - Number of Utterances: 19232
 - Number of Conversations: 2915


### Contact
Please email any questions to: yb299@cornell.edu (Sophie Bai)