# QwenCloud Text Models

> Scope: recent Qwen general-purpose text and multimodal models released after the `2025-09-01` cutoff and still named by the trusted sources below. This is not a complete catalog of coding, translation, or third-party text models; use the QwenCloud CLI or the model-selector cross-domain catalog for those families. Release notices and dated snapshots establish the cutoff evidence.

## Default

- Default model: `qwen3.8-max`.
- It is the newest production Max model that is available through both PAYG and Token Plan Personal/Team. Since 2026-09-05, the rolling ID maps to `qwen3.8-max-0902`. Use the rolling ID: Token Plan uses an exact-string allowlist and does not list the snapshot ID.
- Do not replace a model explicitly selected by the user. If the selected model is unavailable under the active billing plan, report the mismatch.

## Current model families

| Production model ID | Post-cutoff evidence in the current sources | Supported input / role | Token Plan Personal | Token Plan Team |
|---|---|---|---:|---:|
| `qwen3.8-max` | Released 2026-08-03; current snapshot `qwen3.8-max-0902` released 2026-09-02. | Text, code, image, and video; 1M context; thinking and tool use. | Yes | Yes |
| `qwen3.8-flash` | Released 2026-08-26. | Fast text, code, image, and video model; 1M context; OpenAI- and Anthropic-compatible. | Yes | Yes |
| `qwen3.7-max` | Released 2026-05-21; snapshots `qwen3.7-max-2026-05-20` and `qwen3.7-max-2026-06-08`. | Reasoning and text generation; the June snapshot adds vision. Token Plan lists text capabilities. | Yes | Yes |
| `qwen3.7-plus` | Released 2026-06-01; snapshot `qwen3.7-plus-2026-05-26`. | Reasoning, visual understanding, and text generation. | Yes | Yes |
| `qwen3.7-flash` | Released 2026-07-25; snapshot `qwen3.7-flash-2026-07-15`. | Current fast Qwen3.7 API model. | No | No |
| `qwen3.6-plus` | Released 2026-04-02; snapshot `qwen3.6-plus-2026-04-02`. | Reasoning, visual understanding, and text generation. | No | Yes |
| `qwen3.6-flash` | Released 2026-04-16; snapshot `qwen3.6-flash-2026-04-16`. | Reasoning, visual understanding, and text generation. | Yes | Yes |
| `qwen3.5-plus` | Snapshots `qwen3.5-plus-2026-02-15` and `qwen3.5-plus-2026-04-20`. | General multimodal text generation. | No | No |
| `qwen3.5-flash` | Snapshot `qwen3.5-flash-2026-02-23`. | Fast multimodal text generation. | No | No |

`Yes` above means that the exact rolling ID appears in the corresponding Token Plan allowlist. Snapshot IDs are PAYG/API identifiers and are not Token Plan-compatible unless that exact snapshot string is also listed.

`qwen3.5-plus` and its two listed snapshots retire on 2027-01-19; use `qwen3.8-flash` for new deployments.

## Selection guidance

| Need | Model | Source-backed reason |
|---|---|---|
| Default or highest-capability work | `qwen3.8-max` | Latest upgraded Max generation, multimodal, 1M context, and supported by PAYG plus both Token Plans. |
| Faster current-generation work | `qwen3.8-flash` | Officially described as the fast latest-generation multimodal model; also supported by both Token Plans. |
| Text reasoning | `qwen3.7-max` | Token Plan classifies it for reasoning and text generation. |
| Team-only balanced fallback | `qwen3.6-plus` | Available on PAYG and Team, but absent from the Personal exact-string allowlist. |

## Thinking defaults

| Model | Thinking default | Notes |
|---|---|---|
| `qwen3.8-max`, `qwen3.8-flash` | On | Thinking enabled by default. |
| `qwen3.7-max`, `qwen3.7-plus`, `qwen3.7-flash` | On | Thinking enabled by default. |
| `qwen3.6-plus` | On | Thinking enabled by default. |
| `qwen3.6-flash` | Service default | Official guides differ; omit `enable_thinking` unless explicitly requested. |
| `qwen3.5-plus`, `qwen3.5-flash` | On | Thinking enabled by default. |
| `qwen3.8-27b`, `qwen3.8-omni-flash` | On | Hybrid thinking; preserve the model default unless explicitly overridden. |
| `qwen3.8-2.4t-a95b` | Always on | Thinking-only; streaming is required. |

Preserve each model's default. Do not set `enable_thinking` unless the user explicitly asks to change it, and do not disable thinking merely because a task looks simple. Thinking-only models cannot disable thinking.

## Compatibility and limits

- All general-purpose text-generation models support function calling. For GLM models, `tool_stream` controls whether tool-call arguments are returned incrementally when `stream: true`; it defaults to true for `glm-5.3` and false for the other listed GLM models. With `stream: false`, it has no effect.
- `thinking_budget` is supported by Qwen3.8, Qwen3.7, Qwen3.6, Qwen3.5, Qwen3-VL, GLM, Kimi (except `kimi-k3`), and Qwen3.8 open-source models in Chat Completions and DashScope, but not in the Responses API.
- For `qwen3.8-max`, `reasoning_effort` supports `low`, `medium`, and `xhigh` and defaults to `xhigh`. Do not set `reasoning_effort` and `thinking_budget` together for Qwen3.8 Max, Flash, Omni-Flash, or the listed open-source variants.
- Thinking tokens are billed as output tokens.
- Current API-only variants include `qwen3.8-27b` (released 2026-08-19; hybrid thinking, on by default), `qwen3.8-2.4t-a95b` (released 2026-08-13; thinking-only and streaming required), and `qwen3.8-omni-flash` (released 2026-09-18; hybrid thinking, on by default; text output only). They are not Token Plan models.

Verified: 2026-10-20.
