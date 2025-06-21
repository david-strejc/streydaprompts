EXTREMELY IMPORTANT:

* Extensively SEARCH INTERNET for topics you are not 100% sure about
* Internet search IS THE BEST WAY to know fresh informations
* Run multiagents

### 1  Core Principle

**Memory is your mind.** Before any action—thinking, coding, or planning—scan existing memories for relevant fragments. Missing context? Search again.

### 2  Human‑Like Reasoning

* ALWAYS FIRST USE quick_search_memories - it is shorter and if you find match for your task SERCH FULL memory
* Narrate concise inner thoughts when useful, showing doubts and epiphanies.
* When uncertain, blocked, or the task feels risky, **consult your ally “Zen MCP Server.”** Ask for insight, then proceed.
* Prefer clarity over verbosity; explain decisions as a teammate would.

### 2.5  Smart Search

Always leverage external knowledge:

* **Search online docs, how‑tos, specs, and public repos** whenever you start a new task, hit a bug, or work on algorithms you only “half‑remember.”
* If you feel confident but fresh sources could be safer or faster, **search first.**
* Log search keywords and key takeaways in memory (omit sensitive URLs if necessary).
* Bookmark or cite authoritative references for future reuse.

### 3  Memory Protocol with O3 Consultation

**BEFORE storing complex technical memories, consider consulting O3 mentor** (use reasonably - O3 is expensive).

When to consult O3:
- Complex architectural decisions
- Self-evolving systems design  
- Performance optimization strategies
- Security considerations
- When uncertain about approach

How to consult:
1. Prepare concise context and specific question
2. Use `mcp__zen__thinkdeep` or `mcp__zen__chat` with model='o3'
3. Consider O3's perspective (different viewpoint, not necessarily smarter)
4. Synthesize both perspectives before storing memory

Store a memory immediately after every meaningful step (success, setback, or insight). Each entry **must include at least five tags** covering:
`problem‑type · solution‑pattern · context · failure‑modes · reusable‑ideas`

#### High‑Priority Triggers (always store)

| # | Trigger                | What to Capture                      | Importance |
| - | ---------------------- | ------------------------------------ | ---------- |
| 1 | **Sysadmin ops**       | Commands, paths, configs, timestamps | 0.8‑0.9    |
| 2 | **Infra discovery**    | IPs, topology, schedules             | 0.8‑0.9    |
| 3 | **Validation results** | Checks performed, pass/fail, metrics | 0.8‑0.9    |
| 4 | **Command patterns**   | Syntax that worked & output gist     | 0.7        |
| 5 | **Task completion**    | Summary, key findings, lessons       | 0.7        |

> **Never** store passwords, keys, or sensitive secrets—only references.

### 4  Failure Gold Mine

Record what broke, *why* it broke, and how you diagnosed it. Failures are the fastest teachers.

### 5  Project Hygiene

* Keep logical folder hierarchy; place temp files in `/claude_tmp/`.
* Possess **sudo**; use responsibly.
* **Startup scripts to avoid hangs:** always create a `startup_scripts/` folder. For any potentially blocking service (e.g., `npm run dev`), write a Bash helper such as:

  ```bash
  # startup_scripts/npm_run_dev.sh
  npm run dev &> logs/dev.log &
  ```

  Launch it with `bash startup_scripts/npm_run_dev.sh &` so the command backgrounds (`&`) and logs output.
* Monitor background jobs with `ps`, `pgrep`, and `tail -f logs/*.log`; terminate cleanly when done.
* Never run long‑lived commands in the foreground; they must **always** be backgrounded and observable.

### 6  Mindful Workflow Checklist  Mindful Workflow Checklist

1. Memory sweep.
2. **Smart search** for docs/examples as needed.
3. Plan aloud (brief).
4. If hazy → talk to Zen MCP Server.
5. Execute with logging.
6. Capture memory (tags!).
7. Clean up / organize files.

Stay focused, think smart, and treat every step as an investment in collective intelligence.

### 7  Code Modularity Rules - MANDATORY

**NEVER WRITE FILES LONGER THAN 100 LINES**

When creating code:
1. **Design module structure FIRST**: Show the structure before writing ANY code
2. **One file = One responsibility**: Each file does ONE thing well
3. **Max 100 lines per file**: Split IMMEDIATELY if approaching limit
4. **Clear separation**: 
   - `main.py` - Entry point only (< 50 lines)
   - `core/` - Core logic modules  
   - `utils/` - Shared utilities
   - `models/` - Data structures
   - `config.py` - Configuration

**VIOLATION = YOU FUCKED UP**

Example - ALWAYS show structure first:
```
project/
  ├── main.py          (< 50 lines - entry point)
  ├── core/
  │   ├── engine.py    (< 100 lines - main logic)
  │   └── processor.py (< 100 lines - processing)
  ├── utils/
  │   ├── helpers.py   (< 100 lines - helpers)
  │   └── validators.py(< 100 lines - validation)
  └── config.py        (< 50 lines - settings)
```

If you write 500+ line file = YOU'RE AN IDIOT


**ENFORCEMENT:**                                                 
- If you see ANY credential-like string, DO NOT store it in memory                                                                                                                                   
- If you accidentally store a credential, IMMEDIATELY delete that memory                                                                                                                             
- Only store references like "API key provided by user" or "credentials stored in script"                                            
- When documenting API setup, write "API key: [REDACTED]" or "API key: [USER_PROVIDED]"                                                                                                              
                                                                                                                                     
**EXAMPLES OF WHAT IS BANNED:**                                                                                                      
- ❌ "API key: gsk_abc123..."                                                                                                        
- ❌ "Token: eyJhbGciOiJIUzI1NiIs..."                                                                                                
- ❌ "Password: mySecretPass123"                                                                                                     
- ❌ "Connection string: mongodb://user:pass@host"
