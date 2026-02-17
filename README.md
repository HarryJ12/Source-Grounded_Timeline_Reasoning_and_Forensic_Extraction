# SENTRY-FX

### Source-Grounded Timeline Reasoning and Forensic Extraction

### Input

Police-style incident reports (text)

### AI/NLP steps

- Clean the text
- Extract entities (names, locations, weapons)
- Categorize crime type
- Summarize key details

### Output

Structured intelligence-style report

This uses **pretrained models** like:

- Entity extraction ideas: GLINER
- Crime type categorization (classification) ideas: some HuggingFace transformer?
- Summarization: GPT

### FEATURES?

1. Source-grounded “facts table” (not prose):

Instead of (or before) a summary, output **atomic claims** with:

- **claim** (one fact)
- **who/what/where/when**
- **evidence snippet(s)** from the report
- **offsets** (character spans) so you can highlight in UI
- **confidence**
- **conflict flags** (contradicts another claim)

This is the difference between “here’s what it says” vs “here’s what we can *prove from the text*.”

**Example claim row**

- `claim`: “Victim was found in the kitchen.”
- `evidence`: “...located the victim lying on the kitchen floor...”
- `where (page number)`: [1022–1068]

If you can’t point to the text, you don’t get to assert it.

2. Timeline reconstruction (per incident + across incidents)

A narrative summary is fluff if the timeline is unclear.

Extract events with timestamps:

- dispatch time
- arrival time
- contact time
- escalation events
- evidence collected
- arrest time

If times are missing, infer only when explicitly indicated (“later that evening”) and mark as **approximate**.

3. “Analyst to-do” output: leads, gaps, contradictions

This is the killer feature.

Produce:

- **Unanswered questions** (missing victim age, unknown suspect description, unclear entry point)
- **Contradictions** (two different addresses, conflicting witness statements)
- **Next steps checklist** (camera canvass, phone ping, interview X, check prior calls at address)
- **Potential charges** (broad category, not legal advice; clearly marked)

This reduces rereading and gives direction.
