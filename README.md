# ChickenPick

**A playable chicken-pickin' Tele desk for your MIDI keyboard. Hold a chord and a tempo-synced chicken engine fires muted ghosts, open twang, double-stops and hybrid snaps on the grid of your BPM and key, with a country walking bass and train-beat drums underneath. Record a take and export a DAW-ready WAV and MIDI that land on bar 1.** Live: **https://chickenpick.vercel.app**

People want a Tele they can chicken-pick on ([Jason Testifies, Nov 2026](https://x.com/jasontestifies/status/2111974912655061260)). Country guitar expression tools usually live as plugins (e.g. pedal-steel multibend as a free MIDI legato script — [VSTfinds](https://x.com/vstfinds/status/2102193661731652068)). ChickenPick makes the chicken-pickin' Tele the instrument: play it live from a MIDI keyboard in the browser, nothing to install, no DAW open, change the recipe while you play.

## Play it
1. **Your loop:** BPM (60–180), key, mode, bars (4/8/16) and chords (one per bar, e.g. `G C D G`). These are saved in your browser. Changing the key transposes your chords and your take.
2. **Play:** your MIDI keyboard plays the Tele right away and never starts the transport. Press **▶ Play chicken + band** to run the chicken engine, the country bass and the train-beat drums on the audio clock. When the transport is stopped you hear the raw Tele voice.
3. **Chicken pickin':** choose from 7 recipes: Classic Chicken, Train Twang, Double-Stop Snap, Ghost Run, Nashville Hybrid, Slow Porch and Hold (raw Tele). Edit the 16-step grid (M mute / O open / D double-stop / S snap / H hold / - rest). Set mute depth, pick length and snap, and pick drums: train, shuffle, porch or off. Every change lands on the next step, with no restart.
4. **Voice:** Tele Twang, Chicken Mute, Honky Wire or Porch Snap. Each is synthesized and named for how it's made. Controls: cutoff, resonance, attack (a real ramp) and release (≥10 ms). **Scale lock** snaps any key you press to your key.
5. **Rec take:** while playing, press Rec and play. Each pass overdubs onto the loop (snap to 1/16 is optional). The take feeds the chicken engine and is what the export renders. With no take, the export chicken-picks your chords one per bar.

## MIDI controls
- Notes and velocity
- **CC64** sustain
- **CC1 mod wheel** = chicken mute depth
- **CC74** = cutoff
- **Pitch bend** ±2 semitones
- **CC123** all notes off
- MIDI clock and start are ignored: notes never start the transport.
- **MIDI in select** and **MIDI out select.** Out mirrors what you play (ch 1), the bass (ch 2) and the drums (ch 10). Stop sends All Notes Off.
- **Audio out select** (`setSinkId`, with a note if the browser can't). No audio input is used.
- On-screen keys and computer keys (A W S E D F T G Y H U J K O L P ;, Z/X octave) are a fallback only.

## Export
- **WAV:** `chickenpick-<recipe>-<bpm>bpm-<key>.wav`. 48 kHz, 24-bit stereo, rendered with OfflineAudioContext. The length is exactly your bars (92 BPM × 8 bars = 1,001,739 samples) and the downbeat is at sample 0. The limiter's look-ahead is measured and removed. The ring-out tail is folded into the start so it loops seamlessly, and the peak is ≤ −1 dBFS. The render is deterministic: the noise uses a seeded generator, with no `Math.random`.
- **MIDI:** same name, `.mid`. It has your tempo, 4/4, key signature and a bar marker per chord, plus one track per chair:
  - Chicken Tele (synth picks)
  - Country Bass (synth)
  - Train Beat (synth)
- Drop both at bar 1 of a session at the same BPM.

## Sounds
Everything is synthesized in your browser, and every voice says so: bright saw + square Tele twang, filtered noise mute ghosts, detuned honky saws, triangle porch snaps, a sine/saw walking bass, and a seeded-noise snare and hat. There are no samples and no CDN, so nothing can fail to load.

## Pricing
- **Launch (no Lemon Squeezy product configured yet):** everything is free ("Checkout opening soon"). Gating turns on only when `LEMON.storeId` and `LEMON.productId` are set, and keys are only accepted for that store and product.
- **Once checkout is live:** playing, recording, every recipe and voice, and exports up to 8 bars are free. A **$19 one-time** license unlocks 16-bar exports.
- **Why one-time:** it's a single focused playable instrument that runs fully in the browser (no server or AI cost per user), it matches the other WorkinWithAI desks, and players buy instruments once.
- **Where to sell:** Lemon Squeezy (license keys, merchant of record for VAT and sales tax). Gumroad is the backup.

## QA
- `qa/s9.py <url>`: AUDIO-ENGINE-RULES §9 checks 1–7, plus simulated Web MIDI (note on/off, velocity, CC64, CC1 → muteDepth, clock ignored, MIDI out), the MIDI file, stop silence, persistence and the license gate. Evidence is in `checks/`.
- `qa/no_unpinned.sh [url]`: check 7 grep.

No accounts, no database, no tracking. © 2026 WorkinWithAI.
