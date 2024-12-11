
This is a fork of - https://github.com/Codium-ai/pr-agent with custom implementation

### [Documentation](https://pr-agent-docs.codium.ai/)

- See the [Usage Guide](https://qodo-merge-docs.qodo.ai/usage-guide/) for instructions on running Qode Merge PR-Agent tools via different interfaces, such as CLI, PR Comments, or by automatically triggering them when a new PR is opened.

- See the [Tools Guide](https://qodo-merge-docs.qodo.ai/tools/) for a detailed description of the different tools, and the available configurations for each tool.

### Commands

‣ **Auto Description ([`/describe`](https://pr-agent-docs.codium.ai/tools/describe/))**: Automatically generating PR description - title, type, summary, code walkthrough and labels.
\
‣ **Auto Review ([`/review`](https://pr-agent-docs.codium.ai/tools/review/))**: Adjustable feedback about the PR, possible issues, security concerns, review effort and more.
\
‣ **Code Suggestions ([`/improve`](https://pr-agent-docs.codium.ai/tools/improve/))**: Code suggestions for improving the PR.
\
‣ **Question Answering ([`/ask ...`](https://pr-agent-docs.codium.ai/tools/ask/))**: Answering free-text questions about the PR.

___

### How it works

The following diagram illustrates PR-Agent tools and their flow:

![PR-Agent Tools](https://codium.ai/images/pr_agent/diagram-v0.9.png)


### Configuration in Github Actions

In your workflow.yml 

```
- name: PR Agent action step
        id: pragent
        uses: neo-analytics-pr-agent@main
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          OPENAI.API_BASE: ${{ secrets.OPENAI_API_BASE }}
          OPENAI.KEY: ${{ secrets.OPENAI_KEY }}
          OPENAI.API_VERSION: ${{ secrets.OPENAI_API_VERSION }}
          OPENAI.DEPLOYMENT_ID: ${{ secrets.OPENAI_DEPLOYMENT_ID }}
          OPENAI.API_TYPE: "azure"

          # Below can be customised based on your needs
          
          github_action_config.auto_review: "true"
          github_action_config.auto_describe: "true"
          github_action_config.auto_improve: "true"
          github_action_config.pr_actions: "opened,reopened,ready_for_review,review_requested"
          github_action_config.comment_actions: "created,edited"

          pr_description.publish_labels: "false"
          pr_description.publish_description_as_comment: "true"
          pr_description.publish_description_as_comment_persistent: "true"
          pr_description.enable_help_text: "false"
          pr_description.enable_help_comment: "false"

          pr_reviewer.num_code_suggestions: "6"
          pr_reviewer.inline_code_comments: "true"
          pr_reviewer.enable_review_labels_effort: "false"
          pr_reviewer.enable_help_text: "false"

          pr_code_suggestions.num_code_suggestions_per_chunk: "6"
          pr_code_suggestions.commitable_code_suggestions: "true"
          pr_code_suggestions.enable_help_text: "false"
          pr_code_suggestions.max_number_of_calls: 5
```