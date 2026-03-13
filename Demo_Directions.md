# Demo Directions

Step-by-step presenter walkthrough for the **Designing Custom Agents** demo. Each step includes what to do and what to say to the audience.

---

## Pre-Demo Setup

1. Ensure Node.js 18+ is installed
2. Ensure Claude Code is installed and authenticated
3. Open a terminal in the `devx-agents/` directory
4. Have the slide deck open if presenting alongside

---

## Part 1: Explore the Project Structure

**Goal:** Show the audience how custom agents are defined — both inline in `CLAUDE.md` and as standalone files in `.claude/agents/`.

### Step 1: Show the project files

```bash
ls -la
cat CLAUDE.md
```

**Notes:** "This is our project. The `CLAUDE.md` file is the main instruction file that Claude Code reads automatically. Notice we have two agent personas defined inline here — the **Security Reviewer** and the **API Architect**. These are just markdown sections with detailed system prompts."

### Step 2: Show the standalone agent files

```bash
ls .claude/agents/
cat .claude/agents/doc-writer.md
cat .claude/agents/test-strategist.md
```

**Notes:** "We also have two more agents defined as standalone files in `.claude/agents/`. The **Doc Writer** and **Test Strategist** live here. This is a second approach — instead of putting everything in CLAUDE.md, you can break agents into their own files. Claude Code discovers them automatically."

### Step 3: Show the task list

```bash
cat TASKS.md
```

**Notes:** "We use a `TASKS.md` file for spec-driven development. This tells Claude what to build and in what order. It's a pattern that works really well — you define the spec upfront, and Claude follows it step by step."

---

## Part 2: Build the API

**Goal:** Use Claude Code to build the Express API from the TASKS.md spec.

### Step 4: Start Claude Code and build

```bash
claude
```

Then prompt:

```bash
Complete Task 1 from TASKS.md — initialize the project and install dependencies. Tell me which agents you used for this task.
```

**Notes:** "We start by asking Claude to follow our task list. It reads TASKS.md, sees what needs to be done, and executes the steps."

### Step 5: Build the API

```bash
Complete Task 2 from TASKS.md — build the Task Management API in server.js. Tell me which agents you used for this task.
```

**Notes:** "Now Claude builds the actual API. It follows the spec in TASKS.md — the endpoints, the data model, the validation rules. This is spec-driven development in action."

### Step 6: Verify it works

```bash
Start the server and test it with a curl command. Tell me which agents you used for this task.
```

**Notes:** "Let's make sure it actually works before we bring in our agents."

---

## Part 3: Invoke the Custom Agents

**Goal:** Show how each agent persona produces specialized, structured output.

### Step 7: Security Review (inline agent)

```bash
Review server.js for security vulnerabilities. Tell me which agents you used for this task.
```

**Notes:** "Now watch what happens. Claude picks up the Security Reviewer persona from CLAUDE.md. Instead of a generic response, we get structured findings with severity levels, file locations, and specific remediation steps. This is the power of a well-designed agent prompt."

### Step 8: API Design Review (inline agent)

```bash
Review the API design of server.js. Tell me which agents you used for this task.
```

**Notes:** "Same idea, different agent. The API Architect evaluates our REST conventions, status codes, error handling, and gives us a design maturity rating. Notice the structured output format — that's defined in the agent prompt."

### Step 9: Test Strategy (standalone agent)

```bash
@test-strategist Design a test strategy for server.js. Tell me which agents you used for this task.
```

**Notes:** "Here we're invoking the Test Strategist using the `@agent` syntax. This agent lives in `.claude/agents/test-strategist.md`, not in CLAUDE.md. Claude Code discovers it automatically. It gives us prioritized test cases with the right mix of unit and integration tests."

### Step 10: Generate Documentation (standalone agent)

```bash
@doc-writer Generate API documentation for this project. Tell me which agents you used for this task.
```

**Notes:** "Finally, the Doc Writer agent. Again using the `@agent` syntax for a standalone agent. It produces complete, ready-to-use markdown documentation — not an outline, but actual docs with curl examples."

---

## Part 4: Wrap-Up

### Key Takeaways

1. **Two ways to define agents**: Inline in `CLAUDE.md` (good for project-specific agents) or standalone files in `.claude/agents/` (good for reusable agents across projects)
2. **Structured output**: Agent prompts should specify the exact output format you want
3. **Spec-driven development**: `TASKS.md` keeps Claude focused and on-track
4. **Composability**: You can invoke multiple agents in the same session on the same codebase

### Questions to Anticipate

- **"How does Claude know which agent to use?"** — It matches your prompt to the agent descriptions. You can also invoke standalone agents explicitly with `@agent-name`.
- **"Can I share agents across projects?"** — Yes, put them in `~/.claude/agents/` for global agents, or `.claude/agents/` for project-scoped agents.
- **"What about agent-to-agent handoffs?"** — Not built-in yet, but you can chain prompts manually (e.g., "Now review the code the Test Strategist suggested").
