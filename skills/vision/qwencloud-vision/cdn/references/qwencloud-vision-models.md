# QwenCloud Vision Models

> Scope: models released after the `2025-09-01` cutoff and still named by the trusted sources below. Release notices and dated snapshots establish the cutoff evidence.

## Defaults

| Task | Runtime default | Reason |
|---|---|---|
| Image or video understanding | `qwen3.8-max` | Newest production Max generation; PAYG and Token Plan Personal/Team. |
| Visual reasoning | `qwen3.8-max` | Supports reasoning and visual understanding under both billing modes. |
| OCR | `qwen3.8-max` | Cross-plan default. Use a dedicated OCR model only when PAYG is available and the user chooses it. |

Token Plan uses an exact-string allowlist. Use `qwen3.8-max`, which maps to `qwen3.8-max-0902` since 2026-09-05; the snapshot ID itself is PAYG only.

## Current model families

| Model ID | Post-cutoff evidence in the current sources | Primary use | Token Plan Personal | Token Plan Team |
|---|---|---|---:|---:|
| `qwen3.8-max` | Released 2026-08-03; current snapshot `qwen3.8-max-0902` released 2026-09-02. | Highest-capability text, image, and video understanding; 1M context. | Yes | Yes |
| `qwen3.8-flash` | Released 2026-08-26. | Faster text, image, and video understanding; 1M context. | Yes | Yes |
| `qwen3.7-plus` | Released 2026-06-01; snapshot `qwen3.7-plus-2026-05-26`. | General multimodal understanding and reasoning. | Yes | Yes |
| `qwen3.7-flash` | Released 2026-07-25; snapshot `qwen3.7-flash-2026-07-15`. | Faster multimodal work. | No | No |
| `qwen3.6-plus` | Released 2026-04-02; snapshot `qwen3.6-plus-2026-04-02`. | General multimodal understanding and reasoning. | No | Yes |
| `qwen3.6-flash` | Released 2026-04-16; snapshot `qwen3.6-flash-2026-04-16`. | Faster multimodal work. | Yes | Yes |
| `qwen3.5-plus` | Snapshots `qwen3.5-plus-2026-02-15` and `qwen3.5-plus-2026-04-20`. | General multimodal understanding. | No | No |
| `qwen3.5-flash` | Snapshot `qwen3.5-flash-2026-02-23`. | Faster multimodal understanding. | No | No |
| `qwen3-vl-plus` | Released 2025-09-23 with snapshot `qwen3-vl-plus-2025-09-23`. | Localization and document/webpage parsing. | No | No |
| `qwen-vl-ocr` | Listed in the 2025-11-20 release entry alongside `qwen-vl-ocr-2025-11-20`. | OCR and structured extraction from text-heavy images. | No | No |

`Yes` means that exact rolling ID appears in the corresponding Token Plan allowlist. No dedicated Qwen3-VL, Qwen-VL, or OCR ID appears in either allowlist.

`qwen3.5-plus` and its two listed snapshots retire on 2027-01-19; use `qwen3.8-flash` for new deployments.

## Selection guidance

| Need | Model | Notes |
|---|---|---|
| Default, highest capability, or visual reasoning | `qwen3.8-max` | Cross-plan default; do not substitute the snapshot ID for Token Plan. |
| Faster current-generation analysis | `qwen3.8-flash` | PAYG and both Token Plans. |
| Dedicated localization or document parsing | `qwen3-vl-plus` | PAYG only. |
| Dedicated OCR | `qwen-vl-ocr` | PAYG only; use `qwen-vl-ocr-2025-11-20` when a pinned version is required. |

## Thinking behavior

- Thinking is off by default for `qwen3-vl-plus`.
- For `qwen3.6-flash`, official guides differ on the thinking default; omit `enable_thinking` to preserve the service default unless explicitly requested.
- Thinking is on by default for the other listed Qwen3.5 and later multimodal models.
- A model ID ending in `-thinking` always thinks.
- Thinking tokens are billed as output tokens.

## Input limits

- Image dimensions: width and height must each be greater than 10 pixels; aspect ratio must not exceed 200:1. Keep images within 8K to reduce timeout risk.
- Formats below 4K: BMP, JPEG, PNG, TIFF, WEBP, and HEIC. From 4K through 8K, only JPEG/JPG and PNG are supported.
- Per-image size by public URL: up to 20 MB for Qwen3.8, Qwen3.7, Qwen3.6, Qwen3.5, and Qwen3-VL; 10 MB for other models. A local path is limited to 10 MB.
- Base64 input: original file up to 20 MB for those newer families and 10 MB for others; the resulting Data URI must not exceed 20 MB on OpenAI-compatible and DashScope APIs, or 32 MB on the Anthropic-compatible API. The total request body across all images must not exceed 64 MB.
- Image count by URL/local path: up to 2,048 for Qwen3.8 Max/Flash and Qwen3.7 Plus; up to 256 for Qwen3.7 Flash, Qwen3.6 Plus/Flash, Qwen3.5 Plus/Flash, and Qwen3-VL. Base64 input supports up to 250 images.
- Video image lists: 4-8,000 frames for Qwen3.8, Qwen3.7, Qwen3.6, and Qwen3.5; 4-2,000 for `qwen3-vl-plus`.
- Video file size by public URL: up to 2 GB for Qwen3.8, Qwen3.7, Qwen3.6, Qwen3.5, and Qwen3-VL.
- Video file size by Base64: the encoded string must be less than 10 MB.
- Video file size by local path: up to 100 MB when passed as a local file path through the DashScope SDK. A local file encoded as Base64 is subject to the Base64 limit instead.
- Video duration: 2 seconds-2 hours for Qwen3.8, Qwen3.7, Qwen3.6, and Qwen3.5; 2 seconds-1 hour for `qwen3-vl-plus`.
- At most 64 videos can be supplied per request. Vision models sample frames and do not understand the video's audio track.

## OCR limits

- `qwen-vl-ocr` and `qwen-vl-ocr-2025-11-20`: 38,192-token context, 30,000 maximum input tokens, and 8,192 maximum output tokens.
- `qwen-vl-ocr` defaults `max_tokens` to 4,096. Increasing it to 4,097-8,192 requires contacting a commercial manager.
- These OCR models use 32 x 32 pixels per visual token.

Verified: 2026-10-20.
