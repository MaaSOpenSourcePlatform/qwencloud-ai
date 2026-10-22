# QwenCloud Token Plan Models

> Catalog checked: 2026-10-20. The tables use exact model IDs from the official Individual and Team allowlists, filtered to models released after 2025-09-01. The `auto` router is excluded because its underlying model version is not fixed.

## Billing and access scope

| Dimension | PAYG | Token Plan |
|-----------|------|------------|
| Key prefix | `sk-` or `sk-ws-` | `sk-sp-` |
| Billing | Model-specific units | Unified Credits |
| Protocol compatibility | Model/API-specific | OpenAI/Anthropic compatibility for chat-capable models; dedicated native or WebSocket endpoints for image, video, and audio models |
| Intended use | API usage | Interactive use in compatible AI programming and agent tools |

Token Plan publishes these endpoints: OpenAI-compatible `https://token-plan.maas.qwencloudapi.com/compatible-mode/v1`, Anthropic-compatible `https://token-plan.maas.qwencloudapi.com/apps/anthropic`, and native multimodal `https://token-plan.maas.qwencloudapi.com/api/v1`. The native TTS endpoint is `/services/audio/tts/SpeechSynthesizer`; other speech protocols must match the selected model's current Token Plan API. Obtain the API key from the QwenCloud console and honor a console-provided Base URL override if it differs.

## Token Plan Individual (22 models)

| Brand | Model ID | Capability |
|-------|----------|------------|
| Qwen | `qwen3.8-max` | Reasoning, visual understanding, text generation |
| Qwen | `qwen3.8-flash` | Reasoning, visual understanding, text generation |
| Qwen | `qwen3.7-max` | Reasoning, text generation |
| Qwen | `qwen3.7-plus` | Reasoning, visual understanding, text generation |
| Qwen | `qwen3.6-flash` | Reasoning, visual understanding, text generation |
| Qwen | `qwen-image-3.0-pro` | Image generation |
| Qwen | `qwen-audio-3.0-tts-plus` | Speech synthesis |
| Qwen | `qwen-audio-3.0-realtime-plus` | Realtime voice conversation |
| Qwen | `qwen-audio-3.0-asr-flash` | Speech recognition |
| Zhipu AI | `glm-5.3` | Reasoning, text generation |
| Zhipu AI | `glm-5.2` | Reasoning, text generation |
| DeepSeek | `deepseek-v4-pro` | Reasoning, text generation |
| DeepSeek | `deepseek-v4-pro-0813` | Reasoning, text generation |
| DeepSeek | `deepseek-v4-flash-0731` | Reasoning, text generation |
| DeepSeek | `deepseek-v4.1-flash` | Reasoning, visual understanding, text generation |
| DeepSeek | `deepseek-v4.1-flash-1017` | Reasoning, visual understanding, text generation |
| Wan | `wan2.7-image` | Image generation |
| Wan | `wan2.7-image-pro` | Image generation |
| Wan | `wan3.0-video` | Video generation |
| HappyHorse | `happyhorse-1.1-i2v` | Video generation |
| HappyHorse | `happyhorse-1.1-t2v` | Video generation |
| HappyHorse | `happyhorse-1.1-r2v` | Video generation |

## Token Plan Team (31 models)

Team includes all 22 Individual models and these 9 additional models:

| Brand | Model ID | Capability |
|-------|----------|------------|
| Qwen | `qwen3.6-plus` | Reasoning, visual understanding, text generation |
| Qwen | `qwen-image-2.0` | Image generation |
| Qwen | `qwen-image-2.0-pro` | Image generation |
| Moonshot AI | `kimi-k2.7-code` | Reasoning, visual understanding, text generation |
| Moonshot AI | `kimi-k2.6` | Reasoning, visual understanding, text generation |
| Moonshot AI | `kimi-k2.5` | Reasoning, visual understanding, text generation |
| Zhipu AI | `glm-5.1` | Reasoning, text generation |
| Zhipu AI | `glm-5` | Reasoning, text generation |
| MiniMax | `MiniMax-M2.5` | Reasoning, text generation |

## Audio capabilities

- `qwen-audio-3.0-tts-plus`: speech synthesis and the default TTS model because it is available through both PAYG and Token Plan.
- `qwen-audio-3.0-realtime-plus`: realtime voice conversation.
- `qwen-audio-3.0-asr-flash`: speech recognition.
- Other Qwen3-TTS, Qwen-Audio-TTS Flash, and CosyVoice model IDs are not in the Token Plan exact allowlists and require PAYG.

## Plans and quotas

### Individual

| Tier | Standard price | Current promotional price | Monthly quota | Concurrent agents |
|------|----------------|---------------------------|-------------|-------------------|
| Lite | $8/month | $6/month | 11,500 Credits | 1–2 |
| Essential | $16/month | $10/month | 25,500 Credits | 2–3 |
| Standard | $25/month | $18/month | 45,000 Credits | 3–4 |
| Pro | $80/month | $68/month | 180,000 Credits | 6–8 |
| Credit Pack | — | $15/pack/month | 20,000 Credits/pack; not subject to plan quota limits | — |

Quotas reset each 30-day subscription cycle; unused quota does not carry over. Credit Packs require an active Individual subscription, and an account may hold up to five at a time. After the monthly quota is exhausted, Credit Pack Credits are deducted automatically; service pauses when both are exhausted.

### Team

| Seat or pack | Standard price | Current promotional price | Monthly quota |
|--------------|----------------|---------------------------|---------------|
| Standard Seat | $30/seat/month | $20/seat/month | 25,000 Credits/seat/month |
| Pro Seat | $100/seat/month | $75/seat/month | 100,000 Credits/seat/month |
| Max Seat | $200/seat/month | — | 250,000 Credits/seat/month |
| Credit Pack | $700/pack | — | 625,000 Credits/pack |

Promotional pricing is time-sensitive. Check the official pages before purchase.

## Console URLs

- Token Plan Individual: https://home.qwencloud.com/analytics/token-plan/individual
- Token Plan Team: https://home.qwencloud.com/analytics/token-plan/team
- Team Management: https://tokenplan-enterprise.qwencloud.com
- Pricing: https://www.qwencloud.com/pricing/token-plan
