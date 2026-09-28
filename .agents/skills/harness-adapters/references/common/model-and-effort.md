# Model and effort

Load this with the selected tool reference before choosing, validating, or changing either axis.
Add `references/common/dispatch.md` for configured profile precedence.

## Axes and precedence

`../../../bin/fm-spawn.sh` accepts concrete `--harness`, `--model`, and `--effort` values selected at intake; scripts never parse natural-language dispatch rules.
The tool reference records verified flags, accepted values, omission behavior, and discovery.

Effort precedence is a per-task captain instruction, then an applicable dispatch profile or secondmate pin, then the task's class default below.
Never replace either higher-precedence value.

This reference owns the class names, and `bin/fm-spawn.sh --effort-class <explicit|investigation>` applies a class's standing level.
The built-in table is `explicit=low` for well-understood work with an explicit bounded path and `investigation=xhigh` for ambiguous investigation or design.
Pass the class that matches the task and let the spawn fill in the level.
A middle level is not a class default: `medium`, `high`, `max`, and `ultra` still need an explicit `--effort` or a configured dispatch profile.
`$FM_HOME/config/crew-effort` overrides a class's level with one `<class>=<effort>` line per class, and `docs/configuration.md` "Crew effort classes" owns the format, the accepted classes, the accepted values, and how a captain changes them.
If an adapter lacks the resolved level, cap at its highest supported non-`max` level rather than silently omitting the intent.
Never select `max` through a class default; only an explicit per-task or standing captain preference permits it.

The explicit native `ultra` value follows the model-scoped refusal contract in `../../../bin/fm-harness.sh validate-native-effort`; it is never silently omitted or mapped to a Pi level.
For other values, if requested effort is outside the adapter's accepted set, the spawn records `effort=` in task metadata but emits no effort flag.
This preserves launch success instead of passing a known-bad value.
A harness with no verified interactive effort flag follows the same record-and-omit contract.

## Harness and provider identity

Harness identity is independent of model provider.
`harness=pi` with `model=xai/grok-*` is Pi using xAI, not standalone Grok Build, and does not require Grok CLI login.
`harness=cursor` with `model=cursor-grok-4.5-*` is Cursor routing a Grok model, not `harness=grok`.

No script resolves credential provenance for you.
Establish it from the tool's discovery surface and `quota-axi auth --json` per-provider sources, and show the reasoning rather than inferring it from a name.

## Discovery

Treat model and provider knowledge as current discovery, not a permanent namespace or mapping.
Use the selected tool reference's authoritative surface in the current authenticated environment because availability changes by version, account, and configuration.

For an unfamiliar namespace, establish support and provider identity from that harness's CLI help, model listing, or current documentation.
An account-reaching listing that omits a model is concrete unsupported evidence; block the candidate and quote it.
An unreachable surface establishes nothing; report uncertainty instead of a verdict.

For a matched profile array, return to `quota-array-dispatch` only after establishing every candidate's harness support, provider relationship, and uncertainty.
