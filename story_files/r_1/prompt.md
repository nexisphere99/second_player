PART 2: TWINE SUGARCUBE CODE AGENT PROMPT & FILE STRUCTURE
File Structure
player-two/
├── index.html
├── style.css
├── src/
│   ├── init.tw           (StoryInit, variable setup, stat defaults)
│   ├── header.tw         (StoryCaption or HUD widget)
│   ├── widgets.tw        (Custom macros: stat display, phone UI, choice styling)
│   ├── release1/
│   │   ├── r1-start.tw           (Opening: The Stream)
│   │   ├── r1-apartment.tw       (Post-stream apartment)
│   │   ├── r1-bedroom.tw         (Bedroom scene, intimate)
│   │   ├── r1-riley-dm.tw        (Riley Discord DM choices)
│   │   ├── r1-side-dale.tw       (Side quest: neighbor Dale)
│   │   ├── r1-side-email.tw      (Side quest: LunaFrag email)
│   │   ├── r1-side-gym.tw        (Side quest: Marcus gym encounter)
│   │   ├── r1-stream2.tw         (Evening stream day 2)
│   │   ├── r1-poststream.tw      (Post-stream quiet + Marcus VOD)
│   │   ├── r1-end-choices.tw     (End of release branching)
│   │   └── r1-stats.tw           (End stats display)
│   ├── release2/
│   │   └── (future)
│   └── ...
├── img/
│   ├── locations/
│   │   ├── apartment-bedroom.png
│   │   ├── apartment-kitchen.png
│   │   ├── stream-setup.png
│   │   ├── gym-interior.png
│   │   └── city-night.png
│   │   ├── ethan-neutral.png
│   │   ├── jess-bed.png
│   │   ├── riley-avatar.png
│   │   ├── marcus-gym.png
│   │   └── dale-icon.png
|.  |   scenes
        characters
│   └── ui/
│       ├── phone-frame.png
│       ├── discord-bg.png
│       ├── twitch-chat.png
│       └── stat-bar.png
└── audio/ (optional)
    ├── ambient-apartment.mp3
    ├── stream-alert.mp3
    └── notification.mp3
Code Agent Prompt
You are building a Twine SugarCube 2.x interactive fiction game called "Player Two."

TECH STACK:
- Twine 2 with SugarCube 2.37+
- Custom CSS for dark theme UI
- JavaScript widgets for stat tracking, phone UI, chat simulation

CORE ARCHITECTURE:

1. StoryInit (init.tw) - Initialize all variables:
<<set $viewers to 200>>
<<set $followers to 80000>>
<<set $donationsMonthly to 400>>
<<set $jessCloseness to 85>>
<<set $jessMarcusBond to 0>>
<<set $feminization to 0>>
<<set $streamPersona to "EthX">>
<<set $chatMood to "neutral">>
<<set $suspicion to 0>>
<<set $selfImage to "insecure">>
<<set $rileyTrust to 70>>
<<set $moneyStress to "high">>
<<set $currentRelease to 1>>
<<set $money to 340>>
<<set $rent to 750>>
<<set $rentDays to 12>>
<<set $invictaOpen to "undecided">>
<<set $lunaFragReply to "none">>
<<set $marcusMet to false>>
<<set $daleLurked to false>>
<<set $r1EndChoice to "none">>

2. PASSAGE STRUCTURE:
- Each passage starts with a background image macro and ambient setting
- Use <<timed>> for text reveals where dramatic pacing matters
- Phone/Discord UI uses a custom widget that styles text messages in chat bubbles
- Twitch chat simulation uses a scrolling widget with randomized messages

3. STAT HUD (header.tw):
Create a collapsible sidebar or top bar showing key stats with colored bars.
Use a widget <<statbar>> that takes name, value, max, color.
Stats update reactively after each choice.

4. CHOICE SYSTEM:
- Main story choices use styled <<link>> macros with stat consequence previews (optional toggle)
- Side quests branch and rejoin the main path
- Track choices in variables for Phase 2 inheritance
- Use <<if>> gates for content that requires prior choices

5. PHONE UI WIDGET:
<<widget "phone">>
  Renders a phone-screen overlay with:
  - Text message threads (Jess, Riley, others)
  - Instagram feed simulation
  - Discord DM view
  Accepts sender, message, timestamp, and optional image
<</widget>>

6. TWITCH CHAT WIDGET:
<<widget "twitchchat">>
  Scrolling chat simulation with:
  - Array of pre-written messages cycling
  - Donation alerts with sound
  - Mood-reactive message pools (neutral, hype, toxic, thirsty)
  Uses $chatMood to select message pool
<</widget>>

7. INTIMATE CONTENT:
- All adult scenes are written in full
- No fade-to-black, no euphemisms
- Content intensity marked with fire emoji in passage metadata
- Use <<nobr>> for unbroken prose sections

8. STYLING:
- Dark theme: #0a0a0f background, #e0e0e0 text
- Accent purple: #9b59b6 (matches LED aesthetic)
- Font: 'Inter' for UI, 'Merriweather' for narrative prose
- Chat bubbles: left-aligned (others) and right-aligned (Ethan)
- Stat bars: colored gradients with smooth transitions
- Choice buttons: outlined, hover-fill, no default Twine styling

9. OPEN WORLD ELEMENTS:
- After main passage, offer exploration: "Look around the apartment" / "Check phone" / "Go outside"
- Each exploration node has 2-3 interactions before funneling back to main story
- Time-of-day system: Morning / Afternoon / Evening / Night / Late Night
- Some side content only available at certain times
- Map system: Apartment / Gym / Convenience Store / Riley's Place / City Streets

10. PASSAGE NAMING CONVENTION:
R[release]-[scene]-[variant]
Example: R1-bedroom-intimate, R1-riley-dm-choiceA, R1-end-datenight

11. SAVE SYSTEM:
- Autosave at each release boundary
- Manual save slots (8)
- "Stats so far" review screen accessible from sidebar

12. First person perspective throughout. Ethan narrates everything.
No em dashes in any text. Use commas, periods, or line breaks instead.
Writing style: raw, confessional, contemporary. Short sentences mixed with
longer flowing internal monologue. Modern internet-literate voice.

BUILD EACH PASSAGE as a complete Twee/SugarCube passage with:
:: PassageName [tags]
Full narrative content with embedded macros for choices, stat changes,
and UI elements. Include all widget calls, variable sets, and
conditional branches inline.