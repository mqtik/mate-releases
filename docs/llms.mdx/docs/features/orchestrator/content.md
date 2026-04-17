# Orchestrator (/docs/features/orchestrator)



The Orchestrator lets you run multiple AI agent sessions in parallel, coordinated by a plan. Instead of sending tasks to one agent at a time, you define a set of tasks and the orchestrator distributes them across concurrent agent sessions, tracks progress, and handles retries.

## How it works [#how-it-works]

The orchestrator follows a straightforward model:

1. **Define tasks** — describe what needs to be done, broken into independent units of work
2. **Create a run** — the orchestrator schedules tasks and assigns them to agent sessions
3. **Monitor progress** — watch as agents work in parallel, with real-time status updates
4. **Review results** — see what each agent accomplished when the run completes

Each task runs in its own agent chat session. The orchestrator manages the lifecycle — starting sessions, sending prompts, monitoring for completion, and handling failures with automatic retries.

## Use cases [#use-cases]

* **Large refactors**: Split a codebase-wide change into file-by-file or module-by-module tasks
* **Parallel code reviews**: Have multiple agents review different parts of a PR simultaneously
* **Batch operations**: Run the same type of task across many files or repositories
* **Testing campaigns**: Generate tests for multiple modules in parallel

## Creating a run [#creating-a-run]

<Steps>
  ### Open the Orchestrator [#open-the-orchestrator]

  Click &#x2A;*+** in the tab bar and select **Orchestrator**.

  ### Define your tasks [#define-your-tasks]

  Add tasks with descriptions of what each agent should do. Each task should be independent — agents work in parallel without knowledge of what other agents are doing.

  ### Start the run [#start-the-run]

  The orchestrator creates agent chat sessions for each task and begins execution. You can watch progress in real time.

  ### Monitor and review [#monitor-and-review]

  Each task shows its status: pending, running, completed, or failed. Failed tasks are retried automatically with exponential backoff.
</Steps>

<Callout type="info">
  Tasks should be independent units of work. The orchestrator runs them in parallel, so tasks that depend on each other's output will not work well. Design your tasks so each agent can work without waiting for another.
</Callout>

## Task states [#task-states]

| State     | Meaning                                                      |
| --------- | ------------------------------------------------------------ |
| Pending   | Queued, waiting for an available agent session               |
| Running   | An agent is actively working on this task                    |
| Completed | The agent finished successfully                              |
| Failed    | The task failed — will be retried up to the configured limit |

## Concurrency [#concurrency]

The orchestrator manages how many agent sessions run simultaneously. This prevents overwhelming your machine with too many concurrent CLI processes. Tasks that exceed the concurrency limit are queued and start as earlier tasks complete.

## Retries [#retries]

When a task fails, the orchestrator retries it with exponential backoff. This handles transient issues like API rate limits or temporary network errors. You can configure the maximum number of retries per task.
