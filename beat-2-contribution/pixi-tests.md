# Pixi build/test results

Date: 2026-11-18

## Outcome
Build SUCCEEDED and ctest PASSED.

- `ctest -j6`: 100% tests passed, 0 tests failed out of 4929
- Total test time: 128.67 sec (real)
- 1 test skipped (not a failure):
  `908 - StringTools.StringToDouble_LocaleIndependent (Skipped)`
- ctest exit code: 0

## Not covered
- Python wrapper tests (`build-python` / `test-python`, pytest) were not built or run.
- Debug/release variants (`test-debug`, `test-release`) were not built or run.

## Build history
- The first build stopped silently at step 4986/5651 with no `FAILED:` line.
  Cause: the kernel ran out of memory (OOM).
- Resumed with `ninja -j6` using the pixi ninja
  (`.pixi/envs/cxx/bin/ninja`, not on the default PATH; the first attempt failed
  with `ninja: command not found`, exit 127).
- The remaining 665 steps finished cleanly (exit 0, 0 `FAILED`, 0 warnings).

## Commands
```
cd build
PATH=<repo>/.pixi/envs/cxx/bin:$PATH ninja -j6
PATH=<repo>/.pixi/envs/cxx/bin:$PATH ctest -j6
```

## Logs
- Build: /tmp/claude-1000/-home-user-Documents-msu-725-vision-proj-Frequency-Aware-ESRT/6b053ecd-e036-4463-9048-34efc3667dfc/scratchpad/build2.log
- Tests: /tmp/claude-1000/-home-user-Documents-msu-725-vision-proj-Frequency-Aware-ESRT/6b053ecd-e036-4463-9048-34efc3667dfc/scratchpad/ctest.log
