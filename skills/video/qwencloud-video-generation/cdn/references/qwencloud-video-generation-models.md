# QwenCloud Video Generation Models

> Catalog checked: 2026-10-20. Only models or dated snapshots released after 2025-09-01 are included.

## Defaults and recommendations

| Mode | Runtime default | Notes |
|------|-----------------|-------|
| Text-to-video (`t2v`) | `wan3.0-video` | Token Plan + PAYG; unified media protocol. |
| Image-to-video (`i2v`) | `happyhorse-1.1-i2v` | Token Plan + PAYG; first-frame input is preserved by the current request builder. |
| First-and-last-frame (`kf2v`) | `wan2.2-kf2v-flash` | Released 2025-09-12; PAYG-only; fixed 5s, silent; dedicated `kf2v` endpoint/payload. |
| Reference-based role-play (`r2v`) | `happyhorse-1.1-r2v` | Token Plan + PAYG. |
| Function-based editing (`vace`) | None (`null`) | No model meets the release cutoff for this payload; do not submit an implicit VACE request. |
| Prompt-driven editing (`videoedit`) | `wan2.7-videoedit` | PAYG-only; unified media protocol. |
| Character animation (`animate`) | `wan2.2-animate-move` | PAYG-only; image plus driving video. |

Never replace an explicitly selected model or silently change the requested mode because of plan restrictions.

No Qwen-branded video generation model is available in the current catalog. Wan 3.0 is the text-to-video default; image-to-video and the dedicated `r2v` runtime use HappyHorse 1.1.

Do not substitute `wan3.0-video` for the dedicated `kf2v` payload. For modern first-and-last-frame generation, explicitly select `wan3.0-video` or `wan3.0-video-prime` with `media` items of type `first_frame` and `last_frame`, using the compatible i2v route. Do not replace a function-based VACE request with `wan2.7-videoedit`: its media protocol does not preserve VACE mask, extension, or outpainting fields.

The current Wan 3.0 request builder does not convert `first_frame_url` or `last_frame_url` into media items; use explicit `media`. It also does not forward the `audio` parameter, so audio control requires a compatible API caller.

The consumer must support `null` as a disabled default for VACE. Older readers that require a nonempty model string reject it, including when `--help` reads every mode's default. Update such readers before using this configuration; a disabled VACE default must not restore an older fallback model.

## All-in-one and text-to-video

| Model | Capability | Important limits |
|-------|------------|------------------|
| `wan3.0-video` | All-in-one generation, references, editing, and extension | 2–30s; 480P–1080P; optional audio; Token Plan + PAYG. |
| `wan3.0-video-prime` | Faster Wan 3.0 tier | Same modes and flat request shape; PAYG-only. |
| `wan2.7-t2v` | Ratio control, automatic audio, long prompts | 720P/1080P; uses `resolution` + `ratio`. |
| `wan2.7-t2v-2026-06-12` | Wan 2.7 text-to-video snapshot | Same capabilities as `wan2.7-t2v`. |
| `wan2.7-t2v-2026-04-25` | Wan 2.7 text-to-video snapshot | Same capabilities as `wan2.7-t2v`. |
| `happyhorse-1.1-t2v` | Text-to-video with audio | 3–15s; 480P–1080P; Token Plan + PAYG. |
| `happyhorse-1.0-t2v` | Earlier HappyHorse text-to-video | Same request family as 1.1. |
| `wan2.6-t2v` | Audio and multi-shot narrative | 2–15s; 720P/1080P. |
| `wan2.5-t2v-preview` | Text-to-video with audio | 5s or 10s. |

Wan 3.0 first/last-frame media cannot be mixed with reference media, files, or links. With input video, input plus output duration must not exceed 30s. File/link input requires `prompt_extend=true`.

## Image, reference, and transition video

| Model | Mode | Important compatibility |
|-------|------|-------------------------|
| `wan2.7-i2v` | i2v | Unified media protocol for first/last frame, continuation, and audio sync. |
| `wan2.7-i2v-2026-04-25` | i2v | Snapshot with the same capabilities as `wan2.7-i2v`. |
| `happyhorse-1.1-i2v` | i2v | Exactly one first-frame reference; Token Plan + PAYG. |
| `happyhorse-1.0-i2v` | i2v | Earlier strict first-frame request format. |
| `wan2.6-i2v-flash`, `wan2.6-i2v` | i2v | Audio-capable, multi-shot, 2–15s. |
| `wan2.5-i2v-preview` | i2v | Audio; 5s or 10s. |
| `wan2.7-r2v` | r2v | Up to five mixed media references. |
| `wan2.7-r2v-2026-06-12` | r2v | Snapshot; up to five mixed image/video references. |
| `happyhorse-1.1-r2v` | r2v | Up to nine reference images; Token Plan + PAYG. |
| `happyhorse-1.0-r2v` | r2v | Earlier HappyHorse reference-video request family. |
| `wan2.6-r2v`, `wan2.6-r2v-flash` | r2v | Single/multi-character role-play; 2–10s. |
| `wan2.2-kf2v-flash` | kf2v | Dedicated first/last-frame payload; fixed 5s; silent; released 2025-09-12. |

## Editing and animation

| Model | Mode | Important compatibility |
|-------|------|-------------------------|
| `wan2.7-videoedit` | videoedit | Optional prompt and negative prompt; media protocol; up to four image references. |
| `happyhorse-1.0-video-edit` | videoedit | Prompt required; one video plus up to five image references. |
| `wan2.2-animate-move` | animate | Transfers actions/expressions from a driving video to a character image. |
| `wan2.2-animate-mix` | animate | Replaces the video subject with the subject from an image. |

Animation requests require `image_url`, `video_url`, and `mode` (`wan-std` or `wan-pro`) and do not accept prompt, resolution, duration, seed, or watermark parameters.

## Token Plan compatibility and billing

- `wan3.0-video`, `happyhorse-1.1-t2v`, `happyhorse-1.1-i2v`, and `happyhorse-1.1-r2v` support Personal and Team Token Plan.
- Dedicated `kf2v`, `videoedit`, and `animate` routes have no Token Plan model; use PAYG without silently changing the task. `vace` has no eligible model in this catalog.
- Video output is billed per generated second; rates vary by model and resolution, and reference/editing calls may also bill input-video duration.
