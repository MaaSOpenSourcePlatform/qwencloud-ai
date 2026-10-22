# QwenCloud Audio TTS Models

> Catalog checked: 2026-10-20. Only models released after 2025-09-01 are included.

## Defaults

| Scope | Default or recommendation | Configured default voice | Protocol and availability |
|-------|-----------------|--------------------------|---------------------------|
| Overall | `qwen-audio-3.0-tts-plus` | `longanlingxin` | PAYG: WebSocket; Token Plan: native HTTP TTS API |
| Qwen-Audio Flash (WebSocket caller) | `qwen-audio-3.1-tts-flash` | `longanfengyue_v3.1` | Requires a compatible WebSocket caller; PAYG-only |
| Qwen3-TTS HTTP | `qwen3-tts-flash` | `Cherry` | HTTP with optional SSE; non-streaming calls return an audio URL; PAYG-only |
| CosyVoice | `cosyvoice-v3-flash` | `longanyang` | WebSocket; PAYG-only |

`Cherry` is the default voice for Qwen3-TTS HTTP. The `nrt_default_voices` mapping supplies `longanlingxin` for the documented Token Plan HTTP route of `qwen-audio-3.0-tts-plus`; WebSocket-aware callers use `ws_default_voices`. Only models with a verified HTTP route and an entry in `nrt_default_voices` may use that route; do not fall back to another model's voice. An HTTP-only caller does not switch to WebSocket because a model appears in `ws_models`. Use a compatible WebSocket caller for `qwen-audio-3.1-tts-flash` and the PAYG Qwen-Audio WebSocket routes. Explicit model and voice selections are not replaced.

## Model catalog

| Model | Use | Protocol | Plan scope |
|-------|-----|----------|------------|
| `qwen-audio-3.0-tts-plus` | **Default.** Quality-oriented speech synthesis | PAYG: WebSocket; Token Plan: native HTTP TTS API | Token Plan + PAYG |
| `qwen-audio-3.1-tts-flash` | Low-latency multilingual speech synthesis with instruction control | Requires a compatible WebSocket caller | PAYG-only |
| `qwen-audio-3.0-tts-flash` | Low-latency speech synthesis | WebSocket | PAYG-only |
| `qwen3-tts-flash` | Multilingual synthesis | HTTP with optional SSE; non-streaming calls return an audio URL | PAYG-only |
| `cosyvoice-v3-flash` | Fast CosyVoice synthesis | WebSocket through DashScope SDK | PAYG-only |
| `cosyvoice-v3-plus` | Quality-oriented CosyVoice synthesis | WebSocket through DashScope SDK | PAYG-only |

The Qwen3-TTS voice reference also documents real-time aliases. They require the separate Qwen3-TTS WebSocket protocol and cannot use the Qwen3-TTS HTTP path.

Qwen3-TTS's HTTP API supports optional SSE streaming. A non-streaming HTTP caller returns/downloads the resulting audio URL; streaming chunks require an SSE-capable caller.

## Limits and request compatibility

- Token Plan documents the native HTTP `/api/v1/services/audio/tts/SpeechSynthesizer` endpoint. A model's inclusion in its allowlist does not establish compatibility with the PAYG WebSocket path.
- The CosyVoice `nrt_models` and `custom_voice_only_models` arrays are empty for this catalog. Compatible consumers must use the documented WebSocket route for the listed CosyVoice models; HTTP support cannot be inferred from model names.
- Qwen3-TTS HTTP models accept at most 600 characters of synthesis text per request.
- Qwen3-TTS non-streaming output URLs expire after 24 hours.
- `language_type` applies to the Qwen3-TTS HTTP path. WebSocket models use their own model-specific parameters and voices.
- A cloned or designed voice must be synthesized with the same target model used to create it.

## Qwen-Audio system voices

Voices are model-specific and cannot be interchanged without verification.

