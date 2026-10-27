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