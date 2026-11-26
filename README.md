# NBM Fitness Pulse

An interactive tablet prototype for a gym-equipment check-in kiosk. The screen is mounted on a single machine, Treadmill 04 in the cardio zone of a fictional gym called Riverside Fitness, and a member taps it on their way onto the machine.

The whole thing is one self-contained HTML file. There is no build step, no package manager and no network calls. Open `index.html` in a browser and it runs.

## Running it

Double-click `index.html`, or serve the folder if you prefer a real origin:

```
python3 -m http.server 8000
```

Then open `http://localhost:8000`. The frame is sized for a 520 x 832 portrait tablet, so a desktop browser shows it as a device mock-up rather than filling the window.

## The flow

Nine screens, wired as one journey:

| Screen | What it does |
| --- | --- |
| Idle | Attract mode: live clock, cycling tips, sanitation status, and the two ways in |
| Equipment info | Who the trainer is, what the machine is for, a mock video guide, safety steps |
| Verifying | Short spinner standing in for the wristband read |
| Welcome | Personal records on this machine, recent sessions, an unread note from the trainer |
| Plan | The trainer-assigned workout and the five-week programme it sits inside |
| Active session | Live timer, pace, distance, calories, heart-rate zone, stage transitions |
| Summary | Totals, personal-best and target badges, confetti, updated history |
| Leaderboard | Fastest times, filterable by distance (1K to 10K) and period (daily to annual) |
| Logout | Brief confirmation, then back to idle |

Two ways to sign in from the idle screen: tap the wristband, or enter a four-digit member ID on the keypad. Both land on the same verifying step.

## Things worth clicking

- The trainer note on the welcome screen, which opens as a message rather than a notification.
- The video guide on the equipment-info screen. The play button drives a progress bar; there is no real video file.
- The leaderboard tabs. Times are scaled from the 5K dataset by distance ratio, so switching distance recomputes rather than showing placeholder rows.
- The end of a session. A personal best only fires if the simulated average pace beats 4:55/km, so it depends how long you leave it running.

One screen is not reachable by tapping: the idle-timeout warning, which asks whether you are still there and logs out after a ten-second countdown. Trigger it from the browser console:

```js
__demoIdleWarning()
```

## What is fake

Everything. This is a prototype for showing a flow, not a working product.

- Member, trainer, gym and leaderboard names are invented.
- Session metrics are simulated on a one-second tick, not read from any machine.
- Session history, records and programme weeks are hard-coded constants at the top of the script block.
- Nothing is saved. Reloading the page resets it.

## Design notes

The theme is deliberately loud: a deep violet base with violet, pink, teal and gold accents, and rounded display type. Gym lighting is harsh and the screen competes with a room full of other things, so the palette is built for contrast and for reading at arm's length while moving. Tap targets are sized for someone standing up and slightly out of breath rather than for a mouse.

There is one committed visual world and no light-mode toggle. Reduced-motion preferences are respected: all animation collapses if the operating system asks for it.