| Model | Supported system voices |
|-------|-------------------------|
| `qwen-audio-3.1-tts-flash` | `longanhuan_v3.1`, `longanlingxin_v3.1`, `longanfengyue_v3.1`, `xunanchuan_v3.1`, `Emily_v3.1`, `Luna_v3.1`, `Eric_v3.1`, `Luca_v3.1`, `Abby_v3.1`, `Annie_v3.1`, `Ava_v3.1`, `Beth_v3.1`, `Betty_v3.1`, `Cally_v3.1`, `Cindy_v3.1`, `Donna_v3.1`, `Andy_v3.1`, `Brian_v3.1`, `David_v3.1` |
| `qwen-audio-3.0-tts-plus` | `longanlingxin`, `longanlufeng` |
| `qwen-audio-3.0-tts-flash` | `longanfengyue`, `longanyuanfei`, `longanlingxi`, `longanxiaoxin`, `longanhuan_v3.6`, `longjielidou_v3.6`, `longpaopao_v3.6`, `longhuohuo_v3.6`, `longchuanshu_v3.6`, `loongmary`, `loongeva_v3.6`, `loongjohn` |

The listed Qwen-Audio 3.1 voices are available in Singapore and Beijing. Its other system voice categories are Beijing-only. Both Qwen-Audio 3.0 models also provide model-specific base voices generated through voice cloning. Use the exact model prefix documented in the official voice list.

## Qwen3-TTS system voices

The unversioned aliases expose the following current voice sets. Language support is voice-specific, especially for dialect voices.

### `qwen3-tts-flash` (48)

`Cherry`, `Serena`, `Ethan`, `Chelsie`, `Momo`, `Vivian`, `Moon`, `Maia`, `Kai`, `Nofish`, `Bella`, `Eldric Sage`, `Mia`, `Mochi`, `Bellona`, `Vincent`, `Bunny`, `Neil`, `Elias`, `Arthur`, `Nini`, `Seren`, `Pip`, `Stella`, `Jennifer`, `Ryan`, `Katerina`, `Aiden`, `Bodega`, `Sonrisa`, `Alek`, `Dolce`, `Sohee`, `Ono Anna`, `Lenn`, `Emilien`, `Andre`, `Radio Gol`, `Jada`, `Dylan`, `Li`, `Marcus`, `Roy`, `Peter`, `Sunny`, `Eric`, `Rocky`, and `Kiki`.

## CosyVoice system voices

| Model | Supported system voices |
|-------|-------------------------|
| `cosyvoice-v3-plus` | `longanyang`, `longanhuan` |
| `cosyvoice-v3-flash` | `longanyang`, `longanhuan`, `longhuhu_v3`, `longjielidou_v3`, `longshanshan_v3`, `longniuniu_v3`, `longanyue_v3`, `longshange_v3`, `longanmin_v3`, `longyingxiao_v3`, `longyingxun_v3`, `longyingtao_v3`, `longanyun_v3`, `longanwen_v3`, `longanli_v3`, `longanlang_v3`, `longyingmu_v3`, `longhua_v3`, `longwan_v3`, `longanzhi_v3`, `longanya_v3`, `longanqin_v3`, `longwanjun_v3`, `longyichen_v3`, `longlaobo_v3`, `longlaoyi_v3`, `longjiqi_v3`, `longhouge_v3`, `longdaiyu_v3`, `longanxuan_v3` |

All listed CosyVoice voices support SSML and timestamps. Instruction support is voice-specific:

- `cosyvoice-v3-plus`: `longanyang`, `longanhuan`.
- `cosyvoice-v3-flash`: `longanyang`, `longanhuan`, `longhuhu_v3`.

## Billing and Token Plan compatibility

- Qwen-Audio 3.0, Qwen3-TTS, and CosyVoice PAYG synthesis is billed per **10,000 input characters**; output is not charged.
- `qwen-audio-3.1-tts-flash` uses token billing: **$0.23 per million input tokens** and **$1.87 per million output tokens**.
- A Chinese character, Japanese kanji, or Korean hanja counts as 2 characters. Letters, digits, punctuation, spaces, Japanese kana, and Korean letters count as 1 character. SSML tags are excluded.
- The official `qwen-audio-3.0-tts-plus` model page currently lists **$0.20 per 10,000 characters** and an RPM limit of **180**.
- `qwen-audio-3.0-tts-plus` is the only speech-synthesis model in the current Token Plan Individual and Team exact allowlists.
- `qwen-audio-3.1-tts-flash`, `qwen-audio-3.0-tts-flash`, Qwen3-TTS, and CosyVoice models require PAYG.
