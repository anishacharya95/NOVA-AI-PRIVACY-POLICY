# Nova AI Privacy Policy

**Effective date:** 20 November 2026  
**App:** Nova AI for Android  
**Package:** `com.novaai.app`  
**Developer contact:** [Anishacharya95@gmail.com](mailto:Anishacharya95@gmail.com)

This Privacy Policy explains how Nova AI handles information when you use the Android application and its optional Nova Free service. It is based on the app's current repository documentation and implementation notes. Features and data flows may change as the app evolves; this policy must be updated before materially different data practices are released.

## 1. At a glance

- Chat conversations and message content are stored locally on your device; Nova AI's Firestore conversation index contains metadata, not message bodies.
- When you send a prompt, the prompt and relevant conversation context are sent to the AI provider and model you select.
- Nova Free sends requests through a Cloudflare Worker to its configured upstream model provider.
- Firebase Authentication and Firestore are used for account and limited conversation-index data when Firebase is configured for the app.
- Provider API keys that you add are encrypted using Android Keystore-backed AES-GCM encryption and are not uploaded or synced by the app.
- The reviewed build documentation reports no analytics, advertising, or crash-reporting SDK.

## 2. Information handled by Nova AI

### Information stored on your device

The app stores the following in its private application storage:

- Chat messages and conversation details, including titles and timestamps.
- References to attachments you choose, such as the content URI, display name, MIME type, and file size. Image bytes are read when you send an image with a message.
- Provider settings and API keys you enter. API keys are encrypted using AES-GCM with a non-exportable Android Keystore key.
- Assistants, system prompts, and app preferences such as language, theme, temperature, and streaming settings.
- AI response reports you create. Reports remain local unless you choose to share them.

The app's documented Android backup rules exclude these app data stores from cloud backup and device-to-device transfer. Local data is removed when you uninstall the app or clear its storage. Chat content is protected by Android's app sandbox; it is not described as separately encrypted at rest. Provider API keys receive the additional Keystore-backed encryption described above.

### Account information

When Firebase account functionality is configured and you register or sign in, Firebase Authentication processes your email address and authentication data. The app's documented Firestore profile contains your Firebase user ID, email address, optional display name, and account timestamps.

While signed in, the app may also store a conversation index in Firestore. This index contains conversation titles (limited to 160 characters), timestamps, message counts, and sync timestamps. It does **not** contain message bodies, attachments, provider API keys, or safety reports.

Firebase is operated by Google and processes account information under Google's applicable terms and privacy disclosures.

## 3. Information shared with AI providers

When you submit a chat request, Nova AI sends the selected provider:

- Your prompt text.
- The conversation history included in the request.
- Your system prompt or assistant instructions.
- Images you attach, encoded for the request, when the selected model supports vision. Image requests are blocked when the selected model is not marked as supporting vision.
- Filenames and MIME types of non-image attachments as text references. The app documentation says the contents of those non-image files are not uploaded.
- Your provider API key as the authentication credential when the provider requires one.

Supported provider presets documented by the project include OpenRouter, Google Gemini, Puter, NVIDIA NIM, Cohere, Groq, OpenAI, DeepSeek, Mistral, Together AI, SiliconFlow, Nova Free, and custom OpenAI-compatible endpoints. Local services such as Ollama and LM Studio may also be configured.

Each provider processes requests under its own privacy policy, retention practices, and terms. Nova AI does not control whether a third-party provider retains prompts or uses submitted information to improve its services. Review the provider's terms before sending information. Avoid submitting passwords, payment details, confidential documents, or other sensitive information unless you have assessed the provider's practices and have a lawful reason to do so.

## 4. Nova Free

Nova Free is an optional shared free-model gateway. When you use it:

- Your Firebase ID token is sent to the Nova Free Cloudflare Worker to authenticate the request.
- Your prompt and included conversation history are forwarded to the configured upstream model provider, and the response is streamed back to the app.
- The documented Worker does not persist prompts or replies. Its diagnostic logs are described as containing model identifiers and HTTP status codes, not prompt text, credentials, or user identifiers.
- Abuse-protection counters are keyed by Firebase user ID and IP address and expire after approximately one hour.
- Images are not accepted through this route.

The upstream provider receives the request and may process or retain it under its own terms. Cloudflare also processes network metadata, including IP address, as necessary to host, deliver, and protect the service. The project documentation identifies BlockRun and Cloudflare Workers AI as upstream routes for different Nova Free models; the upstream route depends on the model selected.

