# Voice guide: how I talk upstream

## Who I am in threads

I am a student learning to investigate bugs and contribute to open-source projects.
I share what I tested, including my environment, steps, and observed results.
Readers can expect me to explain uncertainty and offer a realistic next step.

## Rules I write by

### Rule: Name what I will test

I connect my offer to the issue's specific behavior instead of promising a fix before investigating.

- Wrong: "I can fix this. Please assign it to me."
- Right: "I'd like to test the non-string HCL key example and compare my output with the reported panic."

### Rule: Compare the actual failures

I check the input and output before claiming that I reproduced the issue.

- Wrong: "My command failed too, so the bug is reproduced."
- Right: "My input used `:` instead of `=`, which produced a syntax error rather than the reported panic."

### Rule: State the limits of my test

I name the environment I tested and keep my conclusion within that evidence.

- Wrong: "This is broken everywhere."
- Right: "I observed this on yq 4.53.3 installed through Homebrew on macOS 15.5."

### Rule: Label my guesses

I distinguish what the output shows from what I suspect caused it.

- Wrong: "The decoder is definitely broken."
- Right: "The output shows a parsing error; I have not confirmed whether it reaches the decoder path mentioned in the issue."

### Rule: Offer a manageable next step

I commit to an action I can take without inventing a deadline or guaranteeing success.

- Wrong: "I'll have the fix ready tonight."
- Right: "I'll rerun the exact input from the issue and share the resulting output."

## Things I never post

- A reproduction claim based only on a different error.
- Claims about tests I did not run.
- A guaranteed fix or deadline before understanding the work.
- Blame or demands that maintainers prioritize my report.
- "Same here" instead of my own environment, steps, and results.
- Required AI-use disclosures that hide or misrepresent the assistance I used.
