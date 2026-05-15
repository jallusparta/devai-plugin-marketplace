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
4. Build the execution order from the config's top-level `modules:` order by default. This registration order is the canonical default order for configured modules.
5. If the user selects extra modules that are not part of the default preset, insert them into the ordered module list at the semantically correct position instead of appending them blindly. Use module purpose, `requires`, and any user-provided workflow intent to place them.
6. Keep `requires` minimal and semantic. Do not add dependencies just to force ordering when the selected `modules.yml` order can express that a module should run later in this run.
7. If two valid insertion points exist, ask one short question instead of guessing.
8. Determine which modules can run in parallel.
9. Serialize modules that may edit the same files or have unclear interaction.

## Ordering Examples

For a TDD flow added to a normal implementation run:

- `tdd-red-tests` should usually run after `implementation-plan` and before `implementation`.
- `tdd-green-tests` should usually run after `implementation` and after any selected review, cleanup, lint, or diagnostics modules that the user wants before green verification.
- `tdd-green-tests` should still only require the modules it semantically needs, such as `tdd-red-tests` and `implementation`; later placement can be represented by the selected run order.

Example selected order:

```yaml
selected_modules:
  - id: intake
  - id: implementation-plan
  - id: tdd-red-tests
  - id: implementation
  - id: integration-review
  - id: boy-scout-cleanup
  - id: lint
  - id: lsp-diagnostics
  - id: tdd-green-tests
  - id: final-report
```

## Resume Behavior

When resuming:

1. Read `manifest.yml`, `modules.yml`, `events.jsonl`, and relevant module attempt files.
2. Identify incomplete, failed, or skipped modules.
3. Ask whether to continue from the next pending module, rerun failed modules, or reselect modules.
