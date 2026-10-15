```text
ness.js@github:~$ whoami
ricardo freitas — software engineer · MSc SWE @ ISEP, final year · porto, portugal
ness.js@github:~$ cat tagline.txt
I drink coffee, write code, and I know things. That's what I do.
ness.js@github:~$ cat ~/now
building    RNAP — native audio engine for React Native (swift + kotlin + jsi)
shipping    Rádio Animu's official app — 1,000+ installs, 4.9★, runs on RNAP
finishing   MSc in Software Engineering @ ISEP — jul 2027
ness.js@github:~$ uptime
shipping since 2020 · 8 hackathons, 6 awards · fueled by caffeine
```

[website](https://rmotafreitas.dev) · [x / twitter](https://x.com/rmotafreitas) · [github](https://github.com/rmotafreitas) · [linkedin](https://www.linkedin.com/in/ricardo-freitas-0b620124b/)

---

## now building — RNAP

<img src="https://raw.githubusercontent.com/rmotafreitas/react-native-anything-player/main/docs/assets/brand/mascot-480.webp" width="170" align="right" alt="RNAP's mascot, a fox girl in orange headphones" />

> **[React Native Anything Player](https://github.com/rmotafreitas/react-native-anything-player)**: a native-first audio player for React Native. Files, streams and internet radio that keep playing correctly through network loss, phone calls, app switches and a frozen JavaScript thread.

When React Native Track Player went commercial (v5 needs a paid licence, even for a free app from a non-profit radio), I wrote my own player instead. The whole player lives in native code: state machine, recovery, audio focus, interruptions, media session and clocks. JavaScript only sends commands and mirrors native state, so playback never depends on it.

```ts
const player = new Player();
await player.load('https://radio.example.com/stream');
await player.play(); // reconnects, survives wifi ↔ cellular, ICY metadata on the lock screen
```

What it handles:

- **playback runs in Swift/Kotlin engines** that keep going and recover while React Native has the JS runtime suspended in the background
- **one connection per stream.** An iOS HTTP proxy stops duplicate downloads and releases abandoned sockets, checked against a connection-counting test server
- **recovery.** Stall and silent-stall detection, dead-socket re-open, jittered backoff, offline-aware probing, and circuit breakers so it can't cause a connection storm
- **no race conditions.** Per-open generations reject stale native events, commands apply in call order, and status snapshots are sequence-numbered
- **TurboModule with zero JS dependencies.** Progress is a synchronous JSI read (~10 µs), so a progress bar doesn't need events
- **decoded-audio access for visualisers**, including live HTTP streams on iOS, where AVPlayer's audio tap never runs
- works with Expo (config plugin) and bare RN, and has a [docs site](https://react-native-anything-player.vercel.app) with benchmarks, a recovery policy and soak test results

![Swift](https://img.shields.io/badge/Swift-F05138?style=flat-square&logo=swift&logoColor=white)
![Kotlin](https://img.shields.io/badge/Kotlin-7F52FF?style=flat-square&logo=kotlin&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![React Native](https://img.shields.io/badge/TurboModules%20%2F%20JSI-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![Expo](https://img.shields.io/badge/Expo-000020?style=flat-square&logo=expo&logoColor=white)

## in production — Rádio Animu

> **[RadioAnimu/animu-mobile-app](https://github.com/RadioAnimu/animu-mobile-app)**: the official Android/iOS app for [Rádio Animu](https://www.animu.moe), "the most moe radio in Brazil". It's a community-run, non-profit radio that has played anime openings, vocaloid, J-Pop and game OSTs 24/7 since 2018.

I own the app's development and releases, with 530+ commits since 2023. RNAP is what it plays on.

- **audio and metadata stay in sync.** It compensates for stream buffering and device clock drift, so the song info and lock-screen progress match what listeners actually hear, in the background too
- **a shared identity backend** for social sign-in (Discord / Google / Apple), passwordless email and account linking
- **[animu-api](https://github.com/RadioAnimu/animu-api)**, a typed, zero-dependency TypeScript SDK for auth and radio integration that I extracted from the app
- **CI with GitHub Actions + Jenkins** checks code quality, security and device compatibility before each build ships
- localised in **PT / EN / JP / ES**, and distributed on iOS through AltStore

[Play Store — 1,000+ downloads, 4.9★](https://play.google.com/store/apps/details?id=com.nessjs.animu) · [animu.moe](https://www.animu.moe) · [source](https://github.com/RadioAnimu/animu-mobile-app)

## experience

**Research Intern, Software Engineering** · [GECAD](https://www.gecad.isep.ipp.pt), ISEP · *feb – jun 2025*
Built the Medicinal Garden Platform (web + mobile): AI plant identification, garden management, plant trades and messaging. It's split into .NET, Python and TypeScript microservices with shared Keycloak auth, Docker and centralised logging. I made Gemini's image identification output reliable by validating and normalising it into structured results, and built account deletion that removes a user's data from MySQL, MongoDB and uploaded files.

**Intern, E-Learning & E-Commerce** · RFA.pt · *jul 2021 – feb 2022*
PrestaShop storefront features and Articulate Storyline training modules. This was my first time writing code for someone else's users.

## hackathons

8 hackathons and 6 awards. Three of the wins were solo, against teams.

| event | project | result | stack |
|---|---|---|---|
| **FCUP Update 23/24** · Porto | [planner.ai](https://github.com/rmotafreitas/planner.ai) | 🥇 1st (solo, vs teams) | React · Fastify · OpenAI |
| **Music Hackspace '26** · Lisbon | [Venue Brain](https://github.com/rmotafreitas/venue-brain) | 🥈 2nd, Algoriddim + TouchDesigner challenge (solo). Showcased at **Abbey Road Studios** during SXSW London | React · Bun/Elysia · MongoDB · WebSockets · OSC |
| **Sonae · Future Innovators '24** | [StudyCopilot](https://github.com/rmotafreitas/StudyCopilot) | 🥈 2nd (solo, vs teams) | React · Fastify · Whisper · GPT-4o vision |
| **BugsByte 23/24** · Braga | [Xeonex](https://github.com/rmotafreitas/trading-bot-xeonex) | 🥈 2nd overall + 🥇 1st thematic (team of 2) | React · Spring Boot · OpenAI |
| **Hanko Hackathon '23** · online | [docus.autos](https://github.com/rmotafreitas/docus.autos) | 🏅 runner-up (top 10) | React · Fastify · OpenAI · ffmpeg.wasm |
| **FCUP '23** · Porto | [mental-health-bot](https://github.com/rmotafreitas/mental-health-bot) | 🥉 3rd | Node · JavaScript |
| **HackUPC '24** · Barcelona | [Nutri Mate](https://github.com/rmotafreitas/hackupc2324) | shipped & demoed | React Native · Node · MongoDB · OpenAI |
| **HackUDC '25** · A Coruña | [TerapIA](https://github.com/pintous66/hack-udc) | shipped & demoed (team of 3) | Spring Boot · React · OpenAI |

Also 🥈 2nd at the **Celfocus Cybersecurity CTF** (ISEP DEI HackDays '22).

## other things I've built

- **Hospital.ai** (ISEP, team of 4). A hospital platform across .NET and Node.js services, with a **Prolog planner + genetic algorithm** that schedules surgeries around rooms, staff and existing bookings, and a **Three.js** 3D hospital view for checking room occupancy
- **[Badminton Buddy](https://github.com/rmotafreitas/badminton-app)**. Club match tracking with singles and doubles **Elo**, which gets recalculated correctly when someone edits or deletes a past result
- **[dotfiles](https://github.com/rmotafreitas/dotfiles)**. Bash/Zsh/tmux/Git config with toolchain discovery and a tested, backup-first installer

## stack

[![stack](https://skillicons.dev/icons?i=ts,swift,kotlin,cs,java,py,go,php,lua&theme=dark)](#stack)
[![stack](https://skillicons.dev/icons?i=react,threejs,tailwind,vite,nodejs,bun,dotnet,spring&theme=dark)](#stack)
[![stack](https://skillicons.dev/icons?i=mongodb,mysql,sqlite,docker,azure,githubactions,jenkins&theme=dark)](#stack)

Also: React Native New Architecture (TurboModules / JSI), Expo, Prolog, Keycloak / OIDC, OAuth 2.0, WebSockets, SSE, OpenAI / Gemini APIs. I like domain-driven design and tests that would actually catch the bug.

## latest youtube uploads

<!-- YOUTUBE:START -->
- [Touhou Monster TD Level 10 Lunatic 3*](https://www.youtube.com/watch?v=ovvEyyD_EuU)
- [Discord Bot#3 - Comando de Waifu](https://www.youtube.com/watch?v=oX1t-nX6y9o)
- [Discord.js#2 Comando de Triggered](https://www.youtube.com/watch?v=7152O0BKzuM)
- [Tutorial Bot Discord v13 #1](https://www.youtube.com/watch?v=bbYpBe1MR6c)
- [Pokemon Fire Red até zerar? (Chill)](https://www.youtube.com/watch?v=WaFsmi5KA9c)
<!-- YOUTUBE:END -->

[more on the channel](https://www.youtube.com/channel/UCwGmvFQAQLIFMfyDKKzafPw)

## side quests

<img src="https://www.rmotafreitas.dev/kita1.gif" width="150" align="right" alt="kita" />

- **NEI-ISEP**: I've co-organised events, workshops and hackathons for ISEP's informatics students since 2022
- **Kaori Miyazono**: a [Discord bot](https://github.com/rmotafreitas/BotKaoriDiscord) (23★, discord.js) from before slash commands existed. It did anime lookups, an economy, music and games, and it spawned a Portuguese YouTube tutorial series
- **Ness.js**: retired Super Smash Bros. player, Ness main. The alias stuck
- badminton, chess, and DJing (which is how Venue Brain happened)

<img src="https://www.rmotafreitas.dev/chihiro.gif" width="120" alt="chihiro" />

---

[website](https://rmotafreitas.dev) · [x / twitter](https://x.com/rmotafreitas) · [linkedin](https://www.linkedin.com/in/ricardo-freitas-0b620124b/)

© 2026 Ricardo Freitas · Gaia, Portugal
