<details><summary>Learning Objectives</summary>

After completing this module, learners will be able to:

- Explain what it means for an AI tool to be integrated into an IDE.
- Identify common features provided by IDE integrated AI tools beyond basic code completion.
- Configure basic settings for an AI tool within a development environment.
- Scope a request to a selection or a file so the tool has the right context.
- Recognize how to keep AI assistance from interrupting an existing development workflow.

</details>

<details><summary>Description</summary>

## What IDE Integration Means

An Integrated Development Environment, or IDE, is the software developers use to write, run, and debug code, such as Visual Studio Code, PyCharm, or similar tools. AI tools like Copilot, covered in the previous module, are typically distributed as extensions or plugins that integrate directly into these environments, rather than existing as a separate, standalone application a developer has to switch to.

This integration is significant because it places AI assistance directly in the context where a developer is already working, rather than requiring them to copy code out to a separate tool, describe the problem again, and copy a result back in.

---

## Common Features Beyond Code Completion

Beyond suggesting code as a developer types, IDE integrated AI tools commonly provide:

- **Inline chat**: The ability to ask a question or request a change directly within the editor, often referencing the currently open file or selected code, without switching to a separate window.
- **Code explanation on demand**: Selecting a block of code and requesting a plain language explanation, directly within the editor.
- **Refactoring suggestions**: Requesting a specific structural change to existing code, such as simplifying a function or extracting repeated logic into a reusable piece.
- **Error and warning assistance**: Some tools can explain an error message or a failing test directly in context, suggesting a possible fix based on the surrounding code.

---

## Configuring Basic Settings

Most IDE integrated AI tools provide configuration options worth reviewing when first setting one up, including:

- Which files or file types the tool is allowed to access as context, which connects directly to the data privacy and security considerations covered earlier in this section, particularly for a project containing sensitive or proprietary code.
- How aggressively the tool offers suggestions, since some developers prefer frequent inline suggestions while others prefer to request help only when explicitly asked.
- Whether the tool is permitted to send code externally for processing, which should be reviewed against an organization's specific data handling policies before enabling on any project containing confidential code.

---

## Scoping a Request

The most common reason an inline request produces a poor answer is that the tool was not given the right context. Integrated tools generally work from one of three scopes:

- **The current selection**, when text is highlighted before asking. This is the narrowest and usually the most accurate, since the request is unambiguous.
- **The current file**, when nothing is selected. Useful for questions about how a file fits together.
- **The wider project**, which some tools support for questions spanning several files, though coverage varies and is rarely complete for a large codebase.

Selecting the relevant function before asking about it is a small habit that noticeably improves the quality of the response, for the same reason that providing context improves any prompt.

```text
Weak:   "Why is this slow?"                  (nothing selected, whole file as context)
Better: [select the function] "Why is this slow?"
Best:   [select the function] "This is called once per row in a loop over
        about 50,000 records. Why is it slow, and what would you change?"
```

The third version adds the one thing the tool cannot see from the code alone: how it is actually used.

---

## Keeping AI Assistance From Disrupting Workflow

While these tools are designed to integrate smoothly, it is worth being deliberate about how they are used, rather than accepting every suggestion reflexively out of habit. A useful practice is treating frequent inline suggestions the same way a developer would treat a colleague's frequent comments, useful and worth considering, but not something to accept automatically without a moment of actual evaluation, consistent with the review habits covered throughout this section on AI pair programming and responsible usage.

</details>

<details><summary>Real World Application</summary>

## Adopting AI Tooling on an Existing Team

A development team introducing an IDE integrated AI tool typically starts by configuring it conservatively, restricting its access to sensitive files and reviewing its data handling settings, before rolling it out broadly. Developers are encouraged to use its inline chat and explanation features when working with unfamiliar code, and to use its inline refactoring suggestions as a starting point, reviewing each proposed change rather than accepting it directly. Over time, teams often refine their configuration and usage habits based on where the tool has proven genuinely useful versus where it required more correction than it saved, treating adoption as an ongoing, evaluated process rather than a one time setup.

</details>

<details><summary>Implementation</summary>

## Configuring Extension Settings

Most editors store extension settings in a configuration file.

```json
{
    "aiAssistant.enable": {
        "*": true,
        "plaintext": false,
        "markdown": false
    },
    "aiAssistant.inlineSuggest.enable": true
}
```

Disabling suggestions for certain file types reduces noise in files where they are not useful.

## Excluding Sensitive Files

```text
# Files the assistant should not read as context
.env
secrets/
config/production.yml
*.pem
```

Reviewing which files a tool can access is part of the security practice covered earlier in this section.

## Using Inline Chat

Inline chat is invoked with a keyboard shortcut, which varies by editor and is worth locating early since it is the feature used most often.

```text
Select code, then invoke inline chat and type a request:

"Explain what this does, in two sentences."
"Rename the variables here to something more descriptive."
"Add a docstring describing the parameters and return value."
"Why would this raise a KeyError?"
```

The response appears in context, and edits are proposed as a diff to accept or reject rather than applied directly.

---

## Explaining Unfamiliar Code

One of the strongest everyday uses is understanding code nobody on the team wrote recently.

```text
[select the function]

"Explain this function in plain language. What are its inputs and
outputs, what does it assume about the data, and what happens if
that assumption does not hold?"
```

Asking about assumptions, rather than only what the code does, tends to surface the fragile parts that a straight description would skip over. The explanation still needs checking against the code itself, for the reasons covered earlier in this section.

---

## Steps to Follow

1. Install the extension and review its default settings.
2. Configure which file types receive suggestions.
3. Exclude files containing credentials or sensitive configuration.
4. Select the relevant code before asking, so the request is scoped precisely.
5. Use inline chat for explanations, renaming, and small refactors, reviewing each proposed diff before accepting it.

</details>

<details><summary>Summary</summary>

In this module, we learned:

- IDE integrated AI tools place assistance directly within a developer's existing environment rather than a separate application.
- Common features include inline chat, code explanation, refactoring suggestions, and error assistance.
- Configuration settings control what context a tool can access and whether code is sent externally for processing.
- Scoping a request to a selection, and stating how the code is actually used, produces markedly better responses.
- Deliberate, evaluated use of AI assistance keeps these tools productive without disrupting an existing development workflow.

With IDE integration covered, the next module looks at AI pair programming and working alongside a tool such as Copilot.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>