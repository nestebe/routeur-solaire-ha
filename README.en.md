# 🌞 Home Assistant solar diverter

[🇫🇷 Français](README.md) · **🇬🇧 English**

Heat the water tank with solar surplus, power modulated from 0 to 2200 W, driven by Home Assistant.

## Parts

| Part | Purpose |
|---|---|
| **LSA-H3P40YB** 40 A, version **without "-F"** | Power regulator |
| **Shelly Dimmer 0/1-10V PM Gen3** | 0-10 V control of the LSA, driven over Wi-Fi by HA |
| Aluminium heat sink (LCTC H-110) + thermal paste | LSA cooling |
| IP65 enclosure, depth ≥ 150 mm, with vents | Protection |
| 2 A fuse | Shelly protection |
| Grid metering (ZLinky TIC or Shelly Pro EM) | Surplus seen by HA |
| 20 A breaker + 30 mA type A RCD, 2.5 mm² cable | Water heater circuit |

⚠️ The **LSA-H3P40YB-F** version does not work with an external command.

## Wiring

![Wiring diagram](images/wiring-en.svg)

![Control terminal](images/control-terminal-en.svg)

## Photos

<table>
  <tr>
    <td align="center"><img src="images/photo-prototype.jpg" alt="Test build" width="380"><br><em>Test build on a board</em></td>
    <td align="center"><img src="images/photo-coffret.jpg" alt="Final build" width="380"><br><em>Final build</em></td>
  </tr>
</table>

## Settings

- Shelly: **1-10V** mode, min brightness on toggle **0**, no min/max remapping.
- HA regulation: every 20 s, adjust the Shelly to keep ~200 W of export. Starting point: [Mathieu Carbou's YaSolR](https://yasolr.carbou.me/blog/2024-07-01_shelly_solar_diverter).

## Dimmer calibration

The LSA does not respond over the Shelly's full range: you need to find the useful range.

Tank **cold** (the thermostat must call for heat), bulb test passed first.

1. Set the Shelly to 10, 20, 25, 30, 35, 40, 50… 100 %, wait 10 s at each step.
2. Write down the power drawn (grid metering or clamp meter).
3. **Low threshold** = first % where it heats (~100 W).
4. **High threshold** = % above which power stops increasing.

On my build: **≈ 100 W at 30 %**, ≈ +38 W per %, **full power around 90 %**. The HA regulation only works between these two values.

## Safety

- Work with power off. Water heater thermostat **always in series**, never bypassed.
- Earth on the water heater and the LSA heat sink.
- The LSA has no thermal protection: heat sink and ventilated enclosure required.
- Test with a 60 W incandescent bulb first.

## Contact

devestebe@gmail.com
