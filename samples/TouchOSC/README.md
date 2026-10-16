# TouchOSC

`Grand Hall.tosc` is the layout built in the video "Control your lights from TouchOSC":
a phone-sized panel (640 x 860) for the DMX Core 100 with

- four look buttons: two cues (`/dmxcore/cue/CUE2`, `/dmxcore/cue/CUE4`) and two presets
  (`/dmxcore/preset/PRESET2`, and Dance Club on `/dmxcore/preset/DANCE/fade 4000`, a preset
  with its own four-second fade: the message sends a constant on the press only), plus All Off
  (`/dmxcore/preset/ALL_OFF`) and Stop (`/dmxcore/cuecontrol/stop`);
- a master fader on `/dmxcore/dimmer/master` (sends and receives);
- a Storm button on `/grandhall/storm`, an example of your own address for an input trigger;
- live feedback: every button listens on `/dmxcore/active/<cue|preset|timeline>/<code>` and
  lights while that item plays, and the status line shows `/dmxcore/status/text`.

Open it in TouchOSC and set the OSC connection: host is the unit (Browse finds it by name),
or `127.0.0.1` when TouchOSC runs on the same computer as the DMX Core desktop software; send
port 8000, receive port 9000. Connections live in the TouchOSC app, not in the layout file.
Then register the device under Control & Integrations > OSC Clients, source IP the same
address, feedback port 9000 and "Send device status updates" on. Change the codes
in the buttons' messages to match your own cues and presets.

The buttons send their value as TouchOSC does by default, 1 on press and 0 on release; the
unit reads a trigger address that way (any non-zero number is a press, 0 is ignored), so
nothing needs changing on the button. A plain preset button fades over the device default. Dance Club shows the
other way, `/dmxcore/preset/<code>/fade <ms>` with the time as the value, which leaves every other
button alone. A fader on `/dmxcore/fadetime` (0 to 5000 ms) would instead set the time for
everything this panel sends, like a time fader on a console.

Reference: https://docs.dmxcore.com/dmx-core-100/integrations/osc-open-sound-control/
