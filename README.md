# Hand MIDI Controller - Professional Edition

A high-performance, real-time hand tracking MIDI controller using MediaPipe and OpenCV. Transform your hand movements into MIDI control signals for music production, VJing, and creative performances.

## ✨ Features

### Core Functionality
- **Dual Hand Tracking**: Independent tracking of both hands with 6 parameters each
- **12 MIDI CC Outputs**: Organized in logical blocks (CC 1-6 left hand, CC 7-12 right hand)
- **Virtual MIDI Device**: Creates "HandMIDI Virtual" device for DAW integration
- **Zero Latency**: Optimized for real-time performance (30+ FPS)

### Advanced Features
- **Click-Drag Region Selection**: Define custom X/Y mapping bounds
- **Retina Display Optimization**: Crisp UI scaling for high-DPI displays
- **Professional UI**: Cyberpunk-styled overlay with real-time parameter visualization
- **Multi-Camera Support**: Cycle between available cameras with 'V' key
- **Smoothing Algorithms**: Exponential moving average for stable output
- **Preset System**: 5 built-in presets optimized for different use cases
- **Runtime Configuration**: Adjust smoothing and sensitivity on-the-fly
- **Extended Gestures**: Fist detection, finger spread, velocity tracking
- **Hand Distance**: Track distance between both hands for expressive control
- **Multi-Finger Tracking**: Optional thumb-to-finger distance for all fingers

### Hand Parameters
#### Left Hand (CC 1-10, 11-23 advanced)
1. **X-Axis** (CC 1): Horizontal hand position
2. **Y-Axis** (CC 2): Vertical hand position (inverted for natural control)
3. **Pinch** (CC 5): Thumb-index finger distance
4. **Palm** (CC 7): Hand openness/spread
5. **Rotation** (CC 9): Hand rotation angle
6. **Thumb-Middle** (CC 11): Thumb to middle finger distance (optional)
7. **Thumb-Ring** (CC 13): Thumb to ring finger distance (optional)
8. **Thumb-Pinky** (CC 15): Thumb to pinky distance (optional)
9. **Fist** (CC 17): Closed fist detection (optional)
10. **Spread** (CC 19): Finger spread detection (optional)
11. **Velocity** (CC 21): Hand movement speed (optional)

#### Right Hand (CC 3-10, 12-23 advanced)
1. **X-Axis** (CC 3): Horizontal hand position
2. **Y-Axis** (CC 4): Vertical hand position (inverted for natural control)
3. **Pinch** (CC 6): Thumb-index finger distance
4. **Palm** (CC 8): Hand openness/spread
5. **Rotation** (CC 10): Hand rotation angle
6. **Thumb-Middle** (CC 12): Thumb to middle finger distance (optional)
7. **Thumb-Ring** (CC 14): Thumb to ring finger distance (optional)
8. **Thumb-Pinky** (CC 16): Thumb to pinky distance (optional)
9. **Fist** (CC 18): Closed fist detection (optional)
10. **Spread** (CC 20): Finger spread detection (optional)
11. **Velocity** (CC 22): Hand movement speed (optional)

#### Both Hands
12. **Distance** (CC 23): Distance between both hands (optional)

*Note: Advanced parameters (CC 11-23) are disabled by default. Enable them using presets or configuration file.*

## get it running in 30 seconds

