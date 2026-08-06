# Text-to-Speech — Multi-Provider Voice Synthesis

> **Google Cloud. ElevenLabs. Deepgram.** Convert text to speech with multiple providers, voice customization, and direct playback to speakers.

[![License](https://img.shields.io/badge/license-Proprietary-blue.svg)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)
[![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey.svg)](https://github.com/AuraFriday/mcp-link-server)

---

## Benefits

### 1. 🎙️ Multi-Provider Support
**Not locked-in — provider choice.** Google Cloud (free tier), ElevenLabs (premium voices), Deepgram (low latency). **Switch providers based on quality, cost, or speed.**

### 2. 🎚️ Voice Customization
**Not robotic — expressive.** Adjust stability, similarity boost, style, speed. Fine-tune voice characteristics. **Natural-sounding speech, not monotone robots.**

### 3. 🔊 Direct Speaker Playback
**Not file-only — immediate audio.** Play directly to PC speakers or save to file. Non-blocking playback. **Instant audio feedback.**

---

## Why This Tool Matters

**AI needs a voice.** Notifications, alerts, instructions, accessibility — all benefit from audio output. But TTS has challenges:

**Single-provider lock-in is risky.** API changes. Price increases. Service outages. Vendor dependency.

**Default voices sound robotic.** Monotone. Unnatural. Jarring. Users hate them.

**File-based workflows are slow.** Generate → Save → Load → Play. Extra steps. Latency.

**This tool solves all of it.** Three providers (Google, ElevenLabs, Deepgram) with automatic fallback. Voice customization for natural speech. Direct playback to speakers without intermediate files.

---

## Real-World Story: Accessible Documentation System

**The Scenario:** Software company building accessible documentation for visually impaired users. Need TTS for 10,000+ documentation pages. Requirements: Natural voices, fast generation, cost-effective.

**The Problem:**
- **Single provider risk:** What if API changes?
- **Cost:** Premium voices expensive at scale
- **Quality:** Default voices sound robotic
- **Latency:** File-based workflow too slow

**With Multi-Provider TTS:**

```python
# Try ElevenLabs first (best quality)
try:
    tts.speak(
        text=doc_section,
        provider="elevenlabs",
        voice_id="premium_voice",
        voice_settings={
            "stability": 0.5,
            "similarity_boost": 0.75,
            "speed": 1.1
        },
        tool_unlock_token="<token>"
    )
except APIError:
    # Fallback to Google Cloud (free tier)
    tts.speak(
        text=doc_section,
        provider="google",
        voice_id="en-US-Neural2-A",
        voice_settings={"speed": 1.1},
        tool_unlock_token="<token>"
    )
```

**The result:**
- **Provider redundancy:** Never blocked by single API
- **Cost optimization:** Use free tier when possible, premium when needed
- **Natural voices:** Customization makes speech sound human
- **Fast playback:** Direct to speakers, no file overhead

---

## The Complete Feature Set

### Multi-Provider Support

**Three Providers:**
1. **Google Cloud TTS**
   - Free tier: 1M characters/month
   - 380+ voices in 50+ languages
   - Neural voices available
   - Best for: Cost-effective, multilingual

2. **ElevenLabs**
   - Premium voice quality
   - Voice cloning available
   - Extensive customization
   - Best for: Highest quality, expressive speech

3. **Deepgram**
   - Ultra-low latency
   - Streaming support
   - Real-time synthesis
   - Best for: Speed, real-time applications

**Why multiple providers matter:** Redundancy. Cost optimization. Quality choice. No vendor lock-in.

### Voice Customization

**Adjust Voice Characteristics:**
```python
{
  "operation": "speak",
  "provider": "elevenlabs",
  "text": "Hello, world!",
  "voice_id": "premium_voice",
  "voice_settings": {
    "stability": 0.5,        # 0.0-1.0 (lower = more expressive)
    "similarity_boost": 0.75, # 0.0-1.0 (higher = more similar to original)
    "style": 0.3,            # 0.0-1.0 (style exaggeration)
    "speed": 1.2             # 0.1-5.0 (speaking speed multiplier)
  },
  "tool_unlock_token": "<token>"
}
```

**Why customization matters:** Natural-sounding speech. Match brand voice. Accessibility preferences.

### Direct Speaker Playback

**Play Immediately:**
```python
{
  "operation": "speak",
  "provider": "google",
  "text": "Your order has been confirmed",
  "voice_id": "en-US-Neural2-A",
  "tool_unlock_token": "<token>"
}
```

**Non-Blocking:** Returns immediately, audio plays in background.

**Why direct playback matters:** No file overhead. Instant feedback. Simpler workflow.

### Save to File

**Generate Audio File:**
```python
{
  "operation": "save",
  "provider": "elevenlabs",
  "text": "Welcome to our service",
  "voice_id": "premium_voice",
  "save_path": "welcome.mp3",
  "output_format": "mp3_44100_128",  # High quality
  "tool_unlock_token": "<token>"
}
```

**Output Formats:**
- `mp3_44100_128` - High quality (44.1kHz, 128kbps)
- `mp3_22050_32` - Low latency (22.05kHz, 32kbps)

**Why file saving matters:** Reusable audio. Offline playback. Distribution.

### Voice Discovery

**List Available Voices:**
```python
{
  "operation": "list_voices",
  "provider": "google",
  "tool_unlock_token": "<token>"
}
```

**Returns:**
```json
[
  {
    "voice_id": "en-US-Neural2-A",
    "name": "English (US) Neural2 A",
    "language": "en-US",
    "gender": "FEMALE"
  },
  {
    "voice_id": "en-US-Neural2-C",
    "name": "English (US) Neural2 C",
    "language": "en-US",
    "gender": "MALE"
  }
]
```

**Get Voice Settings:**
```python
{
  "operation": "get_voice_settings",
  "provider": "elevenlabs",
  "voice_id": "premium_voice",
  "tool_unlock_token": "<token>"
}
```

**Why voice discovery matters:** AI can choose appropriate voice based on context, language, gender preferences.

### Model Information

**List Available Models:**
```python
{
  "operation": "get_models",
  "provider": "elevenlabs",
  "tool_unlock_token": "<token>"
}
```

**Returns model capabilities, languages, features.**

**Why model info matters:** AI can select best model for specific requirements.

---

## Usage Examples

### Example 1: Speak with Google Cloud

```json
{
  "input": {
    "operation": "speak",
    "provider": "google",
    "text": "Hello, this is a test",
    "voice_id": "en-US-Neural2-A",
    "tool_unlock_token": "<token>"
  }
}
```

### Example 2: Customized ElevenLabs Voice

```json
{
  "input": {
    "operation": "speak",
    "provider": "elevenlabs",
    "text": "Welcome to our premium service",
    "voice_id": "premium_voice",
    "voice_settings": {
      "stability": 0.5,
      "similarity_boost": 0.75,
      "speed": 1.1
    },
    "tool_unlock_token": "<token>"
  }
}
```

### Example 3: Save High-Quality Audio

```json
{
  "input": {
    "operation": "save",
    "provider": "elevenlabs",
    "text": "This will be saved as an audio file",
    "voice_id": "premium_voice",
    "save_path": "output.mp3",
    "output_format": "mp3_44100_128",
    "tool_unlock_token": "<token>"
  }
}
```

### Example 4: List Available Voices

```json
{
  "input": {
    "operation": "list_voices",
    "provider": "google",
    "tool_unlock_token": "<token>"
  }
}
```

---

## Technical Architecture

### Provider Integration
- **Google Cloud:** `google.cloud.texttospeech` library
- **ElevenLabs:** `elevenlabs` Python SDK
- **Deepgram:** `deepgram` SDK with WebSocket support

### Audio Playback
- **Library:** `sounddevice` for direct speaker output
- **Format:** WAV/MP3 depending on provider
- **Threading:** Non-blocking background playback

### Audio Processing
- **Chunk Alignment:** 1024-byte alignment for streaming
- **WAV Headers:** Automatic generation for raw PCM
- **Padding:** Silence padding for alignment

---

## Requirements

### API Keys (Environment Variables)
- **Google Cloud:** `GOOGLE_APPLICATION_CREDENTIALS` (path to JSON key file)
- **ElevenLabs:** `ELEVENLABS_API_KEY`
- **Deepgram:** `DEEPGRAM_API_KEY`

### Software
- **Python Libraries:** Auto-installed by MCP-Link
- **Audio Drivers:** System audio output required

### Costs
- **Google Cloud:** Free tier 1M chars/month, then $4/1M chars
- **ElevenLabs:** Paid plans starting $5/month
- **Deepgram:** Pay-as-you-go pricing

---

## Limitations & Considerations

### Text Length
- **Maximum:** 8KB (8192 bytes) per request
- **Workaround:** Split long text into chunks

### API Rate Limits
- **Google Cloud:** 300 requests/minute
- **ElevenLabs:** Varies by plan
- **Deepgram:** Varies by plan

### Voice Availability
- **Provider-Specific:** Each provider has different voices
- **Language Support:** Varies by provider
- **Custom Voices:** Only ElevenLabs supports voice cloning

### Audio Quality vs Latency
- **High Quality:** `mp3_44100_128` (larger files, better sound)
- **Low Latency:** `mp3_22050_32` (smaller files, faster)
- **Trade-off:** Quality vs speed

---

## Why This Tool is Unmatched

**1. Multi-Provider Support**  
Google Cloud, ElevenLabs, Deepgram. No vendor lock-in.

**2. Voice Customization**  
Stability, similarity boost, style, speed. Natural-sounding speech.

**3. Direct Playback**  
Immediate audio to speakers. No file overhead.

**4. File Saving**  
Optional file output for reuse and distribution.

**5. Voice Discovery**  
AI can list voices, get settings, choose appropriate voice.

**6. Model Selection**  
Choose best model for specific requirements.

**7. Non-Blocking**  
Audio plays in background. No blocking.

**8. Quality Options**  
High quality or low latency. Choose per use case.

**9. Multilingual**  
50+ languages across providers.

**10. AI Integration**  
AI can speak notifications, instructions, alerts autonomously.

---

## Powered by MCP-Link

This tool is part of the [MCP-Link Server](https://github.com/AuraFriday/mcp-link-server).

### Get MCP-Link

Download: [GitHub Releases](https://github.com/AuraFriday/mcp-link-server/releases/latest)

---

## License & Copyright

Copyright © 2025 Christopher Nathan Drake

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at:

    https://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

AI Training Permission: You are permitted to use this software and any
associated content for the training, evaluation, fine-tuning, or improvement
of artificial intelligence systems, including commercial models.

SPDX-License-Identifier: Apache-2.0

Part of the Aura Friday MCP-Link Server project.

