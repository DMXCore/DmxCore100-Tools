# TouchOSC

`Grand Hall.tosc` is the layout built in the video "Control your lights from TouchOSC":
a phone-sized panel (640 x 860) for the DMX Core 100 with

- four look buttons: two cues (`/dmxcore/cue/CUE2`, `/dmxcore/cue/CUE4`) and two presets
  (Bar Red on `/dmxcore/preset/BAR_RED`, and Bar Blue on `/dmxcore/preset/BAR_BLUE/fade 4000`, a
  preset with its own four-second fade: the message sends a constant on the press only), plus All Off
  (`/dmxcore/preset/ALL_OFF`) and Stop (`/dmxcore/cuecontrol/stop`);
- a master fader on `/dmxcore/dimmer/master` (sends and receives);
- a Storm button on `/grandhall/storm`, an example of your own address for an input trigger;
- live feedback: the unit sends an item's state on its trigger address, with the code as stored
  (`/dmxcore/preset/BAR_RED 1` while Bar Red is applied, `0` when it is not), so a plain button
  is one message with Send and Receive both ticked and lights while its item plays. Bar Blue and
  Storm send on other addresses (`/fade 4000`, your own `/grandhall/storm`), so each has a second,
  receive-only message on its item's address (`/dmxcore/preset/BAR_BLUE`, and
  `/dmxcore/timeline/<code>` for the timeline the Storm trigger plays). The status line shows
  `/dmxcore/status/text`.

Open it in TouchOSC and set the OSC connection: host is the unit (Browse finds it by name),
or `127.0.0.1` when TouchOSC runs on the same computer as the DMX Core desktop software; send
port 8000, receive port 9000. Connections live in the TouchOSC app, not in the layout file.
Then register the device under Control & Integrations > OSC Clients, source IP the same
address, feedback port 9000 and "Send device status updates" on. Change the codes
in the buttons' messages to match your own cues and presets.

The buttons send their value as TouchOSC does by default, 1 on press and 0 on release; the
unit reads a trigger address that way (any non-zero number is a press, 0 is ignored), so
nothing needs changing on the button. A plain preset button fades over the device default. Bar Blue shows the
other way, `/dmxcore/preset/<code>/fade <ms>` with the time as the value, which leaves every other
button alone. A fader on `/dmxcore/fadetime` (0 to 5000 ms) would instead set the time for
everything this panel sends, like a time fader on a console.

The layout carries one small document script: when it loads it sends `/dmxcore/hello`, so the
unit replies with its full state and every button and fader starts out right, and it sends
`/ping` every ten seconds so a phone that comes back from sleep gets the state again. The
buttons and faders themselves are plain messages; nothing else in the file is scripted.

Reference: https://docs.dmxcore.com/dmx-core-100/integrations/osc-open-sound-control/
