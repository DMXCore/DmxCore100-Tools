# TouchOSC

`Grand Hall.tosc` is the layout built in the video "Control your lights from TouchOSC":
a phone-sized panel (640 x 860) for the DMX Core 100 with

- four look buttons: two cues (`/dmxcore/cue/CUE2`, `/dmxcore/cue/CUE4`) and two presets
  (`/dmxcore/preset/PRESET2`, `/dmxcore/preset/DANCE`), plus All Off (`/dmxcore/preset/ALL_OFF`)
  and Stop (`/dmxcore/cuecontrol/stop`);
- a master fader on `/dmxcore/dimmer/master` (sends and receives);
- a Storm button on `/grandhall/storm`, an example of your own address for an input trigger;
- live feedback: every button listens on `/dmxcore/active/<cue|preset|timeline>/<code>` and
  lights while that item plays, and the status line shows `/dmxcore/status/text`.

Open it in TouchOSC, set the OSC connection's host to the unit (Browse finds it by name),
send port 8000, receive port 9000, and register the device under Control & Integrations >
OSC Clients with feedback port 9000 and "Send device status updates" on. Change the codes
in the buttons' messages to match your own cues and presets.

Preset buttons send the address with no argument on purpose: on a preset address a numeric
argument is the fade time in milliseconds, and a TouchOSC button sends its value (1, then 0 on
release).

Reference: https://docs.dmxcore.com/dmx-core-100/integrations/osc-open-sound-control/
