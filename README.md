# sign/speller

**Real-time ASL fingerspelling to text, in your browser.**

Spell words with your hand in front of a webcam using the ASL fingerspelling alphabet, then have the sentence read out loud. A picture of every letter stays on screen, so someone who doesn't know sign language can learn while they spell. It runs entirely in the browser: nothing to install, and no video leaves your device.

**Try it:** https://mukundkapoor26.github.io/sign-speller/ · [project page](https://mukundkapoor.com/projects/sign-speller/)

**This covers fingerspelling only:** the 26 letters of the American manual alphabet, one at a time. Real sign language (ASL) is a full language with its own signs and grammar. This is not a replacement for it or for an interpreter.

## What it does

- Tracks your hand with MediaPipe and recognises the ASL alphabet (A–Z)
- Hold a letter still for about half a second to type it; a ring fills while you hold
- J and Z are drawn in the air: make an I and hook the pinky down for J, point and draw a Z for Z
- Word suggestions as you spell, auto capitals, and a speak button (the browser's own voice)
- A letter guide with a drawing of every handshape, flipped to match how you see yourself
- **Teach:** pick a letter in the guide, hold it, press teach. It learns your hand, which helps most with the thumb letters (a e m n s t)
- **Learn mode:** tap a letter to keep it on screen while you practise it, or type a word and spell it letter by letter, with feedback on each one. Nothing gets typed while you learn
- **Show signs:** everything you type, by hand or keyboard, appears on screen as large hand pictures facing the viewer, so whoever is watching your shared screen can read it. **Play** fingerspells your last sentence one big letter at a time
- Camera picker: use your laptop camera, an iPhone through Continuity Camera, or a USB webcam. It remembers your choice
- Minimal black-and-white UI that works on phones, with keyboard and tap fallbacks

## Gestures

Gestures use an **open hand with the fingers spread** (not a letter), so they don't collide with the alphabet.

| Gesture | Action |
| --- | --- |
| Hold a letter still | Type it |
| Relax, drop or slide your hand, then hold again | Double letter |
| Open hand, swipe → | Space |
| Open hand, swipe ← | Delete |
| Open hand, swipe ↓ | Full stop |
| Open hand, swipe ↑ | Speak the last sentence |
| Both hands open, held | Clear (tap undo to bring it back) |

## Keys

| Key | Action |
| --- | --- |
| Click the text | Type normally |
| Space / . / Backspace | Space / full stop / delete |
| Enter | Speak |
| Tab | Accept the first suggestion |
| G | Letter guide |
| S | Show your text as signs |
| P | Play the last sentence as signs |
| C | Switch camera (or use the camera menu in the dock) |
| K | Switch between camera mode and keyboard mode (or the camera / keyboard button) |
| H | Hide the UI (for recording) |
| ` | Copy the current hand landmarks (for bug reports) |

## How the recognition works

Each frame, 21 hand landmarks become 20 features measured in the hand's own frame, so it doesn't matter where the hand is or which way it's turned. The features are finger bends, finger spread, where the thumb tip is and how deep it sits, and the direction the hand points. The palm side is worked out from the way curled fingers fold, so left and right hands both work. A frame is matched against three kinds of letter template:

1. MediaPipe readings of real ASL alphabet photos from [Lifeprint / ASL University](https://www.lifeprint.com/asl101/fingerspelling/abc.htm). Only the measured numbers are stored, not the photos.
2. A small 3D hand model of every letter, corrected to match how MediaPipe reports real hands
3. Your own samples from teach

On reference photos it picks the right letter about 4 times in 5 (82%). For that test, each photo's own copies and near-duplicates were removed from the templates first. A, E, F, G, H, L, N, P, Q, R, T, U, V, W and Y did best. B, C, K, M, O, S and especially X are weaker. It hasn't been measured on a live webcam yet, and real lighting and angles will be harder than clean photos. Teach is the fix for any letter that doesn't work for your hand.

## Run it locally

It's one HTML file. Serve the folder and open it in Chrome:

```bash
python3 -m http.server 5180
```

Then open http://localhost:5180 and allow the camera. To use an iPhone as the camera on a Mac, turn on Continuity Camera and pick it from the camera menu in the dock.

## Credits

- Hand drawings (`signs/`): [wpclipart.com via Wikimedia Commons](https://commons.wikimedia.org/wiki/Category:American_Sign_Language_letters), public domain
- Handshapes checked against [Lifeprint / ASL University](https://www.lifeprint.com/asl101/fingerspelling/abc.htm) (Dr. Bill Vicars)
- Hand tracking: [MediaPipe Hand Landmarker](https://ai.google.dev/edge/mediapipe/solutions/vision/hand_landmarker)

## Licence

MIT
