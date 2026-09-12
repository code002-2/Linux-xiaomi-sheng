# Xiaomi Pad 6S Pro audio fix

[中文](../声音修复.md) | **English**

## 1. Firmware

Copy the `cs35l43` related `.wmfw` and `.bin` files extracted from Android into `/lib/firmware/cirrus/` on your Linux install.

> These files can be extracted from Android, or obtained from the upstream repository.

## 2. Rename the firmware (fixes loading errors)

In `/lib`, run the following to create the names the driver expects:

```bash
cd /lib/firmware/cirrus/
for pos in BLH BLL BRL TLH TLL TRL; do
    sudo cp cs35l43-dsp1-spk-prot.wmfw "cs35l43-DSP1-spk-prot-(null)-${pos}.wmfw" 2>/dev/null
    sudo cp cs35l43-dsp1-spk-prot.wmfw "cs35l43-DSP1-spk-prot--(null)-${pos}.wmfw" 2>/dev/null
    sudo cp "${pos}-cs35l43-dsp1-spk-prot.bin" "cs35l43-DSP1-spk-prot-(null)-${pos}.bin" 2>/dev/null
    sudo cp "${pos}-cs35l43-dsp1-spk-prot.bin" "cs35l43-DSP1-spk-prot--(null)-${pos}.bin" 2>/dev/null
done
```

## 3. Initialise the audio path

Run the following to set up the audio matrix routing and activate the driver:

```bash
# start pd-mapper
pd-mapper &

# set up the virtual matrix route and volume
amixer -c 0 cset name='SECONDARY_MI2S_RX Audio Mixer MultiMedia1' 1
amixer -c 0 sset 'stream0.vol_ctrl0 MultiMedia1 Playback Volu' 80%

# save the ALSA state
alsactl store 0
```

## 4. Verify and troubleshoot

- **Playback test**: `speaker-test -D plughw:0,0 -c 2`
- **Restart the services**: if the desktop audio stack shows no output device, run `systemctl --user restart pipewire wireplumber`
- **Add a sink manually**: `pactl load-module module-alsa-sink device=hw:0,0`
