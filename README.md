<div align="center">

<p><a href="./README.md"><kbd><b>English</b></kbd></a>&nbsp;&nbsp;<a href="./README.zh-CN.md"><kbd>简体中文</kbd></a></p>

# Hotel TV Agent

### Turn a room screen into a conversational companion.

Character conversation, service information and room-control demonstrations in one screen experience.  
An open source hotel-room assistant prototype with a local web app and Android client source.

[**Get the complete source**](./hotel-tv-agent-sanitized-source.zip) · [**Run the demo**](#getting-started) · [**Meet the companions**](#two-companions-two-starting-points) · [**Share an idea**](https://github.com/fanalar/hotel-tv-agent/issues)

**MIT code · React + FastAPI · Android source · Local prototype**

![Hotel companion selection UI preview](docs/showcase/welcome.jpg)

</div>

## A warmer way to interact with the room

A room screen can be a place to ask a simple question, plan the next part of a trip, or settle into a conversation at the end of the day. Hotel TV Agent explores how character companionship and practical assistance can share a single interface.

Choose a companion, try a conversation or bedtime story, explore a sample service knowledge base, and inspect simulated light, air-conditioner, curtain and TV states. Text input remains available alongside the voice interaction prototype.

**This is a local demonstration, not a deployed hotel system.** The rooms, device states, channel and knowledge entries are samples. Actual hotel, PMS, room-controller and live-TV integrations are not included. It is a starting point for studying those experiences before implementing real integrations.

## Two companions, two starting points

<table>
<tr>
<td align="center"><img src="docs/showcase/xiaonuan.png" width="300" alt="Xiaonuan"><br><b>Xiaonuan</b><br>Warm company for a conversation about your day</td>
<td align="center"><img src="docs/showcase/azhe.png" width="300" alt="Azhe"><br><b>Azhe</b><br>A conversational partner for plans and room interactions</td>
</tr>
</table>

The two personas are entry points into different conversational styles. Explore the current behavior, adjust the persona logic, and develop your own interaction ideas rather than assuming a character guarantees a particular response.

Preview artwork comes from the original project, published for display at the maintainer's request. Screenshots use isolated demo data; the source archive uses placeholders by default. The current UI is primarily Chinese. The buttons above switch the project introduction, not the app language.

## From a simple request to a visible interaction

| Try this idea | Explore this part of the prototype |
|---|---|
| “I’d like someone to talk to.” | Character selection and conversation |
| “Tell me a bedtime story.” | Story content and the story panel |
| “Set the air conditioner to 26°C.” | A simulated device action and visible room state |
| “What services are available?” | Retrieval from the local sample knowledge base |
| “What is the weather like?” | Public weather lookup and source connectivity |
| “I’m checking out.” | The demo session-cleanup flow |

These are English descriptions of interaction ideas, not a claim that the current Chinese interface or voice recognizer accepts every English request. Actual replies depend on the model, language and configuration; device examples change software states, not physical hardware.

## What you can explore

### 1. A companion on the big screen

The character view brings a persona, dialogue and suggested actions into the same space. Use it to study how a guest moves between a casual conversation, a story and practical room information without navigating unrelated applications.

The project includes a welcome screen, a character stage and panels for specific tasks. The original preview portraits are shown in the gallery; the public code package uses replaceable placeholder assets.

### 2. Voice interaction with a text fallback

The web interface contains a voice interaction prototype and a text input path. Browser support, microphone permissions and speech services affect availability. The Android source includes native speech integration for further experimentation on a phone or intended device.

Voice and text should be tested separately. A working text action is not proof that acoustic recognition or TV microphone routing will work on the intended hardware.

### 3. Room controls you can inspect

The device panel exposes simulated lighting, air-conditioning, curtain and TV states. It provides a concrete surface for studying how a request becomes an action and how that action is presented back to the user.

![Simulated room-control panel](docs/showcase/devices.jpg)

No physical device is connected in this demonstration. To use real room controllers, an integration needs device adapters, authentication, room binding, action permissions and hardware-specific failure handling.

### 4. A knowledge base you can replace

The backend includes a local sample knowledge base. Replace it with information you are authorized to use and test how answers are retrieved and presented. The public source uses generic demonstration entries rather than real hotel addresses, customer details or private service documents.

This is an opportunity to explore reliable hotel-information answers; it is not a promise that a generated answer is an actual service commitment.

### 5. Public information as a conversation topic

Weather and public-information lookup can complement a travel conversation. Availability depends on connectivity and upstream sources. The demonstration channel and ticker are clearly sample content, not a live news feed or real television broadcast.

### 6. A checkout interaction to improve

The prototype contains a checkout cleanup action for demo session data. It offers a starting point for designing how a room interface resets between stays. Before any real use, test the scope of data cleared, client state, session binding and failures across multiple guests and devices.

## Who might find this useful?

- **Developers** exploring TV-oriented interfaces, conversational actions, local APIs or Android integration.
- **Hospitality product teams** evaluating how companionship and service information could fit into a room screen before building real hotel integrations.
- **Open source contributors** interested in speech compatibility, knowledge retrieval, room-controller adapters, localization or accessibility.

The most productive starting point is one small scenario with a clear expected result: a service question, a simulated device action, or a reliable transition between conversation and a panel.

## Getting started

> **Download and extract the complete source archive first.** The browsable Git tree is still being organized. The ZIP contains the complete code, build configuration and Android source. Do not build the incomplete browsable tree directly.

### Run the local web demonstration

Prepare **Python 3.11 and Node.js 20 or later**. The following commands use Windows PowerShell:

```powershell
Invoke-WebRequest "https://github.com/fanalar/hotel-tv-agent/raw/refs/heads/main/hotel-tv-agent-sanitized-source.zip" -OutFile source.zip
Expand-Archive ./source.zip ./hotel-source
cd hotel-source
python -m venv backend/.venv
backend/.venv/Scripts/python -m pip install -r backend/requirements.txt
Copy-Item .env.example .env
cd frontend
npm ci
npm run build
cd ..
backend/.venv/Scripts/python backend/main.py
```

Open **http://127.0.0.1:8000**. Without a model key, the app uses local fallback replies and demonstration device states. For model conversations, configure your own endpoint, model and key in `.env`. No live operator credentials are bundled.

The service listens on loopback by default. Configuring LAN access requires a deliberate host change. The current prototype does not provide production authentication or room isolation; do not expose it directly to the public internet.

### Explore the Android source

Prepare **JDK 17 and Android SDK 35**, configure your local SDK as described in the archive README, then run from the extracted source root:

```powershell
python scripts/fetch_android_model.py
python scripts/android_gradle.py assembleDebug
```

The model script downloads the Chinese Vosk model from its official source. Gradle and libraries are obtained separately. No prebuilt APK, signing material or embedded operator key is supplied. Configure service access at runtime and test recognition, permissions and audio behavior on the intended device.

The Android source uses Android Keystore encryption for stored runtime keys. This implementation still needs real-device testing and does not replace a production account and access-control design.

## Under the hood

| Component | Technology | Purpose |
|---|---|---|
| Screen interface | React | Welcome screen, character stage and task panels |
| Local backend | FastAPI | Conversation, knowledge, lookup and device-state endpoints |
| Local data | SQLite | Demo knowledge and conversation records |
| Android client | Java | Native client, speech integration and runtime settings |
| Android recognition | Vosk | Chinese speech-model integration |

The code provides a prototype interaction flow. It does not contain a production PMS connector, a real room-control driver or licensed live-TV distribution.

## Questions before you try it

<details>
<summary>Can I connect it to an actual hotel room?</summary>

Not out of the box. The current controls are demonstrations. Real integration needs authorized hardware APIs, secure room binding, authentication, action permissions, privacy checks and testing with the actual controller. Build and validate those components before making service promises.

</details>

<details>
<summary>Why do the previews differ from my first run?</summary>

The preview copy uses the original portrait artwork and isolated demo data, with its microphone initially paused. The source ZIP uses new SVG placeholders. Preview images are not pixel-identical installer screenshots or evidence of working voice hardware. Asset rights are documented separately.

</details>

<details>
<summary>Can I run it without a model key?</summary>

You can explore local fallback replies, the interface and simulated device states. Model conversations and some external services need working configuration and connectivity. Provider charges may apply when using your account.

</details>

## Contribute one useful scenario

Ideas worth exploring include reliable microphone behavior, clearer room-action confirmations, room-controller adapters, knowledge-source checks, English UI localization, accessibility and a well-tested checkout reset.

Open an [issue](https://github.com/fanalar/hotel-tv-agent/issues) with the device, version, reproduction steps, expected behavior and actual result. Use fictional room and guest data, and remove credentials from logs. A small reproducible example helps more than a broad claim that a feature “does not work.”

If this direction is useful to you, **star the repository** or help improve one concrete interaction.

## Validation and licensing

The frontend build, isolated sample APIs, Android Java compilation and secret scans of the selected public source passed. Live-model, full APK, real-device audio and actual hotel integration acceptance are not complete. This is a demo prototype, not a production hotel deployment.

No real customer database, private knowledge content, live keys or original Git history is bundled. Code is [MIT](./LICENSE); dependencies are listed in [NOTICE](./NOTICE.md). Preview artwork is covered separately by the [media notice](docs/showcase/MEDIA_NOTICE.md). Models retain their upstream licenses.

Source archive SHA-256: `d073a0303bb3d9e3be7b28ad4efa209256577458e61f25248bdf8640cf656a9b`.

<p align="center"><a href="./README.zh-CN.md"><kbd>切换到简体中文</kbd></a></p>
