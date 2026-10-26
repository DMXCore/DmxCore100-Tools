# Fixture Patch

Templates for importing a fixture patch into the DMX Core 100 under
**Lighting Setup > Fixtures > Import** in the Web UI:

- `fixture-patch-template.csv` - UTF-8 CSV
- `fixture-patch-template.xlsx` - Excel

Both hold the same five example fixtures on the built-in Generic profiles (PAR Wash RGB
and RGBW, LED Strip RGB, Bulb), so they import on any unit as they are. Replace the rows
with your own: one row per fixture, a name, a slot and start channel, and the fixture type.

| Column | Notes |
|---|---|
| Code | Leave empty for a new fixture (a code is assigned). The code of an existing fixture updates it |
| Name | |
| Enabled | Yes or No |
| Slot ID | 1 and up |
| Start Ch | 1-512. `2.101` style (slot.channel) also works when there is no Slot ID |
| Copies | 1-680 |
| Personality | Empty uses the profile's first personality |
| Zone Name | Matched ignoring case and extra spaces. A zone the unit does not have yet is an error, unless **Create missing zones** is on in the import dialog |
| Manufacturer, Profile | Matched to the profiles on the unit; anything not exact gets a suggestion in the import dialog |
| Profile Code | Optional exact profile, as written by the export |
| Template | Optional code of a patched fixture: the row gets its profile, personality, hidden functions and custom options |
| Copy Trims | Optional, one per copy, e.g. `100% 80%` |
| Hidden Functions | Optional, separated by `;` |
| Custom Options | Optional, `Name=Value; Name=Value` |

The easiest way to a full patch is usually to patch one fixture of each type on the unit,
export the patch (the export uses the same columns), add your rows, and import it.

Full description: [Fixture Setup - Importing Fixtures](https://docs.dmxcore.com/dmx-core-100/lighting/fixture-setup#importing-fixtures)
