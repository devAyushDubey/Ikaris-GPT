![IkarisGPT](https://github.com/devAyushDubey/Ikaris-GPT/assets/33064931/e1f3f73d-c1ab-44a2-9b61-ffdf96a60c26)
<br>
# IkarisGPT - Auto-Describe issues with ChatGPT 🤖
[![IkarisGPT Auto-Describe-Issue](https://github.com/devAyushDubey/Ikaris-GPT/actions/workflows/AutoDescribeIssue.yml/badge.svg)](https://github.com/devAyushDubey/Ikaris-GPT/actions/workflows/AutoDescribeIssue.yml) [![IkarisGPT](https://img.shields.io/badge/Marketplace-IkarisGPT-blue?logo=github)](https://github.com/marketplace/actions/ikarisgpt)

**Just write issue titles and let IkarisGPT do the rest.** <br>
IkarisGPT is a OpenAI API based Github Action that provides bootstrap issue templates with issue-specific details in a markdown format, saving time that goes in formatting and writing general information.

<br>

![Untitled video - Made with Clipchamp (1)](https://github.com/devAyushDubey/Ikaris-GPT/assets/33064931/4916bb55-343b-4e35-82ca-775453bf83c8)

## Usage
### Auto describe labelled issues
```yml
name: IkarisGPT Auto-Describe-Issue

on:
  issues:
    types:
      - labeled

jobs:
  AutoDescribe:
    if: github.event.label.name == 'auto-described'
    runs-on: ubuntu-latest
    name: IkarisGPT Auto Describe Issue
    steps:
      - name: IkarisGPT Action Step
        id: ikaris
        uses: devAyushDubey/Ikaris-GPT@v1.0
        with:
          openai-api-key: ${{ secrets.OPENAI_API_KEY }}
      - name: Get the output message
        run: echo "${{ steps.ikaris.outputs.message }}"
```

### Use Custom ChatGPT prompts
```yml
name: IkarisGPT Auto-Describe-Issue

on:
  issues:
    types:
      - labeled

jobs:
  AutoDescribe:
    if: github.event.label.name == 'auto-described'
    runs-on: ubuntu-latest
    name: IkarisGPT Auto Describe Issue
    steps:
      - name: IkarisGPT Action Step
        id: ikaris
        uses: devAyushDubey/Ikaris-GPT@v1.0
        with:
          openai-api-key: ${{ secrets.OPENAI_API_KEY }}
          prompt: "Generate an issue description for an issue titled ${{ github.event.issue.title }}"
      - name: Get the output message
        run: echo "${{ steps.ikaris.outputs.message }}"
```

## Action Inputs

| Name | Description | Default |
| --- | --- | --- |
| `token` | `GITHUB_TOKEN` (`issues: write`) or a `repo` scoped [PAT](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token). |  |
| `openai-api-key` | [OpenAI API Key](https://platform.openai.com/account/api-keys) for using ChatGPT, use Github Secrets and add the API Key in secrets like `OPENAI_API_KEY` which can be used in the workflow as `token: ${{ secrets.OPENAI_API_KEY }}`. While testing I used GPT-3.5-Turbo. |
| `prompt` | A ChatGPT `prompt` for generating a **markdown issue description** based on the specifics of the issue title and project. [ChatGPT Prompts](https://twelverays.agency/blog/what-are-chatgpt-prompts) | |

## Important
- The action won't work without a valid OpenAI Api Key that has $ credits (not expired, check here).
- Make sure `workflows have write permissions`. This can be enabled through repository settings > actions > workflow permissions.
![image](https://github.com/devAyushDubey/Ikaris-GPT/assets/33064931/63b752d1-5a96-4fc4-951b-7cdaed3ac8d9)

### Eagerly looking for contributors 👋

## License

[GNU](LICENSE)
