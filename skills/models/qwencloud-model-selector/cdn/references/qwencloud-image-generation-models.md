# QwenCloud Image Generation Models

> Catalog checked: 2026-10-20. Only models or dated snapshots released after 2025-09-01 are included.

## Defaults and recommendations

- General default: `qwen-image-3.0-pro`.
- General image-to-image/editing default: `qwen-image-3.0-pro`.
- Dedicated Wan2.5 image-to-image endpoint default: `wan2.5-i2i-preview`; this compatibility route is PAYG-only.
- Use `qwen-image-3.0-pro` through the general generation route for new requests.
- Image-translation default: `qwen-mt-image-2.0`; image translation currently has no Token Plan model.
- When no model was explicitly selected, do not choose `wan2.6-image` for pure text-to-image; it needs reference images or interleaved-output mode.
- Never replace a model explicitly selected by the user; explain an incompatible request and let the user decide.

| Scenario | Recommended model | Notes |
|----------|-------------------|-------|
| General text-to-image or editing | `qwen-image-3.0-pro` | Runtime default; flagship available on both PAYG and Token Plan. |
| Highest-quality Wan output | `wan2.7-image-pro` | Up to 4K text-to-image and 2K editing. |
| Dedicated text-to-image | `wan2.6-t2i` | Synchronous and asynchronous calls. |
| Open-source generation or editing | `qwen-image-2.1-turbo` | Supports transparent output; no `negative_prompt`; PAYG. |
| Image editing / style transfer | `qwen-image-3.0-pro` | Default; accepts 1–3 input images and returns up to 6 outputs. |
| Subject consistency or multi-image composition | `qwen-image-3.0-pro` or `qwen-image-2.1-pro` | 3.0 accepts 1–3 references; 2.1 accepts up to 10 and supports transparent output. |
| Straightforward image-to-image fusion | `qwen-image-3.0-pro` | Default; use `wan2.5-i2i-preview` only when its dedicated async request format is required. |
| Posters and strong text rendering | `qwen-image-3.0-pro` or `qwen-image-3.0` | Fused generation and editing. |
| Precise bilingual text or element editing | `qwen-image-3.0-pro`, `qwen-image-3.0`, or `qwen-image-2.0-pro` | Qwen Image family for text and layout work. |
| Fast drafts | `qwen-image-3.0` or `qwen-image-2.1-turbo` | Current faster Qwen choices. |
| Custom resolutions | `qwen-image-3.0-pro` or `qwen-image-2.1-pro` | Total pixels from 512×512 to 2048×2048; aspect ratio from 1:8 to 8:1. |
| Image translation | `qwen-mt-image-2.0` | 55 languages; synchronous or asynchronous; no prompt. |

## Wan series

| Model | Capability | Important limits |
|-------|------------|------------------|
| `wan2.7-image-pro` | Multi-function generation/editing, sequential output, interactive editing, thinking, and color palette | 0–9 references; 4K text-to-image, 2K editing. |
| `wan2.7-image` | Faster multi-function generation/editing, sequential output, interactive editing, thinking, and color palette | 0–9 references; up to 2K. |
| `wan2.6-t2i` | Dedicated text-to-image | Sync and async; prompt up to 2,100 characters. |
| `wan2.6-image` | Editing, subject consistency, composition, interleaved output | Not pure text-to-image; 1–4 editing references; prompt up to 2,000 characters. |
| `wan2.5-i2i-preview` | General image editing and multi-image fusion | 1–3 references; async-only. |
| `wan2.5-t2i-preview` | Flexible-resolution preview generation | PAYG. |

For `wan2.7-image-pro` and `wan2.7-image`, non-sequential output supports 1–4 images and sequential output supports 1–12 images.

## Qwen Image series

| Model | Capability | Important limits |
|-------|------------|------------------|
| `qwen-image-3.0-pro` | Flagship generation, strong text rendering, and 1–3-reference editing | 1–6 outputs; size is automatically recommended from the prompt; Token Plan + PAYG. |
| `qwen-image-3.0` | General-purpose generation and 1–3-reference editing with strong text rendering | 1–6 outputs; size is automatically recommended from the prompt; PAYG. |
| `qwen-image-2.1-pro` | Unified generation/editing with native transparent output | Up to 10 references, 1–6 outputs, up to 2K; no `negative_prompt`; PAYG. |
| `qwen-image-2.1-turbo` | Faster, cost-effective open-source generation/editing with transparent output | Up to 10 references, 1–6 outputs, up to 2K; no `negative_prompt`; PAYG. |
| `qwen-image-2.0-pro` | High-quality fused generation and editing | 1–3 inputs, 1–6 outputs; Team Token Plan + PAYG. |
| `qwen-image-2.0` | Faster fused generation and editing | 1–3 inputs, 1–6 outputs; Team Token Plan + PAYG. |

Current dated snapshot IDs documented by the API are:

- `qwen-image-2.0-pro-2026-06-22`, `qwen-image-2.0-pro-2026-04-22`, and `qwen-image-2.0-pro-2026-03-03`.
- `qwen-image-2.0-2026-03-03`.

For `qwen-image-3.0-pro` and `qwen-image-3.0`:

- `enable_thinking` defaults to true, is effective only when `prompt_extend=true`, and is unavailable in image-to-image Agent mode.
- `prompt_extend_mode` defaults to `direct` (DPE); `agent` (APE) is for finer rewriting in text-to-image mode.
- `size` is automatically recommended from the prompt when omitted. Supported total pixels range from 512×512 to 2048×2048 with an aspect ratio from 1:8 to 8:1.
- `n` supports 1–6 outputs. Recommended prompt length is at most 4,500 tokens; the Qwen Image 2.0 series recommendation is 1,300 tokens.

The Qwen Image 2.1 API supports up to 10 references, but the bundled `scripts/image.py` currently accepts at most 3 Qwen reference images. Requests with 4–10 references require a caller that supports the API limit. Do not pass `negative_prompt` to either 2.1 model.

For `qwen-image-2.1-pro`, the current request builder does not forward `enable_thinking` or `prompt_extend_mode`. Use a compatible API caller to override thinking or select Agent prompt rewriting.

## Other models

| Model | Capability | Important limits |
|-------|------------|------------------|
| `z-image-turbo` | Open-source 6B text-to-image model with eight-step inference | Sync-only; single text content; no `n` or references; server-default size is `1024*1536`. |
| `qwen-mt-image-2.0` | Image translation | 55 languages with no source/target-language restriction; synchronous and asynchronous calls; `image_url`, `source_lang`, and `target_lang`; no prompt. |

The image-translation API supports synchronous and asynchronous calls. The bundled `scripts/image.py` currently implements only the asynchronous submission-and-polling route for image translation.

## Token Plan compatibility and billing

- Personal and Team: `wan2.7-image`, `wan2.7-image-pro`, `qwen-image-3.0-pro`.
- Team only: `qwen-image-2.0`, `qwen-image-2.0-pro`.
- All other models above require PAYG in the current catalog.
- Token Plan does not support local file upload; provide public HTTPS references.
- Generated images are billed per output image; image input may also be billable for some models.
