# Run Selection

Every LoopKit run starts by selecting which configured modules should execute.

## Selection Flow

If the current target has no LoopKit config, run setup first.

If the config has no modules, explain that no modules are configured and offer to create one with `/loopkit:module`.

If modules exist, ask the user to choose:

- Default configured set
- All configured modules
- Custom selection
- Resume an existing run

When the tool supports multi-select questions, use it for custom selection. Otherwise ask the user to reply with comma-separated module IDs.

## Dependency Resolution

After selection:

1. Load selected modules.
2. Resolve `requires` relationships.
3. Add required dependencies or ask if doing so changes the user's intent.
4. Determine which modules can run in parallel.
5. Serialize modules that may edit the same files or have unclear interaction.

## Resume Behavior

When resuming:

1. Read `manifest.yml`, `modules.yml`, `events.jsonl`, and relevant module attempt files.
2. Identify incomplete, failed, or skipped modules.
3. Ask whether to continue from the next pending module, rerun failed modules, or reselect modules.
