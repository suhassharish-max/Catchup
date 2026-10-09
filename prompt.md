# Ask away. — CatchUp

## Project

CatchUp is a static, vanilla HTML/CSS/JavaScript app for ProtocolX's **“The Unread Problem — What Did I Miss?”** challenge. Its flow is **Paste conversation → AI analysis → History**. Keep the existing architecture and avoid a backend, account system, analytics, or framework migration.

## On-device AI

- Generate real AI responses in the browser with Transformers.js and `onnx-community/Qwen2.5-0.5B-Instruct`. Prefer WebGPU; fall back to browser WASM/CPU where WebGPU is unavailable.
- The Transformers.js runtime is loaded from jsDelivr and the model weights from Hugging Face on first use; the browser caches downloaded assets. A first run requires internet and can take time. Show download/model errors clearly; never substitute canned AI responses.
- The conversation, name, and follow-up messages are inputs to browser-side inference only. Never include them in network requests, analytics, cloud inference, or requests for model assets. Do not add cloud model APIs or a backend. Keep this privacy statement accurate and visible in the UI.
- The model has a limited context window. When handling a long conversation, make the omission of its middle explicit to the user; do not imply the entire transcript was analyzed.

## Interface and saved data

- Preserve CatchUp branding and the responsive dashboard, follow-up chat, loading states, empty states, useful errors, and clear-input control.
- Support urgent items, decisions, action items and owners, mentions, and deadlines; include source excerpts where the model provides them and do not invent unsupported details.
- Save successful analysis results to browser `localStorage`, restore history items, preserve completed analyses when users edit a transcript, and provide individual deletion and clear-all controls.
- Keep saved conversations on-device and surface storage errors. Do not seed a sample conversation or fabricate model output.

## Validation

Keep changes focused in `index.html`, `styles.css`, and `app.js`. Check JavaScript syntax, ensure the browser model can load and generate a response when network/model availability permits, and exercise paste → analyze → automatic history save → reopen. Confirm conversation content is never sent off-device.