requires [uv](https://docs.astral.sh/uv/getting-started/installation/).

```bash
cd hand-midi-controller
uv run hand_midi_controller_final.py
# or: ./run.sh
```

that's it. "hand midi controller" should appear in your daw's midi inputs.

## first time setup checklist

1. **install uv** if you don't have it:
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **run it** — uv handles python and dependencies automatically:
   ```bash
   uv run hand_midi_controller_final.py
   ```

3. **check your daw**:
   - open logic pro / ableton / your daw
   - create new midi track
   - set input to "hand midi controller"
   - load any synth
   - wave your hands!

## 🎮 Controls

| Key | Action |
|-----|--------|
| Q | Quit application |
| M | Cycle UI modes (minimal/cyberpunk/debug) |
| V | Cycle between cameras |
| S | Save current configuration |
| C | Clear custom mapping area |
| 1-5 | Load preset (1=performance, 2=studio, 3=precise, 4=experimental, 5=minimal) |
| +/- | Adjust position smoothing (more/less smooth) |
| [/] | Adjust gesture smoothing (more/less smooth) |
| {/} | Adjust pinch sensitivity (more/less sensitive) |
| Click+Drag | Select custom X/Y mapping region |

## presets

quickly switch between optimized configurations with number keys 1-5:

### 1 - performance preset
optimized for live performance with maximum expressiveness:
- high sensitivity for responsive control
- all gestures enabled (velocity, distance, fist, spread)
- extended finger distance tracking
- minimal smoothing for real-time feel
- cyberpunk ui mode

### 2 - studio preset  
balanced settings for studio recording:
- increased smoothing for stable recordings
- velocity tracking enabled for dynamics
- minimal ui for clean video
- optimized thresholds for consistent takes

### 3 - precise preset
maximum control resolution:
- 14-bit midi cc for ultra-precise control
- heavy smoothing for minimal jitter
- tight thresholds for accurate gestures
- velocity and distance tracking enabled

### 4 - experimental preset
all features enabled for exploration:
- every gesture type active
- all finger distance combinations
- fist, spread, pointing detection
- debug ui with full telemetry
- ideal for discovering new control methods

### 5 - minimal preset
basic hand tracking only:
- position (x/y) and pinch only
- lightweight processing
- clean interface
- perfect for simple setups

## midi mappings

### basic controls (always active)
left hand:
- **cc01** - x position
- **cc02** - y position  
- **cc05** - thumb-index pinch
- **cc07** - palm openness
- **cc09** - hand rotation

right hand:
- **cc03** - x position
- **cc04** - y position
- **cc06** - thumb-index pinch
- **cc08** - palm openness  
- **cc10** - hand rotation

### advanced controls (enable in presets or config)
left hand advanced:
- **cc11** - thumb-middle distance
- **cc13** - thumb-ring distance  
- **cc15** - thumb-pinky distance
- **cc17** - fist detection
- **cc19** - finger spread
- **cc21** - hand velocity

right hand advanced:
- **cc12** - thumb-middle distance
- **cc14** - thumb-ring distance
- **cc16** - thumb-pinky distance  
- **cc18** - fist detection
- **cc20** - finger spread
- **cc22** - hand velocity

both hands:
- **cc23** - distance between hands

### runtime adjustments

tune your setup on the fly without restarting:

- **+/-** keys adjust position smoothing
  - lower = more responsive, jittery
  - higher = smoother, slight lag
  - range: 1-20 frames

- **[/]** keys adjust gesture smoothing  
  - affects pinch, palm, rotation
  - lower = instant response
  - higher = stable values
  - range: 1-20 frames

- **{/}** keys adjust pinch sensitivity
  - **{** = more sensitive (larger open threshold)
  - **}** = less sensitive (smaller open threshold)
  - watch the pinch values and tune to your hand size

## ui modes

run with different modes:
```bash
uv run hand_midi_controller_final.py --ui minimal  # clean, labels only
uv run hand_midi_controller_final.py --ui cyberpunk # neon meters
uv run hand_midi_controller_final.py --ui debug    # verbose info
```

## performance

if it's laggy:
- use minimal ui mode
- close other camera apps
- reduce smoothing in config
- use model_complexity=0 in config

## custom mapping areas

click and drag on the video to define a control zone. only hand movements in that area will generate midi 0-127. press `c` to clear.

## config

**new: comprehensive configuration guide!** see `CONFIGURATION_GUIDE.md` for detailed documentation on:
- preset selection and customization
- real-time adjustments during performance
- advanced midi mapping strategies
- use case examples (ambient, drums, video, sound design)
- troubleshooting and optimization tips

settings save to `hand_midi_config.json`. see `example_presets.json` for ready-to-use configurations.

quick config options:
- change cc numbers in cc_mappings
- adjust sensitivity multipliers
- modify smoothing windows
- set camera resolution
- enable/disable advanced gestures

## common issues & fixes

### "no module named cv2" or similar errors
run via uv so dependencies are resolved automatically:
```bash
uv run hand_midi_controller_final.py
# or: ./run.sh
```

### "no hands detected"
- better lighting helps (face a window)
- plain background works best  
- keep hands 1-3 feet from camera
- check camera permissions in system settings

### midi not showing in logic pro
1. quit logic pro completely
2. run the hand midi controller
3. reopen logic pro
4. check: track inspector → input → "hand midi controller"

### still stuck?
```bash
# clean install
rm -rf .venv
uv sync
uv run hand_midi_controller_final.py
```

## advanced

### multiple cameras
press `v` to cycle through available cameras. the app will detect all connected cameras on startup.

### custom cc mappings
edit the cc_mappings in config:
```json
"cc_mappings": {
  "left_x": {"cc": 1, "label": "l_x_pos", "color": [0, 255, 255], "enabled": true}
}
```

### performance tuning
```json
"model_complexity": 0,          // 0=faster, 1=more accurate
"position_smoothing": 3,        // lower = more responsive
"skip_frames": 1,              // process every Nth frame
"camera_width": 640,           // lower resolution = faster
"camera_height": 480
```

---

## 🎨 TouchDesigner Integration

Want to turn your hand gestures into sick reactive visuals? Check out `TOUCHDESIGNER_INTEGRATION.md` for:

- Real-time hand-to-visual mapping
- Velocity-reactive particle systems  
- Distance-controlled camera movements
- Pinch-triggered effects and shaders
- Complete .toe project examples

**Hand tracking + TouchDesigner = absolute peak creative tech!** 🔥

---

made for musicians who like to wave their hands around