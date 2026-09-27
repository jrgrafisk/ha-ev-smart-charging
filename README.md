# EV smart charging – Home Assistant blueprint

**🇬🇧 English** · [🇩🇰 Dansk](#-dansk)

Plug in the car and it charges **straight away** to an *immediate target* (e.g. 50 %).
Then it pauses, finds the **cheapest contiguous window** in the next *N* hours that is
long enough to reach the *final target* (e.g. 85 %), and resumes when that window starts.

- Works with **any charger or car Home Assistant can start and stop** – the charger
  doesn't need to know anything about electricity prices. Use its on/off switch, or your
  own start/stop actions (a button, an Easee/Zaptec/Monta service, or the car itself).
- Prices from **Energi Data Service** or the **HACS Nordpool** integration
  (`raw_today` / `raw_tomorrow`, hourly or 15-minute prices). Tariffs included if your
  price sensor includes them.
- A master switch turns it off: the car then charges normally (straight to full).
- If Home Assistant restarts while waiting and the window was missed, it charges at once.

## Install

[![Import blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fjrgrafisk%2Fha-ev-smart-charging%2Fblob%2Fmain%2Fev_smart_charging.yaml)

1. Create three helpers (*Settings → Devices & services → Helpers*):
   - **Toggle** – e.g. "EV smart charging" (the master switch; turn it on)
   - **Dropdown** – e.g. "EV charge phase" (any single option; the blueprint sets the options)
   - **Date and/or time** – e.g. "EV cheap charge start" (choose *date and time*)
2. Import the blueprint (button above) and create an automation from it.
3. Pick your car's battery (SoC) sensor, plug sensor, the charger switch **or** start/stop
   actions, the three helpers and your price sensor. Adjust targets, window, battery size
   and effective charging power (≈ charger power × 0.9).

| Charger / car | How to control it |
|---|---|
| Easee | switch *…is enabled*, or actions `easee.action_command` start/stop |
| Zaptec (HACS) | actions: press the *resume* / *stop* buttons |
| Wallbox | switch *pause/resume* |
| go-e | switch |
| Monta, Clever | their start/stop actions |
| Tesla Wall Connector | read-only – control the **car** (Tesla integration) instead |

**Accuracy:** the car's SoC updates every few minutes in most car integrations, so it may
overshoot the targets by a few percent.

---

## 🇩🇰 Dansk

Sæt bilen til, og den lader **med det samme** op til et *straks-mål* (fx 50 %). Derefter
pauser den, finder den **billigste sammenhængende periode** inden for de næste *N* timer,
der er lang nok til at nå *slutmålet* (fx 85 %), og lader videre, når perioden starter.

- Virker med **alle ladere og biler, som Home Assistant kan starte og stoppe** – laderen
  behøver ikke kende elpriser. Brug dens tænd/sluk-kontakt eller dine egne start/stop-handlinger.
- Priser fra **Energi Data Service** eller **Nordpool (HACS)**, inkl. tariffer hvis din
  pris-sensor har dem med.
- Hovedkontakten slår det fra: så lader bilen som normalt, direkte til fuld.
- Genstarter Home Assistant, mens den venter, og perioden er passeret, lader den med det samme.

### Installation

1. Opret tre hjælpere (*Indstillinger → Enheder og tjenester → Hjælpere*):
   **Kontakt** (hovedkontakt – slå den til), **Rulleliste** (ladefase – vilkårlig
   valgmulighed, blueprinten sætter resten) og **Dato og/eller tid** (vælg *dato og tid*).
2. Importér blueprinten med knappen ovenfor og opret en automation ud fra den.
3. Vælg bilens batteri-sensor (SoC), stik-sensor, laderens kontakt **eller** start/stop-
   handlinger, de tre hjælpere og din pris-sensor. Justér mål, periode, batteristørrelse
   og effektiv ladeeffekt (≈ laderens effekt × 0,9).

Se tabellen ovenfor for hvordan populære ladere styres.

## License

MIT