## 5. Image Studio

Image Studio uses external image-generation services:

- **Nova Free image generation:** The prompt is sent to the public Pollinations image endpoint. The prompt leaves your device; no Nova account or provider API key is used for this route.
- **Gemini image generation:** Your prompt and any source image you select are sent to Google's Gemini API using your own Gemini API key.

Generated images are held in memory for display. They are saved to your device gallery only when you choose **Save image**. The external provider's own privacy policy governs its processing of submitted prompts and images.

## 6. Permissions and device access

The reviewed Android manifest requests internet access and network-state access. It also declares legacy write-storage permission only for Android versions where it is needed to save a generated image to the gallery.

The reviewed app documentation states that Nova AI does not access your location, contacts, microphone, camera, SMS, call logs, calendar, or installed-app list. It does not read files you have not explicitly selected through the Android file picker. Images are processed only when you choose to attach or submit them through a feature.

## 7. Analytics, advertising, and sale of data

The reviewed build documentation reports that the app includes no analytics SDK, advertising SDK, or crash-reporting SDK. Nova AI does not sell personal data.

Third-party infrastructure providers may process limited technical information as described in this policy. Their own privacy terms apply to their services.

## 8. Security

The project documents the following safeguards:

- Remote provider and Firebase traffic uses HTTPS.
- Provider API keys are encrypted with AES-GCM using a non-exportable Android Keystore key and are excluded from Android backup.
- The app does not intentionally log provider API keys or prompt text.
- The Nova Free Worker is documented as validating Firebase tokens, limiting request sizes and concurrency, and logging model identifiers and HTTP status codes rather than prompts or credentials.
- Firestore rules are designed to restrict each user's documents to that authenticated user.

No method of storage or transmission is completely secure. Firestore rules must be deployed and correctly configured in the production Firebase project for the documented server-side access restrictions to apply. If you believe an API key has been exposed, revoke it with the provider and replace it in Nova AI's provider settings.

## 9. Retention and deletion

- **Chats and attachment references:** Kept locally until you delete them, clear app storage, or uninstall the app. Use the message or conversation delete controls, or **Settings → History and data → Clear all chat history** where available.
- **Provider keys and settings:** Kept locally until you remove the provider or clear app storage/uninstall the app. Use **Settings → Providers**.
- **Safety reports:** Kept locally until you delete them. Use **Settings → Safety reports → Clear all reports** where available.
- **Firebase account and cloud metadata:** Retained until you request account deletion. Use **Settings → General → Delete account** where available.
- **Nova Free abuse-protection counters:** Automatically expire after approximately one hour.
- **Android backup:** The documented app data stores are excluded from Android backup and device-to-device transfer.

Account deletion is intended to remove the Firebase Authentication account, Firestore profile, and conversation-index entries, and to clear the account's local chats, providers, and assistants on the device. Firebase may require a recent sign-in before it completes account deletion. If you uninstall without deleting your account first, local app data is removed but your Firebase account is not automatically deleted.

You can also contact the developer at the email below for privacy questions or deletion assistance. Do not email passwords or API keys.

## 10. International and third-party processing

AI providers, Google Firebase, Cloudflare, and image-generation providers may process information on infrastructure located in countries other than your own. Their processing is governed by their own terms and privacy policies. Nova AI does not control the location, retention, or onward use of data by those independent providers.

## 11. Children's privacy

Nova AI is not directed to children under 13 or the minimum age required by applicable law in the user's country, whichever is higher. The app connects to third-party generative AI services that may produce content unsuitable for minors and cannot independently verify a user's age. If you believe a child has provided personal information in connection with Nova AI, contact the developer.

## 12. AI-generated content

AI responses are generated by third-party models and may be inaccurate, incomplete, outdated, or inappropriate. They are not professional medical, legal, financial, or safety advice. Verify important information independently. You can report an inappropriate response using the message action menu where that feature is available.

## 13. Changes to this policy

This policy may be updated when app functionality, providers, or data practices change. Material changes will be reflected in the revised policy and its effective date. Please review this page periodically and before using new features.

## 14. Contact

For privacy questions, data requests, or concerns about this policy, contact:

**Anish Acharya**  
[Anishacharya95@gmail.com](mailto:Anishacharya95@gmail.com)

---

*This policy describes the app's documented behaviour and is not legal advice. The developer should verify the production Firebase configuration, actual provider routing, account-deletion flow, and Google Play Data Safety answers before release.*
