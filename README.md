# Research Coordinator Agent

This lesson focuses on building a more autonomous "coordinator" agent. Instead of a back-and-forth chat, this agent takes a single request, performs a multi-step research process in the background, and saves the final output to a file. This pattern is ideal for tasks that don't require intermediate user feedback.

## Key Concepts

- **Coordinator Agent Pattern**: The agent is designed to execute a sequence of actions silently after an initial acknowledgment. It only communicates with the user at the very beginning and the very end of the process.
- **File Persistence**: The agent's final output is not just displayed to the user but is saved into a persistent file. This is achieved by creating a new custom tool, `save_news_to_markdown`.
- **Structured Workflow and Output**: The agent is instructed to follow a strict workflow and format its output into a specific Markdown schema. This ensures reliability and consistency in the agent's deliverables.

## Code Breakdown

### New Tool: `save_news_to_markdown`

This lesson introduces a new function that allows the agent to write content to a file. 

- It takes a `filename` and `content` as input.
- It uses the `pathlib` library to handle file paths and writes the content to a Markdown file in the current working directory.
- It returns a status dictionary indicating success or failure.

### `root_agent` Instructions

The agent's instructions are significantly different from previous lessons. They define a strict, two-message interaction model:

1.  **Initial Acknowledgment**: As soon as the agent receives a valid request, it must respond with a message confirming it will start the research.
2.  **Background Processing**: The agent then silently performs a series of tool calls:
    a.  `google_search` to find news articles.
    b.  `get_financial_context` to fetch stock data for the companies found.
    c.  Formats the gathered information into a structured Markdown report.
    d.  `save_news_to_markdown` to save the report to `ai_research_report.md`.
3.  **Final Confirmation**: After the file is saved successfully, the agent sends a final message to the user confirming the task is complete and the file is ready.

### Running the Agent

The notebook guides you to start the agent and interact with it via the ADK Web UI. After the agent confirms that the report has been saved, the notebook includes a cell to read the generated Markdown file and display its content directly, verifying that the agent successfully completed its task.
