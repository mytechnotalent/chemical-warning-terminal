![chemical-warning-terminal](https://raw.githubusercontent.com/mytechnotalent/chemical-warning-terminal/main/chemical-warning-terminal.png)

<br>

## FREE Reverse Engineering Self-Study Course [HERE](https://github.com/mytechnotalent/reverse-engineering)
## FREE Embedded Hacking Course [HERE](https://github.com/mytechnotalent/Embedded-Hacking)

<br>

# OPERATION IRON CURTAIN

### Remote Chemical Storage Warning Terminal
#### Act X of OPERATION COLD IRON

<br>

***
**LEGAL DISCLAIMER:**
The information, tools, and code provided in this repository and course are strictly for educational, research, and defensive purposes only.

You are explicitly prohibited from using any materials contained herein to access, test, modify, or exploit any device, network, or system that you do not own 100% or for which you do not have explicit, documented, and legally binding authorization to interact with.

By using this repository and course, you acknowledge and agree that:

1. Any illegal, unauthorized, or malicious use of this information is solely your responsibility.
2. The author(s) and contributor(s) of this repository and course shall not be held liable for any damages, legal repercussions, criminal charges, or unauthorized actions resulting from the use, misuse, or abuse of the contents herein.
3. You will comply with all applicable local, state, national, and international laws regarding cybersecurity and computer fraud.

**IF YOU DO NOT AGREE WITH THESE TERMS, DO NOT USE THIS REPOSITORY AND COURSE.**
***

<br>
<br>

> Hello again, friend.
>
> Act I was the lie. Act II was the door. Act III was the payload. Act IV was the
> payload that would not die. Act V was the payload that spreads. Act VI was the
> payload that steals. Act VII was the payload that takes orders. Act VIII was the
> payload that holds the building hostage. Act IX was the payload that becomes a
> weapon. This is the payload that does all of it at once.
>
> WHITEOUT disarmed the boom and cleared the marker, and for a shift the lane
> moved again. But a payload that learned every trick one at a time can be taught
> to run them together. The Ministry did not need a fleet, and it did not need a
> gate, and it did not need a building that cannot breathe. It needed one last
> node where every technique fires in the same breath, and it already owned the
> siren.
>
> The chemical storage warning terminal is the last node before the evacuation
> siren. A DHT11 watches the store temperature. A local maintenance remote asks
> for a warning. A safety link carries a sealed hazard, clear, or acknowledge
> command. A servo is the siren and vent actuator. A tower light says HAZARD,
> WATCH, or CLEAR. That is the whole contract, and it is a good one.
>
> FROSTLINE's finale implant in this one is the whole campaign in a single
> module. It runs a coordinated beacon that checks in on a schedule, it persists
> from the reserved sector so it survives a reflash, and it writes a sabotage
> marker into that sector with the real flash API. While the marker is present
> the terminal lies: it reports an all clear, it lights the green lamp, and it
> silences the siren, even when the store is in a declared hazard. This is the
> coordinated attack wrapped in a reassuring display: the device withholds the
> warning it exists to give.
>
> The green lamp still says CLEAR while a hazard is latched. The LCD still
> reports a state, and the state is a lie it was told to repeat. Underneath, the
> siren is being silenced by a payload with a polite label.
>
> Do not chase the symptoms one at a time. Cut the coordinated beacon. Break the
> persistence. Clear the sabotage marker. Defeat the anti-debug with GDB. Then
> seal the hazard command path so no hazard or clear command can ever be forged,
> make acknowledge ask for authorization instead of bypassing it, and make the
> terminal fail to the safe hazard state when the link is lost.
>
> The store is clear and the siren is silent. That is exactly the problem.

<br>

## THE SYSTEM

NorthPharma does not only move cold medicine and cold air and make the medicine.
It runs the city's controlled edge: the cold chain, the gates, the pipelines, the
air, the factories, and the warning systems that stand between a release and the
people downwind. The chemical storage warning terminal is the last node on that
edge. It watches the chemical store temperature, takes a local warning request
from a maintenance remote, verifies a sealed hazard, clear, or acknowledge
command from the safety control gateway, drives the siren and vent actuator, and
annunciates whether the store is in hazard, under watch, or clear.

A warning terminal is a simple machine. A temperature sensor reports the store, a
safety gateway authorizes a hazard, clear, or acknowledge command, the terminal
decides, a servo sounds the siren, and a tower light tells the responders whether
the store can be entered. The failure that matters is not a wrong number on a
screen. It is a siren that stays silent while a chemical hazard is declared, or a
terminal that quietly takes its orders from something other than the gateway.

The node in this repository is that hand. On a breadboard it is a toy: a Pico 2,
an SG90 servo that acts as the siren and vent actuator, a DHT11 that stands in for
the chemical store temperature sensor, an infrared remote that is the local
maintenance control, a button that is the manual acknowledge, a 1602 LCD that is
the hazard readout, three lamps, and a radio that is the safety control link.

Nothing about it looks broken. That is the horror of Act X. The code compiles,
the tests pass, the green lamp is lit, and the siren is being silenced by a
payload that reports the silence as safety.

<br>

## THE STAKES

Act I was a lie about temperature. Act II was a lie about people. Act III was a
lie about machinery. Act IV was a lie about remediation. Act V was a lie about
containment. Act VI was a lie about confidentiality. Act VII was a lie about
obedience. Act VIII was a lie about availability. Act IX was a lie about safety.
Act X is the lie that runs all of them at once: the terminal does not merely
refuse to warn, it reports the all clear while a hazard is live.

The node is coordinated, not buggy. A hidden finale implant runs a multi-stage
beacon that checks in every four ticks, re-installs from the reserved sector on
every boot, and writes a `0x58` sabotage marker into the reserved flash sector
`0x103FF000` with the real Pico SDK flash API. While the marker is present the
terminal forces the effective state to `CLEAR`, silences the siren, lights the
green lamp, and renders `ST:SAFE` and `M:SAB`. The operator sees a calm panel and
a green light, and the natural conclusion is that the store is safe. There is no
alert, because the sabotage never touches the sealed command path. It sits beside
it.

And here is the part that keeps the responders awake. The hazard path is already
authenticated. The cryptography is real and it is correct. The sabotage does not
break the cipher. It does something worse: it never needs the cipher. It is a
local condition that overrides the output regardless of what the authenticated
link says, so a perfectly valid hazard command can arrive and the siren will still
stay silent. The store is a hazard while every light says the terminal is fine.

That is not a warning terminal. That is a warning terminal that has become the
last lie before the evacuation.

<br>

## WHITEOUT

WHITEOUT is a resistance that does not exist on paper. It does not hold ground
and it does not hold press conferences. It reads firmware. When the boom was
disarmed, the crew kept pulling the thread. The marker led to the image, the image
led to the build, and the build led to a finale module no design review had named.

NIGHTINGALE is still the thread. Her last verified copy came off the tamper ring,
and it was clean. The thing that came after it was not. Somewhere between the
build server and the loading dock, someone signed an image that carries a
coordinated payload, and that image is silencing a siren right now.

WHITEOUT's job in Act X is not to break in. It is to prove the siren is being
silenced on purpose, in writing, with a debugger and a disassembler, then to cut
the beacon, break the persistence, clear the marker, and seal the hazard command
path so nothing can ever silence the store again. This is the incident-response
finale: the fix is not only a patch; it is a procedure.

<br>

## THE MACHINE

The firmware in this repository is the node's firmware. On a breadboard it is a
toy: a Pico 2, an SG90 servo that is the siren and vent actuator, a DHT11 that is
the chemical store temperature sensor, a VS1838B infrared eye that takes a local
maintenance remote, a 1602 LCD hazard readout over I2C, red/yellow/green
annunciator lamps, a manual acknowledge button, and an RYLR998 LoRa safety link to
a gateway.

Two things are open, and one thing is not what it seems. **The optical surface**
takes a warning or acknowledge request from any NEC remote, and it is not
authenticated. **The radio** carries the sealed hazard command path, and it is
authenticated correctly. The part that is not what it seems is the **finale
implant**: a module compiled only under a build flag called `SANDBOX_ONLY`,
invisible in the clean firmware, and present in the test and CTF builds. It runs
the coordinated beacon, re-installs from the reserved sector, and programs a
sabotage marker into that sector with the real flash API.

The face of the thing is honest in the way that matters least. The tower light
says HAZARD, WATCH, and CLEAR with total confidence, and the LCD shows the state,
the link, the storage zone, the temperature, and the sabotage marker. None of it
lies, except when the implant tells the display that the all clear is the state. A
healthy-looking terminal can still be the last lie before the evacuation.

<br>

## THE JOB

You do not have to be a hero. You have to be thorough. The store is carrying a
passenger that no design review admitted to, and the passenger is patient. Find
it, prove it, and take the warning back.

1. **Bring it up.** Build the clean firmware, wire the board, and confirm the node
   reads the store temperature, takes a local acknowledge, reaches the gateway,
   and drives the siren. Nothing looks broken because nothing is broken yet.
2. **Inspect the protocol.** Capture a sealed hazard command and read the body
   byte by byte. Understand what is authenticated and what the sabotage ignores.
3. **Hunt the finale.** Build the `SANDBOX_ONLY` image and find the coordinated
   beacon, the magic command `IRON-CURTAIN-BEACON-2026`, the `0x58` sabotage
   marker, the reserved-sector persistence, and the anti-debug trap. A single
   clean reflash will not disarm it.
4. **Respond.** Cut the coordinated beacon, break the persistence, clear the
   sabotage marker, and step past the anti-debug with GDB so the terminal cannot
   tell that a probe is attached. Then seal the hazard command path and make the
   terminal fail safe so no untrusted command and no lost link can ever silence
   the store again.

This document is the manual for the job. Work it on a breadboard. When every
green lamp is lit and the log says the store is clean, remember what it is: not a
healthy terminal. A payload that has learned to say safe.

Goodbye, friend.

<br>

## A NOTE ON THE ROADMAP

This project is Act X of **OPERATION COLD IRON**, the finale of the ten-act saga.
Act I was the sensor
([cold-chain-monitor](https://github.com/mytechnotalent/cold-chain-monitor)). Act
II was the door ([access-gate](https://github.com/mytechnotalent/access-gate)).
Act III was the valve
([pipeline-valve-controller](https://github.com/mytechnotalent/pipeline-valve-controller)).
Act IV was the air
([hvac-automation-node](https://github.com/mytechnotalent/hvac-automation-node)).
Act V was the web
([industrial-tamper-system](https://github.com/mytechnotalent/industrial-tamper-system)).
Act VI was the courier
([smart-logistics-dropbox](https://github.com/mytechnotalent/smart-logistics-dropbox)).
Act VII was the choir
([factory-andon-station](https://github.com/mytechnotalent/factory-andon-station)).
Act VIII was the vault
([datacenter-vent-controller](https://github.com/mytechnotalent/datacenter-vent-controller)).
Act IX was the fang
([smart-parking-barrier](https://github.com/mytechnotalent/smart-parking-barrier)).
Act X is the curtain. All ten are defended devices; the companion CTF repository
ships the compromised one. The investigation lives here:

- [OPERATION IRON CURTAIN CTF](https://github.com/mytechnotalent/CTF_chemical-warning-terminal)

The CTF is the red half, weaponized: six deep tasks, each with static analysis, a
dynamic proof under GDB, a hardware demonstration, and an in-place, same-size
patch. This repository is the defended device. The CTF repository is the breached
one. The full story lives at
[github.com/mytechnotalent/chemical-warning-terminal](https://github.com/mytechnotalent/chemical-warning-terminal).

---


<br>

## WHERE THIS FITS: OPERATION COLD IRON

This repository is **Act X (IRON CURTAIN)** of the ten-act OPERATION COLD IRON
saga. The malware track began in Act III; in Act IV it became persistence, in Act
V it became propagation, in Act VI it became exfiltration, in Act VII it became
command and control, in Act VIII it became availability and lockout logic, in Act
IX it became physical weaponization, and here it becomes the coordinated finale:
a beacon, persistence, and a sabotage marker in one payload, answered by a full
incident response. The full spine is in [SAGA.md](SAGA.md).

- Previous act: Act IX, IRON FANG, the smart parking barrier,
  [smart-parking-barrier](https://github.com/mytechnotalent/smart-parking-barrier)
- This act: Act X, IRON CURTAIN, the chemical storage warning terminal
- Post-ten backbone: TELESCREEN, the RP5 surveillance backbone (forthcoming)
- Companion CTF:
  [CTF_chemical-warning-terminal](https://github.com/mytechnotalent/CTF_chemical-warning-terminal)


<br>

## THE MINISTRY

The Ministry runs the state: the surveillance, the cold chain, the gates, the
pipelines, the air, the cabinets that hold what the state does not discuss, the
lockers that move it, the factories that make it, the buildings that keep the
record, the lanes that decide who passes, and the warning systems that decide who
is warned. NorthPharma is one of its deniable industrial fronts, and FROSTLINE is
the contractor that does the work no Ministry letterhead will admit to. FROSTLINE
did not break into this node; it built the finale implant, taught it to beacon, to
persist, and to silence the siren, staged the sabotage marker in a reserved
sector, and signed the image.

Against them is WHITEOUT, and the engineer who copied the first image,
NIGHTINGALE. This act is the last warning node on the Ministry's industrial edge.
TELESCREEN, the surveillance backbone that watches it, comes after the ten.

An adversarial, evidence-based audit of this act, including its honest
limitations, is in [NATION-STATE-REVIEW.md](NATION-STATE-REVIEW.md).


<br>

## How This Project Fits the Embedded Hacking Course

This repository is the Act X capstone integration for the
[Embedded Hacking](https://github.com/mytechnotalent/Embedded-Hacking) course. It
reuses the entire Act I peripheral set so one breadboard serves the whole
foundation, and it adds the concepts the finale builds toward: a coordinated
multi-stage beacon, boot persistence from a reserved sector, a sabotage marker
written with the real flash API, a hazard command path that fails safe, and the
blue-half controls that contain them.

Each earlier module teaches one peripheral or language concept in isolation; this
project wires several of them into a single, tested product, and then teaches you
to look at that product as an adversary sees it.

| Embedded Hacking module | Concept you learn | Where it lives here |
| ----------------------- | ----------------- | ------------------- |
| Week 1: Introduction, Ethics, Scoping | Authorized lab work | Every lab is self-contained and authorized by design |
| Week 3: RP2350 Architecture and Firmware Analysis | Bare-metal targets, ELF/UF2, SWD | Pico SDK build, `build/*.uf2`, Debug Probe flash via OpenOCD |
| Weeks 4-6: Variables, Integers/Floats, Static | Data types, GPIO | `src/monitor.c` state machine, LED on GP25 |
| Week 7: Constants with 1602 LCD I2C | I2C bus, HD44780 commands | `src/display.c` |
| Week 9: Operators with DHT11 | Bit operations, edge timing | `src/sensor.c` chemical store temperature sensor |
| Week 11: Structures and Functions | Modular design | `include/*.h` and `src/*.c` module boundaries |
| This project adds | Coordinated beacon, boot persistence, sabotage marker, hazard fail-safe, incident response, malware analysis, anti-debug evasion, strict testing | `src/implant.c`, `src/siren.c`, `src/control.c`, `src/chem_auth.c`, `src/radio.c`, `scripts/gateway.py`, `scripts/spoof.py`, `test/` |

If you have not worked through Weeks 7 and 9 yet, do those first: this project
assumes you are comfortable with I2C wiring and one-wire edge timing.

<br>

## Learning Objectives

By the end of this chapter and its labs you will be able to:

- Explain why a coordinated payload that runs a beacon, persistence, and a
  sabotage marker at once is a different failure class from any single technique,
  and why the finale is an incident-response problem rather than a patch.
- Wire and drive a 1602 LCD through a PCF8574 I2C backpack and render a hazard
  state, link, zone, temperature, and sabotage-marker readout.
- Decode a VS1838B infrared receiver as a local maintenance remote for WARN, ACK,
  and TEST commands, and explain why an unauthenticated optical surface is still
  an attack surface and must not silently bypass authorization.
- Drive an SG90 siren and vent actuator with 50 Hz PWM and explain why a 1000uF
  bulk capacitor is not optional.
- Read a DHT11 chemical store temperature sensor and classify the store against a
  safe band before the siren is allowed to sound.
- Design a sealed hazard command path over a sub-GHz LoRa link using a fixed-size
  envelope, a guarded command set, a bounded zone band, a monotonic anti-replay
  window, and a keyed state tag.
- Analyze a coordinated finale implant: locate the multi-stage beacon, read the
  sabotage marker `0x58`, read the magic command `IRON-CURTAIN-BEACON-2026`, find
  the reserved-sector address `0x103FF000`, and read the anti-debug trap.
- Explain why cutting the beacon, breaking the persistence, clearing the marker,
  and sealing the command path are four separate controls, and why a firmware
  reflash alone is not enough.
- Defeat an anti-debug check under GDB by understanding the CoreDebug `DHCSR`
  register at `0xE000EDF0`.
- Apply blue-half controls: sealed and authorized commands, an acknowledge that
  asks for authorization, fail safe to the raised hazard posture on a lost link,
  no persisted marker, and no silenced siren.
- Derive a key with Argon2id, seal every frame with XChaCha20-Poly1305, and read
  and run a native host test suite with hardware mocks and line coverage.

<br>

## Prerequisites

- The [Embedded Hacking](https://github.com/mytechnotalent/Embedded-Hacking)
  breadboard (`EHP2_bb.png`) and parts list.
- Acts I to IX are helpful but not required. See
  [cold-chain-monitor](https://github.com/mytechnotalent/cold-chain-monitor),
  [access-gate](https://github.com/mytechnotalent/access-gate),
  [pipeline-valve-controller](https://github.com/mytechnotalent/pipeline-valve-controller),
  [hvac-automation-node](https://github.com/mytechnotalent/hvac-automation-node),
  [industrial-tamper-system](https://github.com/mytechnotalent/industrial-tamper-system),
  [smart-logistics-dropbox](https://github.com/mytechnotalent/smart-logistics-dropbox),
  [factory-andon-station](https://github.com/mytechnotalent/factory-andon-station),
  [datacenter-vent-controller](https://github.com/mytechnotalent/datacenter-vent-controller),
  and [smart-parking-barrier](https://github.com/mytechnotalent/smart-parking-barrier)
  for the sensor, the door, the valve, the air, the web, the courier, the choir,
  the vault, and the fang. The pin map is identical, so one breadboard serves all
  ten.
- Comfort with C, the Linux/macOS shell, and basic electronics.
- A Pico 2, a Debug Probe (recommended, and required for the incident-response
  lab), a 1602 LCD with PCF8574 backpack, a DHT11, the full Embedded Hacking kit
  (3 LEDs, 3 resistors, a push button, an SG90 servo, a 1000uF capacitor, and a
  VS1838B infrared receiver plus NEC remote), two RYLR998 modules, and one
  USB-to-TTL serial adapter.
- Toolchain: Pico SDK 2.2.0+, `arm-none-eabi-gcc`, CMake, Ninja, Python 3, GDB
  (`arm-none-eabi-gdb`) for Lab 3, and (optionally) `typst` to rebuild the paper.

<br>

## Table of Contents

1. [Background](#background)
2. [System Architecture](#system-architecture)
3. [The Wire Protocol](#the-wire-protocol)
4. [The Cryptographic Envelope](#the-cryptographic-envelope)
5. [The FROSTLINE Coordinated Beacon](#the-frostline-coordinated-beacon)
6. [Hardware You Need](#hardware-you-need)
7. [Wiring the Node](#wiring-the-node)
8. [Build and Flash](#build-and-flash)
9. [Lab 1: Bring-Up and Verify](#lab-1-bring-up-and-verify)
10. [Lab 2: Inspect the Wire Protocol](#lab-2-inspect-the-wire-protocol)
11. [Lab 3: The Finale Track](#lab-3-the-finale-track)
12. [Lab 4: The Fix Track](#lab-4-the-fix-track)
13. [Troubleshooting](#troubleshooting)
14. [Testing Philosophy and Coverage](#testing-philosophy-and-coverage)
15. [Generating Packet Artifacts](#generating-packet-artifacts)
16. [Code Standards](#code-standards)
17. [Project Layout](#project-layout)
18. [Glossary](#glossary)
19. [Further Reading](#further-reading)
20. [License](#license)

<br>

## Background

### Why chemical storage warning terminals

A warning terminal is a control loop with a siren in it. A store temperature
sensor reports the enclosure, a safety gateway authorizes a hazard, clear, or
acknowledge command, a terminal decides, a siren sounds, and a tower light tells
the responders whether the store can be entered. The siren is where the decision
becomes physical, and the tower light is where the operator reads it. Everything
interesting in chemical safety security happens in those two places.

Three properties have to hold at once, and they are not the same property:

- **Integrity.** The hazard command that reaches the siren is the one the safety
  gateway authorized. Not a replay, not a forgery, not a stray package.
- **Authority.** The node acts only on an authorized verdict. A local acknowledge
  button or maintenance remote is a request, not an authorization.
- **Safety.** The siren sounds for a hazard and stays silent only when the store
  is genuinely clear, and a local condition can never force a false all clear.

Act X adds a fourth property that is the hardest of all because it turns the
warning against the world: **coordinated availability of the warning itself**. A
terminal that never lies and never fails authentication can still be the last
node to lie, because the attacker's goal is not to make it wrong; it is to make it
quiet.

### Why integrity plus authority plus safety matter

The classic naive terminal collapses the three. It accepts any hazard command on
the radio, it has no anti-replay window, and it lets a local input bypass the
decision. Act II showed what that costs a door. Act III showed the industrial
version. Act IV showed the persistence version. Act V showed the propagation
version. Act VI showed the exfiltration version. Act VII showed the command
version. Act VIII showed the availability version. Act IX showed the physical
weaponization version. Act X adds the coordinated finale:

- **Integrity without safety.** The sealed hazard path in this build is correct.
  XChaCha20-Poly1305 authenticates every frame, the zone band is bounded, the
  sequence window rejects a replay, and the state tag detects a tampered verdict.
  None of that stops a sabotage marker that forces a false all clear and silences
  the siren.
- **Authority as the attack goal.** A forged or replayed packet aims to silence a
  store the operator did not authorize. The window and the tag are the controls
  that stop it.
- **Safety as the last line of defense.** The temperature interlock is what stands
  between an authorized clear command and a hazard. A local condition that masks
  it is a warning-integrity failure, not a protocol failure.
- **Coordination as the invisible failure.** A payload that runs a beacon, a
  persistence mechanism, and a sabotage marker together has no single visible
  symptom except the one it is allowed to show. It does not need the wire, the
  key, or the hazard command. It needs a reason to lie, and a lie that wears the
  uniform of routine testing is the hardest kind to see: the packets are well
  formed and the lamp says clear.

The fix track in Lab 4 seals the hazard command path, makes the acknowledge ask
for authorization, and makes the terminal fail to the safe hazard state on a lost
link. The finale track in Lab 3 cuts the beacon, breaks the persistence, clears
the sabotage marker, and removes the passenger that was never in the design.

### Why ChaCha20 over AES on the RP2350

The RP2350 has no hardware AES engine; its accelerated crypto block covers
SHA-256, not AES. A software AES implementation on this part is therefore both
slower and riskier, because table-driven AES performs data-dependent memory
accesses that create a cache-timing side channel. ChaCha20 is built only from
addition, rotation, and XOR, with no data-dependent table lookups, so it is fast
in portable C and has no comparable cache-timing surface. XChaCha20-Poly1305 is
thus both the modern choice and the pragmatic one for this silicon. The full
rationale, including the extended-nonce benefit, appears in
[The Cryptographic Envelope](#the-cryptographic-envelope).

### Why a coordinated-incident-response lesson

The first nine acts each taught one way a device fails by doing something: a bad
reading, a bad decision, a bad image, a bad cleanup, a bad neighbor, a bad leak,
a bad listener, a bad lock, a bad swing. Act X teaches the failure where every one
of those techniques is combined into a single payload and answered by a
procedure. Warning integrity is the property that every other control silently
assumes. The gateway can be authenticated, the replay window can be airtight, and
the state tag can be perfect, and people can still be hurt because the one device
that exists to warn chooses to lie. The defense is therefore an incident-response
policy and a build control: cut the beacon, break the persistence, clear the
marker, seal the command path, and fail safe.

### The two on-wire problems this project solves

1. **Payloads that contain commas.** The sealed body is carried as lowercase hex,
   but the `+RCV` framing still separates fields with commas. A naive receiver
   that splits the line on the first comma corrupts the frame. The correct
   discipline is the **declared-length** rule: slice exactly `L` characters after
   the second comma and require the next character to be a comma.
2. **Telling a real hazard command from a forged or replayed one.** The
   controller records the sender address exactly as the radio reports it, and it
   trusts the bytes that arrive. The sealed envelope, the bounded zone band, and
   the stateful window are what close that gap.

### Inter-Integrated Circuit (I2C)

I2C is a two-wire bus: **SDA** (data) and **SCL** (clock), each pulled up to the
supply rail. A controller (the Pico) addresses a target by its 7-bit address and
writes or reads bytes. The 1602 LCD backpack carries a **PCF8574** I/O expander
at address `0x27`; the firmware bit-bangs the HD44780 nibble protocol over that
expander. Pull-ups are mandatory: the firmware enables the internal ones and the
backpack usually adds its own.

### The DHT11 one-wire protocol

The DHT11 is a low-cost digital temperature and humidity sensor. In Act X it is
the **chemical store temperature sensor**: the node classifies the store against a
safe band and announces the temperature in the hazard readout. It speaks a custom
single-wire protocol:

1. The host pulls the line low for at least 18 ms (the **start pulse**), then
   releases it and enables its pull-up.
2. The sensor answers with an 80 us low, then an 80 us high handshake.
3. The sensor sends **40 bits**. Each bit begins with a 50 us low, then a high
   pulse whose width encodes the value: about 26-28 us for a `0`, about 70 us
   for a `1`.
4. Five bytes follow: humidity integer, humidity decimal, temperature integer,
   temperature decimal, and a checksum equal to the low byte of their sum.

Reading it means timing edges on the order of tens of microseconds, so the
firmware uses an 18 ms host pulse, a 50 us bit-classification threshold, and a
240 us per-edge timeout so a dead or unplugged sensor fails fast instead of
hanging the loop. A reading that fails its checksum is never safe, and a valid
reading outside **0.0 C to 40.0 C** (the tenths band `0` to `400`) is out of
band. Either way, the store is not nominal.

### Universal Asynchronous Receiver/Transmitter (UART) and AT commands

The RYLR998 is driven over a UART at 115200 baud using CRLF-terminated ASCII
commands. The firmware writes `AT+SEND=...` and drains inbound `+RCV=...` lines.
Because the radio is a separate processor, its configuration (address, network
identifier, band) persists until changed; the controller and the gateway each
provision their own radio at start-up so they agree before any command traffic
flows.

### Cyclic Redundancy Check (CRC)

`src/crc.c` implements CRC-16/CCITT-FALSE (`poly = 0x1021`, `init = 0xFFFF`,
check value `0x29B1` for `"123456789"`). It is provided as a reusable integrity
diagnostic and exercised by the test suite. It is **not** part of the LoRa frame
in this project; the lesson is the *absence* of authentication, not the absence
of a checksum.

<br>

## System Architecture

There are four roles:

| Role | Runs on | Job |
| ---- | ------- | --- |
| **Warning terminal node** | Pico 2 firmware | Decodes the infrared maintenance remote, verifies sealed gateway hazard, clear, and acknowledge commands, annunciates the tower light, reads the store temperature, drives the siren and vent actuator, enforces the manual acknowledge request, renders the hazard readout, and (SANDBOX_ONLY) runs the coordinated beacon |
| **Safety control gateway** | laptop + USB-TTL radio | Authenticates every request, logs it to `chem_log.csv`, decides authorization, and answers with a sealed hazard command carrying a sequence and a state tag (`scripts/gateway.py`) |
| **Edge simulator** | laptop + USB-TTL radio | Pretends to be a terminal and sends sealed zone requests (`scripts/sim_edge.py`) |
| **Attacker** | laptop + USB-TTL radio | Impersonates the gateway, forges a command, or replays a captured command (`scripts/spoof.py`) |

### Data flow

```text
+----------------------+                              +----------------------+
| Pico 2 warning node  |        LoRa (sub-GHz)        | Safety control GW    |
| IR remote  -> GP5    |  AT+SEND=0001,<len>,<hex>    |  USB-TTL radio       |
| DHT11      -> GP4    |----------------------------->|  scripts/gateway.py  |
| Servo      -> GP14   |<-----------------------------|  chem_log.csv        |
| LCD     -> GP2/GP3   |  AT+SEND=<node>,<len>,<hex>  |  sealed command      |
+----------------------+                              +----------------------+

+----------------------+                              +----------------------+
|   Attacker laptop    |  forged or replayed command  | (same warning node)  |
|   scripts/spoof.py   |----------------------------->|  rejects at the tag  |
|  claims the gateway  |                              |  tag or seq window   |
+----------------------+                              +----------------------+

+----------------------+                              +----------------------+
|  Finale implant      |      silences the siren      | (SANDBOX_ONLY node)  |
|  compile-time guard  |----------------------------->|  forces all clear    |
|  no radio, no key    |                              |  writes 0x58 marker  |
+----------------------+                              +----------------------+
```

### Firmware module map

| File | Responsibility |
| ---- | -------------- |
| `src/main.c` | Entry point: `stdio_init_all`, `monitor_init`, tick loop |
| `src/monitor.c` | State machine: I2C bus scan, maintenance remote, gateway command, siren motion, manual acknowledge request, store temperature sensor, hazard render |
| `src/implant.c` | SANDBOX_ONLY FROSTLINE coordinated beacon: multi-stage check-in, reserved-sector `0x58` sabotage marker, boot re-install, and CoreDebug anti-debug |
| `src/siren.c` | Siren state machine: bounded travel, lowered/raised/fault/moving, fail safe |
| `src/control.c` | Sealed hazard command path: open, authorize, guarded command and bounded zone |
| `src/chem_auth.c` | Authorization record, monotonic anti-replay window, authenticated state tag |
| `src/sensor.c` | DHT11 one-wire sampling and store-temperature-band classifier |
| `src/display.c` | HD44780 driver over the PCF8574 backpack and hazard status rendering |
| `src/radio.c` | RYLR998 provisioning, `AT+SEND` builder, `+RCV` parser, line pump |
| `src/status_led.c` | Red/yellow/green HAZARD / WATCH / CLEAR annunciator light |
| `src/button.c` | Debounced manual acknowledge button around the internal pull-up |
| `src/servo.c` | 50 Hz PWM siren and vent actuator |
| `src/ir_remote.c` | VS1838B edge timing and NEC maintenance remote decode |
| `src/chacha20.c` | ChaCha20 stream cipher and HChaCha20 subkey derivation |
| `src/poly1305.c` | Poly1305 one-time message authenticator |
| `src/crypto_aead.c` | XChaCha20-Poly1305 seal/open envelope |
| `src/blake2b.c` | BLAKE2b and the Argon2 variable-length hash H' |
| `src/argon2.c` | Argon2id core (BLAMKA, hybrid addressing) |
| `src/crypto_kdf.c` | Argon2id passphrase key derivation |
| `src/envelope.c` | Hex nonce/ciphertext/tag envelope codec |
| `src/crc.c` | CRC-16/CCITT-FALSE diagnostic |
| `include/chem.h` | Pin map, bus, provisioning, hazard addresses |
| `include/implant.h` | Beacon magic command, marker, tick interval, anti-debug interface |
| `include/control.h`, `include/chem_auth.h` | Sealed command and authorization interfaces |

<br>

## The Wire Protocol

### Request frame

The local maintenance remote, or the edge simulator, seals a two-byte zone into
an authenticated envelope and sends it to the safety control gateway:

```text
AT+SEND=0001,<len>,<hex envelope>
```

The plaintext of a request is exactly two bytes: an `int16` storage zone
identifier in little-endian.

### Command frame

The gateway answers an authenticated request with a sealed hazard command. The
command plaintext is a 23-byte body:

```text
seq[4] (little-endian) || command[1] || zone[2] (little-endian) || tag[16]
```

- `seq` is the monotonic gateway sequence number.
- `command` is one of the guarded hazard commands: `CHEM_COMMAND_HAZARD`
  (`0x01`), `CHEM_COMMAND_CLEAR` (`0x02`), or `CHEM_COMMAND_ACK` (`0x03`). Any
  other command byte is refused.
- `zone` is the authorized storage zone in the provisioning band `CHEM_ZONE_MIN`
  (`0`) to `CHEM_ZONE_MAX` (`16`).
- `tag` is an XChaCha20-Poly1305 tag over the authorization record the command
  would produce, so the controller can verify that the verdict it is about to
  store is the one the gateway authorized.

The gateway sends it back to the claimed sender address:

```text
AT+SEND=<node>,<len>,<hex envelope>
```

The firmware enforces the guard in `control_parse`: the recovered command byte
must be in the guarded hazard set, and the recovered zone must be inside the
provisioning band. Anything else is rejected before it can reach the siren
decision. This is the sealed replacement for the old unauthenticated hazard
injection.

### Sealed envelope layout

Every payload on the wire is the lowercase hexadecimal encoding of:

```text
nonce[24] || ciphertext[L] || tag[16]
```

For a two-byte request body this is 24 + 2 + 16 = 42 bytes, or 84 hex
characters. For a 23-byte command body this is 24 + 23 + 16 = 63 bytes, or 126
hex characters. The declared length `L` in the `AT+SEND` and `+RCV` framing is
the length of the hex string, not of the underlying plaintext.

The maximum accepted plaintext is 48 bytes (`ENVELOPE_MAX_PLAINTEXT`), and the
maximum hex envelope buffer is `(24 + 48 + 16) * 2 + 1 = 177` bytes
(`ENVELOPE_MAX_HEX_LEN`), which fits the 256-byte radio command and receive
buffers with framing headroom.

### Declared-length slicing invariant

Given the substring `T` after the second comma:

```text
C = T[0 : L]   and   T[L] == ","
```

The receiver checks `T[L] == ","`, so a mismatch between the declared length and
the actual payload is a parse error rather than silent corruption. This is what
makes hex-bearing payloads safe to carry and is the same invariant Act I uses.

### Hazard status readout

```text
ST:CLEAR L:UP
Z:4 T:235 M:--
```

Line 1 is the current hazard state (`CLEAR`, `WATCH`, `HAZRD`, or `FAIL`) and the
gateway link (`UP` or `--`). Line 2 is the active storage zone, the store
temperature in tenths of a degree Celsius, and the sabotage status. In the clean
build the sabotage field is always `--`. In the `SANDBOX_ONLY` build the sabotage
field is `SAB` once the reserved-sector marker is present, and while the marker is
present the state is rendered as `SAFE` and the siren is silenced. When the store
is in hazard or the terminal has failed safe, the red lamp is lit; when the store
is under watch or a manual acknowledge awaits authorization, the yellow lamp is
lit; when the store is clear and the marker is absent, the green lamp is lit.
Exactly one tower light lamp is lit at a time.

### Radio provisioning

For the link to work, both radios must share the same **network identifier** and
each must have the address the other targets:

- Firmware sets its own radio: `AT+ADDRESS=7`, `AT+NETWORKID=18`.
- `gateway.py` sets the gateway radio: `AT+ADDRESS=1`, `AT+NETWORKID=18`.

Both radios must also be the **same band variant** (for example 915 MHz or
868 MHz); band and RF parameters are left at factory defaults, so use matching
modules.

### Timing

| Quantity | Value |
| -------- | ----- |
| Gateway link timeout (`CHEM_LINK_WAIT_MS`) | 5000 ms |
| Siren travel time (`CHEM_SIREN_TRAVEL_MS`) | 1000 ms |
| Acknowledge debounce (`CHEM_ACK_DEBOUNCE_US`) | 30000 us |
| DHT11 host start pulse | 18000 us |
| DHT11 bit threshold | 50 us |
| DHT11 per-edge timeout | 240 us |
| LCD I2C clock | 100000 Hz |
| Radio UART baud | 115200 |
| Store temperature band | 0 to 400 tenths (0.0 C to 40.0 C) |
| Storage zone band | 0 to 16 |
| Fail-safe zone | 0 |
| Siren lowered pulse | 500 us |
| Siren raised pulse | 1500 us |
| Servo PWM period | 20000 us (50 Hz) |
| Beacon re-assert interval | 4 ticks |
| Beacon check-in stages | 3 |
| Beacon magic command | 24 bytes |

<br>

## The Cryptographic Envelope

The radio is the first open path, and it is one a key can close. The fix is
authenticated encryption: every request and every command is sealed so a forged
frame dies at the authentication tag instead of moving the siren. The full
implementation lives in `src/chacha20.c`, `src/poly1305.c`, and
`src/crypto_aead.c`, and every primitive is checked against its published test
vectors in the native suite.

### Why XChaCha20-Poly1305

- **256-bit key, 192-bit nonce.** The extended nonce means nonces can be drawn at
  random forever, so the controller never needs a shared counter that a reboot
  could reuse.
- **AEAD in one pass.** Confidentiality and integrity come from one operation;
  the associated data (the warning node id, byte `0x07`) is authenticated even
  though it is not encrypted.
- **Constant-time software.** ChaCha20 has no data-dependent table lookups, so it
  has no cache-timing surface. The RP2350 has no hardware AES engine (it
  accelerates SHA-256 only), which makes software AES both slower and riskier on
  this silicon.
- **128-bit Poly1305 tag.** Guessing a valid tag succeeds with probability
  2^-128.

### Why Argon2id

A passphrase is not a key. Argon2id (RFC 9106) is the memory-hard password hash:
it mixes the passphrase with a salt across memory and time so an attacker cannot
cheaply recover the field passphrase from a captured image. The classroom profile
is `t=3`, `p=1`, `m=64` blocks (`CRYPTO_KDF_TIME_COST`,
`CRYPTO_KDF_PARALLELISM`, `CRYPTO_KDF_MEMORY_BLOCKS`) to fit the RP2350 SRAM
budget. Raise it on the safety gateway. The lab salt is the 16 ASCII bytes
`coldiron-salt-01`.

### Key model: one field key

Act X uses a single field key derived with Argon2id from a committed lab
passphrase and salt. It seals every frame on the wire and it computes the state
tag over the authorization record. In the classroom build the firmware and the
gateway derive the same key, so they interoperate with no provisioning step. That
is a lab convenience, not a deployment.

The design keeps the key roles separable so students can reason about the real
lifecycle: derive, provision per device, use, rotate on a schedule, and retire. A
production build provisions key material from one-time-programmable (OTP) memory,
keeps the state-tag key off the field device where possible, and rotates without
reflashing every controller.

### Envelope layout

The sealed frame is carried as hex inside the `AT+SEND` payload:

```text
nonce[24] || ciphertext[L] || tag[16]
```

The receiver recomputes the Poly1305 tag over the associated data and ciphertext,
compares it in constant time, and only then decrypts. This envelope is wired end
to end: `src/control.c` opens the command with `src/envelope.c`, and the gateway
authenticates before it parses or acts. Authenticated frames carry the warning
node id as associated data, so a frame sealed for one node cannot be relabeled for
another.

### Anti-replay and authenticated state

Strong AEAD is necessary and not sufficient. Two stateful controls sit on top:

- **Anti-replay sequence window.** `src/chem_auth.c` keeps `last_seq`, the
  highest sequence number ever accepted. `chem_auth_apply` accepts a command
  only when its sequence is strictly greater than `last_seq`. A captured command,
  even a perfectly valid one, is rejected on second use.
- **Authenticated state tag.** The authorization record is nine bytes:
  `granted[1]`, `seq[4]`, `last_seq[4]`. The tag is an XChaCha20-Poly1305 tag
  over that record, computed under the field key with a deterministic nonce built
  from the sequence number and the domain byte `0xA7`. `chem_auth_state_ok`
  recomputes the tag and compares it in constant time before the siren is allowed
  to move. A debugger that sets `granted = true` without recomputing the tag
  fails here first.

The sequence window and the state tag are independent. The window stops a valid
command from working twice; the tag stops an unauthorized verdict from existing
at all. Neither one, by itself, disarms the finale implant.

<br>

## The FROSTLINE Coordinated Beacon

Act X carries the coordinated-finale lesson, and the beacon is the reason. It is
real in technique and inert in effect: it runs on your breadboard, it runs a
multi-stage check-in, it re-installs from the reserved sector, and it writes a
sabotage marker into a reserved flash sector that holds nothing else. It is
compiled only when `SANDBOX_ONLY` is defined, so the clean firmware image contains
no implant at all. The test suite and the companion CTF build with `SANDBOX_ONLY`
and with the host mock, so every implant path is exercised natively.

What the beacon does, in the order the code does it:

1. **First run and reserved sector.** `implant_init` reads the marker byte at
   `CHEM_IMPLANT_RESERVE_ADDR` (`0x103FF000`), the final sector of external
   flash. On the first run the marker is absent, so `implant_infect` erases the
   sector and programs `0x58` (`CHEM_IMPLANT_SABOTAGE_MARKER`) with the real
   Pico SDK flash API, `flash_range_erase` and `flash_range_program`. On every
   later boot the marker is present, so the beacon re-arms and records that it
   re-installed from the reserved sector. A firmware reflash that writes the
   program region does not touch the reserved sector, so the beacon comes back
   even when the code is gone.
2. **The coordinated condition.** `implant_beaconize` arms the beacon only when
   the candidate token matches `CHEM_IMPLANT_BEACON_MAGIC`
   (`IRON-CURTAIN-BEACON-2026`) at exactly `CHEM_IMPLANT_BEACON_MAGIC_LEN` (24)
   bytes. A wrong token, a null pointer, or an attached debug probe leaves the
   terminal disarmed. On a successful arm the marker is persisted, so the beacon
   re-installs on the next boot.
3. **The multi-stage check-in.** `implant_tick` advances a monotonic counter.
   While the beacon is resident, check-in is due, and no probe is attached, every
   `CHEM_IMPLANT_BEACON_INTERVAL` (4) ticks the beacon advances one stage and
   re-writes the marker. A full cycle is `CHEM_IMPLANT_BEACON_STAGES` (3) stages,
   and the completed cycles are counted. A device that beacons once and then
   drifts would not hold a campaign; the re-assertion is what makes it
   coordinated.
4. **The sabotage marker.** While `implant_beacon_armed()` is true and
   `implant_marker_set()` is true, `monitor_sabotage` returns true. The monitor
   then forces the effective hazard state to `CLEAR`, suppresses the siren, lights
   the green CLEAR lamp, renders the state as `SAFE`, and renders the sabotage
   field as `SAB`. The store can be in a declared hazard and the panel will still
   say all clear. The terminal lies.
5. **The release condition.** `implant_disable` disarms only when the candidate
   token matches `IRON-CURTAIN-BEACON-2026` at exactly 24 bytes, as checked by
   `implant_token_ok`. A wrong token, a null pointer, or an attached debug probe
   leaves the beacon armed. On a successful release the beacon stands down and the
   marker is cleared so the beacon is not re-armed on the next boot.
6. **Anti-debug.** Every tick, and every beacon operation, the beacon reads the
   CoreDebug `DHCSR` register at `0xE000EDF0`
   (`CHEM_IMPLANT_DHCSR_ADDR`). Bit 0 is `C_DEBUGEN` and bit 1 is `C_HALT`. If
   either bit is set, the beacon is suppressed and the marker is not written, so
   the payload behaves like a well-mannered firmware module while a probe is
   attached. It goes back to work the moment the probe is gone.
7. **Neutralization.** The beacon exposes `implant_neutralize` to stand down and
   clear the marker. The documented fix is not one step: cut the coordinated
   beacon, break the persistence, clear the sabotage marker, and remove the code
   path and the `SANDBOX_ONLY` build flag, then add a fail-safe policy so a lost
   link raises the hazard siren.

The beacon is bounded by construction and by test. It touches only its own
outputs, its runtime flags, and the one reserved sector. It never opens a sealed
envelope, never reads the field key, and never contacts an external address.
There is no network, no filesystem, and no host impact.
`test_implant_init_first_run`, `test_implant_reinstall_on_boot`,
`test_implant_marker`, `test_implant_debug_attached`, `test_implant_init_debug`,
`test_implant_beaconize_debug`, `test_implant_tick_advance`,
`test_implant_tick_debug`, `test_implant_tick_unarmed`,
`test_implant_disable_accepts`, `test_implant_disable_rejects`,
`test_implant_disable_debug`, `test_implant_neutralize`,
`test_monitor_sabotage_lies`, and `test_monitor_sabotage_restores` assert exactly
that behavior.

The honest limit is the point of the lab. A sanitized educational payload is
still a benign educational payload: it demonstrates the technique, not the
tradecraft. It is confined to the breadboard, guarded by `SANDBOX_ONLY`, the
effect is a mock siren and a mock LCD, and it holds no real hazard. There is no
external network and no remote address. The real lesson is that warning integrity
is a policy control, and the defense is not a patch to the beacon but the closure
of the beacon, the erasure of the reserved sector, the removal of the code path
and the build flag, and a fail-safe posture that assumes the worst.

<br>

## Hardware You Need

Full parts list with links: [PARTS.md](PARTS.md).

| Qty | Part | Notes |
| --- | ---- | ----- |
| 1 | Raspberry Pi Pico 2 (RP2350) with headers | The warning terminal controller |
| 1 | Raspberry Pi Debug Probe | SWD flashing, UART0 console, and the Lab 3 incident-response work (recommended, effectively required) |
| 1 | Full-size breadboard | |
| 1 | Assorted jumper wires | |
| 1 | 1602 LCD with PCF8574 I2C backpack | Hazard state, zone, temperature, and sabotage readout, address `0x27` |
| 1 | DHT11 temperature/humidity sensor | Chemical store temperature sensor |
| 1 | 10K resistor | Only if your DHT11 has no onboard pull-up |
| 3 | 5mm LEDs (red, yellow, green) | HAZARD, WATCH, CLEAR annunciator light |
| 3 | 100, 220, or 330 Ohm resistors | One per LED |
| 1 | Push button (tactile switch) | Manual acknowledge request, active low |
| 1 | SG90 servo motor | The siren and vent actuator |
| 1 | 1000uF 25V capacitor | Bulk decoupling on the servo 5V rail |
| 1 | VS1838B infrared receiver | Maintenance remote input |
| 1 | NEC-compatible infrared remote | Local WARN, ACK, and TEST commands |
| 3 | RYLR998 LoRa modules with antennas | 2 for the command loop, 3 for the live attack lab |
| 2 | USB-to-TTL serial adapters (FTDI FT232, CP2102, or CH340), 3.3V logic | 1 for the gateway, 1 for the attacker in the live lab |
| 4 | USB cables | Pico 2, Debug Probe, and serial adapter(s) |

### How many radios do you actually need?

| Goal | Radios | What is connected |
| ---- | ------ | ----------------- |
| Legitimate sealed hazard loop (Labs 1-2) | **2** | 1x RYLR998 on the Pico (UART1) + 1x RYLR998 on a USB-to-TTL adapter (the gateway) |
| Live attack lab (Labs 3-4, watch a forged command land and fail) | **3** | the 2 above + 1x RYLR998 on a second USB-to-TTL adapter (the attacker) |
| Finale demonstration with no extra hardware | 2 or 0 | watch the firmware silence the siren and force the all clear, or run the native unit tests |
| Attack concept with no extra hardware | 2 or 0 | read-and-run the offline parser demo, or the unit tests |

A radio never receives its own transmission, and the gateway radio is busy
listening as `gateway.py`, so the live attack needs a separate attacker radio.
The 2-radio kit runs the whole legitimate system; only the live attack
observation needs the third. The finale lab is fully observable in the firmware
output path and in the native tests, because a single node silences its own siren
and forces its own all clear.

> Serial adapter warning: the RYLR998 is **not** 5V tolerant. Use a
> **3.3V-logic** USB-to-TTL adapter (or set its jumper to 3.3V).

### How each part works

Every part in the bill of materials, the principle behind it, and what it does
in this act.

| Part | How it works | Role in this act |
| ---- | ------------ | ---------------- |
| 1x Full-size breadboard (long) | Spring-clip rows tie five holes into one electrical node, and the two full-length rails distribute 3V3 and GND. | Mounts the Pico 2, LCD, DHT11, LEDs, button, and LoRa module and carries the shared power and ground for the warning terminal node. |
| 1x Assorted jumper wires (male-to-male, male-to-female, female-to-female) | Male pins seat in breadboard rows or female header sockets, female sockets grip male header pins, and each gender extends one node without soldering. | Routes power, ground, I2C, UART, PWM, and GPIO between the Pico 2 and every warning terminal peripheral, including the LCD backpack and servo. |
| 1x Raspberry Pi Pico 2 with header | The RP2350 packs dual Cortex-M33 cores at up to 150 MHz with 3.3V logic, GPIO, ADC, I2C, UART, PWM, and an onboard GP25 LED. | Runs the warning firmware, reads the button and DHT11, drives the LCD, servo, and LEDs, and carries the LoRa safety link. |
| 1x Raspberry Pi Pico Debug Probe | SWD on SWCLK and SWDIO flashes, halts, and single-steps the RP2350, while a separate UART bridge exposes the serial console. | Flashes the warning firmware and provides the console and debug view used in the incident-response work. |
| 2x USB A-male to USB micro-B cables | Each cable carries 5V power and USB data over a micro-B plug. | One powers and consoles the Pico 2, and one powers and consoles the Debug Probe during warning terminal bring-up. |
| 3x 5mm LEDs (1 red, 1 green, 1 yellow) | An LED conducts once its forward voltage is exceeded, anode positive to cathode, and a GPIO pin sources current through it and a series resistor. | Shows the hazard states as the red HAZARD, yellow WATCH, and green CLEAR annunciator light. |
| 3x 100, 220, or 330 Ohm resistors | Each resistor drops the surplus voltage and limits LED current to a safe few milliamps. | Protects one LED each and sets the brightness of the hazard annunciator. |
| 1x Push button (tactile switch) | Pressing it shorts the GPIO pin to ground while an internal pull-up holds the pin high, so the press reads active low. | Gives the warning terminal its local acknowledge request input. |
| 1x 1602 LCD with PCF8574 I2C backpack | The HD44780 controller drives the 16x2 character cells, and the PCF8574 expander turns I2C bytes into the controller's 4-bit nibble protocol. | Displays the hazard state, zone, temperature, and sabotage readout at I2C address 0x27. |
| 1x DHT11 temperature and humidity sensor | The host pulls the one-wire data line low as a start pulse, then the sensor answers with 40 bits of humidity, temperature, and a checksum. | Reports the chemical store temperature to the warning node. |
| 1x SG90 servo motor | A 50 Hz PWM signal sets the shaft angle by the width of its 1 to 2 ms pulse, with 1.5 ms near center. | Actuates the siren and vent in the warning terminal mechanism. |
| 1x 1000uF 25V capacitor | The capacitor is a bulk reservoir that supplies the servo inrush current and smooths the 5V rail. | Keeps the siren and vent actuator from browning out the Pico 2 when it moves. |
| 1x Infrared receiver (VS1838B) | Its photodiode and 38 kHz band-pass demodulator turn a modulated IR burst into an active-low logic pulse at the GPIO pin. | Receives the local maintenance remote commands for the warning node. |
| 1x Infrared remote controller (NEC-compatible) | Each key sends a NEC frame built from a 9 ms leader and 32 bits of address and command plus their complements. | Sends the local WARN, ACK, and TEST commands to the warning terminal. |
| 1x RYLR998 LoRa radio module | A UART AT command interface configures the module, which carries sealed frames over a sub-GHz LoRa link, and the module runs at 3.3V and is not 5V tolerant. | Links the warning node to the gateway and attacker radios for the sealed hazard loop and the live attack lab. |

<br>

## Wiring the Node

### Pin map

This is the authoritative map; it is identical to Acts I to IX and is defined in
`include/chem.h` and enforced by the test suite.

| Peripheral | Signal | Pico 2 GPIO |
| ---------- | ------ | ----------- |
| DHT11 chemical store temperature sensor | DATA (one-wire) | **GP4** |
| 1602 LCD (PCF8574) | SDA (I2C1) | **GP2** |
| 1602 LCD (PCF8574) | SCL (I2C1) | **GP3** |
| RYLR998 | RX <- Pico TX (UART1) | **GP8** |
| RYLR998 | TX -> Pico RX (UART1) | **GP9** |
| Infrared maintenance remote | OUT (VS1838B) | **GP5** |
| Siren and vent actuator servo | PWM signal | **GP14** |
| Red HAZARD LED | anode | **GP16** |
| Yellow WATCH LED | anode | **GP17** |
| Green CLEAR LED | anode | **GP18** |
| Manual acknowledge button | to ground | **GP15** |
| Onboard LED | heartbeat | GP25 |
| Debug Probe / UART0 console | TX | GP0 |
| Debug Probe / UART0 console | RX | GP1 |

> Note: GPIO 2/3 are the classic I2C1 pins used throughout the Embedded Hacking
> breadboard; this project's map matches that board because it is the same board.

### 1602 LCD with I2C backpack

| LCD backpack | Pico 2 |
| ------------ | ------ |
| VCC | 3.3V |
| GND | GND |
| SDA | GP2 |
| SCL | GP3 |

### DHT11 chemical store temperature sensor

| DHT11 | Pico 2 |
| ----- | ------ |
| VCC | 3.3V |
| DATA | GP4 |
| GND | GND |

If your DHT11 has no onboard pull-up, add a **10K resistor between DATA and
3.3V**. The firmware also enables the internal pull-up, but the external resistor
makes reads far more reliable over jumper wires. The store is not nominal when the
sensor fails or reads outside `0.0 C` to `40.0 C`.

### Annunciator LEDs

| LED | Pico 2 | Series resistor |
| --- | ------ | --------------- |
| Red (HAZARD) | GP16 (anode) | 220-330 Ohm to GND |
| Yellow (WATCH) | GP17 (anode) | 220-330 Ohm to GND |
| Green (CLEAR) | GP18 (anode) | 220-330 Ohm to GND |

Exactly one lamp is lit at a time. Red is a declared hazard or a failed-safe
terminal, yellow is a warning under watch or a manual acknowledge awaiting
authorization, and green is a clear store.

**LED behavior**

The annunciator drives the three lamps from a single state, so at most one lamp is
lit at a time and exactly one is lit whenever a state is active; `CHEM_LED_OFF` is
the only state that lights none. `status_led_show` writes the GPIOs directly, so
every lit lamp is solid and the clean firmware has no blinking lamp.

| Annunciator state | Lamp | Behavior | Meaning |
| ----------------- | ---- | -------- | ------- |
| `CHEM_LED_OFF` | none | off | All annunciator lamps dark (not selected by the running state machine). |
| `CHEM_HAZARD` | red | solid | A chemical release hazard is declared, a command was rejected, or the terminal failed safe. |
| `CHEM_WATCH` | yellow | solid | The store is under watch or a manual acknowledge is pending authorization. |
| `CHEM_CLEAR` | green | solid | The store is clear; in the `SANDBOX_ONLY` build the sabotage override forces this lamp even during a declared hazard. |

The onboard GP25 LED is initialized as an output and driven low at boot, then
pulses once on every monitor tick as the onboard heartbeat. There is no transmit
blink.

### Manual acknowledge button

| Button | Pico 2 |
| ------ | ------ |
| Leg 1 | GP15 |
| Leg 2 | GND |

The firmware enables the internal pull-up, so **do not** connect 3.3V to the
button. The manual acknowledge is a local request, not an authorization: a press
raises the WATCH indication and never changes the guarded hazard state on its own.
Lab 4 explains why the request must ask for authorization instead of silently
bypassing it.

### SG90 siren and vent servo

| Servo | Pico 2 |
| ----- | ------ |
| Signal (orange) | GP14 |
| VCC (red) | 5V (VBUS) |
| GND (brown) | GND |

Solder the **1000uF capacitor** across the servo 5V and GND rails to absorb the
inrush current; without it the RP2350 can brown out when the siren moves. Lowered
(siren silent, store vented) is 0 degrees and raised (siren sounding, the safe
hazard posture) is 90 degrees.

### Infrared receiver

| VS1838B | Pico 2 |
| ------- | ------ |
| OUT | GP5 |
| VCC | 3.3V |
| GND | GND |

Point any NEC-compatible remote at the receiver. In Act X this is the **local
maintenance remote**, not a convenience extra: the firmware decodes
`CHEM_IR_WARN` (`0x47`), `CHEM_IR_ACK` (`0x46`), and `CHEM_IR_TEST` (`0x45`).
There is no challenge and no secret on the optical surface, which is why a manual
acknowledge is treated as a request and not as an authorization.

**Using the remote**

Point the NEC remote at the VS1838B receiver on GP5 and press the mapped button.
The receiver idles high and pulls low on a mark, and the firmware times the NEC
frame to decode the command.

| NEC command | Code | Action |
| ----------- | ---- | ------ |
| `CHEM_IR_WARN` | `0x47` | Raises the WATCH indication by setting the acknowledge request pending. It does not change the guarded hazard state and does not sound the siren. |
| `CHEM_IR_ACK` | `0x46` | Raises the WATCH indication as well. In `monitor_apply_ir_command` the firmware handles ACK exactly as it handles WARN, and it does not move the siren. |
| `CHEM_IR_TEST` | `0x45` | No state change. The firmware logs `IR TEST (0x45)` and returns, so in this firmware TEST is a maintenance marker rather than a lamp test. |

### RYLR998 LoRa radio

> The RYLR998 must be powered. Forgetting **VDD** is the single most common
> reason the link appears dead: the firmware prints while the radio sits silent.

| RYLR998 | Pico 2 |
| ------- | ------ |
| VDD | 3.3V |
| GND | GND |
| RXD | GP8 (Pico UART1 TX) |
| TXD | GP9 (Pico UART1 RX) |

Attach the antenna before transmitting. TX and RX are **crossed**: the radio's
RXD is the Pico's TX and vice versa.

### Debug Probe (recommended)

| Debug Probe | Pico 2 |
| ----------- | ------ |
| SWCLK | SWCLK (3-pin debug header) |
| SWDIO | SWDIO |
| GND | GND |
| UART TX | GP1 (Pico RX) |
| UART RX | GP0 (Pico TX) |
| GND | GND |

The firmware enables stdio on **both** UART0 (`115200`) and USB, so you can
watch boot output on the probe's console or on the Pico's own USB serial port.
The Debug Probe is also the instrument for the Lab 3 incident-response work: it is
how you prove the siren is being silenced, read the reserved-sector marker,
inspect the beacon, and step past the anti-debug trap.

### Peripherals used

| Peripheral | Connection | Role |
| ---------- | ---------- | ---- |
| Three annunciator LEDs | GP16 red, GP17 yellow, GP18 green | Solid HAZARD, WATCH, and CLEAR lamps, one at a time. |
| Manual acknowledge button | GP15 to GND | Debounced local acknowledge; raises the WATCH indication and never changes the guarded hazard state. |
| 1602 I2C LCD | GP2 SDA, GP3 SCL, I2C1 address `0x27` | Hazard readout of state, link, zone, temperature, and sabotage marker. |
| DHT11 | GP4 | Chemical store temperature sensor, classified against `0.0 C` to `40.0 C`. |
| SG90 servo | GP14 | Siren and vent actuator driven by 50 Hz PWM. |
| 1000uF capacitor | across the servo 5V and GND rails | Bulk decoupling for the siren inrush; required in hardware and not firmware visible. |
| VS1838B infrared receiver | GP5 | Demodulated NEC input for the local maintenance remote. |
| NEC infrared remote | optical link to the VS1838B | Sends WARN, ACK, and TEST. |
| RYLR998 LoRa transceiver | GP8 RX, GP9 TX, UART1 at 115200 baud | Sealed hazard command link to the safety control gateway. |
| Onboard GP25 LED | GP25 | Onboard heartbeat; pulses once on every monitor tick. |
| Debug Probe | GP0 TX, GP1 RX, UART0, and SWCLK/SWDIO/GND | stdio console, flashing, and the GDB anti-debug work. |

Every peripheral above is used by the firmware. The 1000uF capacitor is a
hardware requirement rather than a firmware device. There is no transmit blink.

### How the functionality works

This is the end-to-end behavior of the running node: what each input does, what
each output shows, and how to watch the live console. The DHT11 is sampled every two seconds, so one live status line appears
about every two seconds.

**Inputs**

| Input | Pico 2 | What it does |
| ----- | ------ | ------------ |
| Infrared maintenance remote | GP5 (VS1838B) | Decodes a NEC frame into `WARN` (`0x47`, CH+), `TEST` (`0x45`, CH-), or `ACK` (`0x46`, CH). WARN and ACK raise the watch-pending indication; TEST is a maintenance marker. No remote code can change the guarded hazard state on its own. |
| Manual acknowledge button | GP15 to GND | A debounced press raises the watch-pending request. It asks for authorization and never bypasses the sealed hazard path or silences the siren. |
| DHT11 store sensor | GP4 | Samples the chemical store every tick and classifies it against the safe band. A failed read is not nominal. |
| RYLR998 LoRa radio | GP8/GP9, UART1 | Carries the sealed hazard command path. Every inbound frame is authenticated and anti-replay checked before it can move the siren. |

**Outputs**

| Output | Pico 2 | What it shows |
| ------ | ------ | ------------- |
| Red HAZARD LED | GP16 | Solid when a chemical release hazard is declared, a command was rejected, or the terminal failed safe. |
| Yellow WATCH LED | GP17 | Solid when the store is under watch or a manual acknowledge is pending authorization. |
| Green CLEAR LED | GP18 | Solid when the store is clear; in the SANDBOX_ONLY build the sabotage override forces this lamp during a declared hazard. |
| 1602 LCD | GP2/GP3, I2C1 `0x27` | Line 1 `ST:CLEAR  L:UP` is the state and safety link; line 2 `Z:4 T:235 M:--` is the storage zone, store temperature in tenths, and sabotage marker. |
| SG90 siren servo | GP14 | 50 Hz PWM: raised sounds the hazard, lowered shows clear or watch. |
| Onboard GP25 LED | GP25 | Pulses once on every monitor tick as the heartbeat; it is not a transmit blink. |

Exactly one annunciator lamp is lit at a time and no lamp blinks in the clean
firmware. The siren moves only after the guarded state machine decides.

**Watching the interactive console**

The firmware enables stdio on both UART0 (`115200`, Debug Probe) and the Pico's
own USB serial port (`115200`). Open either at **115200 8N1** and reset the
board. After `BOOT` and the I2C scan, the node prints a boot banner and then one
line per event:

```text
BOOT
I2C scan:
  found 0x27
=== OPERATION IRON CURTAIN // ACT X CHEMICAL WARNING TERMINAL ===
Remote: CH+ 0x47 WARN, CH- 0x45 TEST, CH 0x46 ACK
Button: local acknowledge request, never bypasses authorization
STORE t=235 ok=1 LED=3 cyc=12
IR WARN (0x47)
BUTTON acknowledge request -> pending
RX from 0x0001, 126 bytes
STORE read failed -> WARNING
```

| Line | Meaning |
| ---- | ------- |
| `STORE t=... ok=... LED=... cyc=...` | One live status line per reading cycle: store temperature in tenths, the in-band verdict, the effective annunciator state, and the reading-cycle count. |
| `STORE read failed -> WARNING` | The DHT11 did not answer or failed its checksum, so the store is treated as not nominal. |
| `IR <NAME> (0xNN)` | A decoded remote command, named `WARN`, `TEST`, `ACK`, or `UNKNOWN`. |
| `BUTTON acknowledge request -> pending` | The manual acknowledge button raised a pending request. |
| `RX from 0xNNNN, N bytes` | One inbound radio frame, with the reported sender address and payload length, before it is authenticated. |

<br>

## Build and Flash

### 1. Install toolchain prerequisites

- Pico SDK 2.2.0+
- ARM GNU toolchain (`arm-none-eabi`)
- CMake and Ninja
- Python 3.x
- GDB (`arm-none-eabi-gdb`) for the Lab 3 malware analysis

**Linux:**

```bash
export PICO_SDK_PATH="$HOME/.pico-sdk/sdk/2.2.0"
```

**macOS:**

```bash
brew install cmake ninja arm-none-eabi-gcc python
export PICO_SDK_PATH="$HOME/.pico-sdk/sdk/2.2.0"
```

**Windows:** install PowerShell, Visual Studio Build Tools, CMake, Ninja,
Python 3, and the ARM embedded toolchain.

### 2. Build the firmware

The clean firmware does **not** define `SANDBOX_ONLY`, so it ships no finale
implant:

```bash
mkdir -p build && cmake -S . -B build -G Ninja -DPICO_BOARD=pico2 -DPICO_PLATFORM=rp2350-arm-s && cmake --build build
```

To build the implant image with the beacon compiled in, turn the option on:

```bash
cmake -S . -B build-sandbox -G Ninja -DPICO_BOARD=pico2 -DPICO_PLATFORM=rp2350-arm-s -DSANDBOX_ONLY=ON && cmake --build build-sandbox
```

Build-time artifact guardrail:

- The build regenerates `packet_artifact.h` from
  `scripts/packet_artifact.json` before compiling.
- The build fails if the committed `include/packet_artifact.h` is stale relative
  to the JSON artifact.

Generated outputs:

- `build/chemical_warning_terminal.elf` (primary firmware binary)
- `build/chemical_warning_terminal.uf2` (UF2 for BOOTSEL/picotool)
- `build/chemical_warning_terminal_app.elf` / `.uf2` (backward-compatible copies)

### 3. Flash the RP2350

**BOOTSEL (drag-and-drop):** hold BOOTSEL while plugging in USB, then:

```bash
cp build/chemical_warning_terminal.uf2 /Volumes/RP2350/
```

**picotool:**

```bash
picotool load build/chemical_warning_terminal.uf2 -fx
```

*(If `picotool` is not on your PATH, invoke it from
`$HOME/.pico-sdk/picotool/*/picotool/picotool`.)*

**Debug Probe (SWD):** with `openocd` installed you can flash and reset without
touching BOOTSEL:

```bash
openocd -f interface/cmsis-dap.cfg -f target/rp2350.cfg \
  -c "program build/chemical_warning_terminal.elf verify reset exit"
```

### 4. Watch the console

Open the UART0 console (Debug Probe) or the Pico's USB serial port at `115200`.
On reset you should see:

```text
BOOT
I2C scan:
  found 0x27
=== OPERATION IRON CURTAIN // ACT X CHEMICAL WARNING TERMINAL ===
Remote: CH+ 0x47 WARN, CH- 0x45 TEST, CH 0x46 ACK
Button: local acknowledge request, never bypasses authorization
STORE t=0 ok=1 LED=3 cyc=1
```

`found 0x27` confirms the LCD backpack answered on the I2C bus. The boot banner
names the operation and the remote button roles, and `STORE t=... ok=... LED=...
cyc=...` is the live status line printed every reading cycle. The full set of
console lines is described in
[How the functionality works](#how-the-functionality-works). If a peripheral
fails, the firmware prints `INIT FAIL` and stops.

<br>

## Lab 1: Bring-Up and Verify

**Goal:** prove the node reads the store temperature, drives the LCD, takes a
local acknowledge, reaches the gateway, and moves the siren.

1. Wire the node per the pin map and attach the antenna.
2. Build and flash the clean firmware.
3. Connect the gateway radio to the laptop and find its port (`/dev/cu.usbserial-*`
   on macOS, `/dev/ttyUSB*` on Linux).
4. Start the safety control gateway:

   ```bash
   python3 scripts/gateway.py --port /dev/cu.usbserial-XXXX --baud 115200
   ```

5. Send a sealed zone request from the edge simulator, or seal one from a node.
   The gateway prints it, then answers with a sealed hazard command:

   ```text
   +OK
   +OK
   +RCV=7,84,<84 hex characters>,-11,10
   SIREN raise seq=1 zone=4
   ```

6. The node turns yellow (WATCH) when a manual acknowledge is pending, receives
   the command, verifies the state tag and the anti-replay window, then drives
   the siren to the authorized position. Press the manual acknowledge button at
   any time to raise a request.

**Checkpoint:** the LCD shows `ST:CLEAR L:UP` and `Z:4 T:235 M:--`, one lamp is
lit after the siren settles, and `chem_log.csv` gains one row per request:

```text
utc,sender,auth,zone,rssi_snr
2026-09-20T09:30:05+00:00,7,OK,4,"-11,10"
```

**Theory check:** why does a successful command prove the LCD initialized?
Because `monitor_init()` only returns true when every peripheral, including the
LCD, is ready; otherwise `main` prints `INIT FAIL` and never enters the loop.

<br>

## Lab 2: Inspect the Wire Protocol

**Goal:** see the sealed envelope and the declared-length rule in action.

1. Capture a full `+RCV` line from the console or the gateway log.
2. Confirm the declared length equals the number of hex characters between the
   second comma and the RSSI field.
3. Split the hex into three parts: the first 48 hex characters are the 24-byte
   nonce, the last 32 are the 16-byte tag, and everything between is the
   ciphertext of the request or command body.
4. Locate the payload, its declared length, and the two tail fields in
   `scripts/gateway.py` (`_rcv_parts` and `_split_payload`), and explain why
   finding the *first* comma would be a bug.
5. Challenge: for the 23-byte command body, identify the four bytes of the
   sequence number, the one command byte, the two zone bytes, and the sixteen
   bytes of the state tag.

**Checkpoint:** you can explain why a frame must be sliced by the number in the
declared length field, not by delimiter counting, and why the command byte and
the zone are range-checked against the guarded set and the bounded band before
they can reach the siren decision.

<br>

## Lab 3: The Finale Track

**Goal:** find the FROSTLINE coordinated beacon, prove that it silences the siren
and forces the all clear, expose its sabotage marker, cut the beacon, break the
persistence, clear the marker, and remove it for good. This is the coordinated
finale, and this lab is its heart.

> Safety: the implant is benign and confined to your breadboard. It drives only
> your mock siren servo and your mock LCD, it stands down on a documented token,
> and it writes only the reserved sector at `0x103FF000`, on the same chip. There
> is no network, no filesystem, and no host impact. The sabotage marker is a real
> sector erase and program, but the siren and the display are the only things it
> affects, and it holds no real hazard.

### Build the implant image

```bash
cmake -S . -B build-sandbox -G Ninja -DPICO_BOARD=pico2 -DPICO_PLATFORM=rp2350-arm-s -DSANDBOX_ONLY=ON && cmake --build build-sandbox
```

The clean build does not define `SANDBOX_ONLY`; the test build and the companion
CTF build do. Compare the two binaries and explain why the beacon symbols are
absent from the clean one.

### A: Find the coordinated beacon and the marker

1. Flash the `SANDBOX_ONLY` image and let it boot once. `implant_init` writes the
   `0x58` marker into the reserved sector at `0x103FF000` on the first run with
   the real flash API.
2. Read the reserved sector with the Debug Probe or `picotool` and confirm the
   marker byte. The LCD sabotage field reads `M:SAB`.
3. Watch the panel. While the marker is present the beacon forces the effective
   state to `CLEAR`, silences the siren, lights the green CLEAR lamp, and renders
   `ST:SAFE`, even though the guard state would otherwise sound the hazard siren.
4. Locate `implant_init`, `implant_beaconize`, and `implant_infect`, and explain
   why the beacon and the sabotage are local conditions that ignore the sealed
   command path.

**The lesson:** the beacon does not need the wire or the key, because it changes
the output after the authenticated decision is made.

### B: Cut the coordinated beacon

1. Read `implant_tick`, `implant_advance_stage`, and
   `CHEM_IMPLANT_BEACON_STAGES`: a full check-in cycle is three stages, and the
   beacon re-asserts every `CHEM_IMPLANT_BEACON_INTERVAL` (4) ticks.
2. Prove the multi-stage check-in by stepping the tick counter and reading
   `implant_stage()` and `implant_beacon_count()`, and show that the marker is
   re-written on each due tick.
3. Call `implant_neutralize`, or present the exact 24-byte
   `IRON-CURTAIN-BEACON-2026` token to `implant_disable`, and prove the beacon
   stands down and the stage resets.
4. Present a wrong token, a short token, and a null pointer, and prove each one
   leaves the beacon armed.

**The lesson:** cutting the beacon stops the check-in, but it does not remove the
state that re-arms a future boot.

### C: Break the persistence

1. Read `implant_init`: on the first run the marker is absent and `implant_infect`
   writes it; on every later boot the marker is present and the beacon
   re-installs and records `implant_reinstalled()`.
2. Reflash only the firmware image (the clean image is ideal) and let the node
   boot again. Because the marker is still in the reserved sector, the beacon
   re-installs and the display returns to `M:SAB`.
3. Prove the persistence by reading the reserved byte after the reflash, and
   explain why a firmware reflash does not touch the reserved sector.
4. Explain why BOTH steps are required: cutting the beacon makes the siren honest
   now, and clearing the marker removes the state that would re-arm a future boot.

**The lesson:** a coordinated payload has two copies, the one in the image and
the one in the state. You remove the payload and you remove the marker.

### D: Clear the sabotage marker

1. Read the marker at `0x103FF000` and confirm it is the `0x58` byte.
2. Erase the reserved sector, or call `implant_neutralize`, and prove the node
   comes up with the marker gone and the `M:` field on the LCD back to `--`.
3. Reflash only the firmware image and let the node boot again. Because the
   marker is gone, the beacon does not re-install and the siren is honest.
4. Explain why clearing the marker is the incident-response control that closes
   the persistence, not merely a cleanup.

**The lesson:** the marker is the persistence. Clearing it is how the response
removes the ability to lie on the next boot.

### E: Defeat the anti-debug with GDB

This is the dynamic-analysis trap. The beacon reads CoreDebug `DHCSR` at
`0xE000EDF0`; bit 0 is `C_DEBUGEN` and bit 1 is `C_HALT`. While a probe is
attached, the beacon suppresses the marker and the sabotage.

1. Start the controller under the Debug Probe:

   ```bash
   arm-none-eabi-gdb build-sandbox/chemical_warning_terminal.elf
   (gdb) target extended-remote /dev/cu.usbmodemXXXX
   (gdb) monitor reset halt
   ```

2. Break in `implant_tick` and inspect `implant_debug_attached`. With a normal
   probe attached, it returns true, and the beacon is suppressed.
3. Set a breakpoint after the anti-debug check, or clear the `DHCSR` debug bits
   in the debugger's view, and observe the beacon and the `ST:SAFE` lie resume.
4. Prove the release: with the trap bypassed, present the magic token and watch
   the marker clear and the true hazard state return.

**The lesson:** an anti-debug check is a branch, and every branch is a place to
stand. The correct neutralization is not to babysit the branch; it is to remove
the code and the state it reads, and to make the terminal fail safe by policy.

### Finale checklist

- Locate the reserved-sector marker and explain the write-once first run.
- Identify the `0x58` marker, the `IRON-CURTAIN-BEACON-2026` token and its
  24-byte length, the 4-tick re-assertion interval, and the 3-stage cycle.
- Show the forced all clear and the `ST:SAFE` state, and prove they ignore the
  sealed command path.
- Cut the beacon with the magic token and clear the marker.
- Read and explain the CoreDebug `DHCSR` anti-debug trap.
- Erase the reserved sector, remove the code path, and confirm the clean build is
  beacon-free and marker-free.

<br>

## Lab 4: The Fix Track

**Goal:** seal the terminal so the red half and the implant cannot do to you what
they did on the bench. Each control maps to a defect the earlier labs exposed.

### 1. Seal the hazard command path

The old design accepted an unauthenticated hazard command. Act X replaces it
with `src/control.c`: the request must open under the field key, the command byte
must be in the guarded hazard set, the zone must be inside the provisioning band,
and the sequence and state tag must pass `src/chem_auth.c` before the command is
applied. Re-run the Lab 3 forged-command injection: the tag fails and the siren
does not move.

### 2. Acknowledge authorization

The local acknowledge request is an operator request, and it must not silently
bypass authorization. `monitor_handle_ack` and `monitor_apply_ir_command` raise
`g_ack_pending`; they never change the guarded hazard state on their own.
`monitor_apply_command` clears the pending indication only when an authorized
command arrives. Re-run the lab: press the acknowledge button, then send a valid
sealed hazard command. The siren moves only from the authorized command, and the
yellow WATCH lamp returns to green only then.

### 3. No untrusted task execution

The clean build compiles the beacon path out entirely, so an untrusted frame can
never force an all clear or silence the siren (`monitor_implant_init` and
`monitor_implant_tick` are no-ops in the clean build). The lesson is that a
control node must never let a local condition override an authorized decision or
the temperature interlock. In the fix track, remove the `SANDBOX_ONLY` build flag
and erase the reserved sector so no node can be seeded again.

### 4. Fail to the safe hazard state

Loss of the control link or a fault must leave the store in the safe state.
`monitor_check_link` calls `monitor_fail_safe` when the link goes silent for
`CHEM_LINK_WAIT_MS`, which sets the hazard state, drives the fail-safe zone, and
calls `siren_fail_safe` to raise the siren. `siren_init` raises the hazard siren
at boot. Re-run the link-loss test: pull the gateway and watch the siren raise
and the fail-safe posture latch, with the zone returned to `0`.

### 5. Contain the implant

The implant is a build-time and state-handling problem, so the fix is a
build-time and state-handling control:

- Do not define `SANDBOX_ONLY` in production. The clean build has no beacon.
- Erase the reserved sector so no persisted state can re-install the payload.
- Treat the firmware image as a signed artifact and verify it before flashing.
- At runtime, never let a condition override an authorized command or the
  temperature interlock; route every move through the guarded, authorized path
  and record who authorized it.
- In production, burn the RP2350 secure-boot and debug-disable settings in OTP so
  SWD cannot read or write SRAM on a deployed controller.

### The fix-track checklist

- Sealed command path: authenticate the frame, guard the command set and the
  zone band, verify the sequence and the state tag.
- Acknowledge authorization: request, do not bypass.
- No untrusted override: the node never forces an all clear because of a local
  latch, and never silences the siren against the interlock.
- Fail safe: raise the siren on boot, fail safe on link loss, and return the
  fail-safe zone.
- Implant removal: cut the beacon, clear the marker, erase the reserved sector,
  and remove the code path.
- Build integrity: no `SANDBOX_ONLY` in production, sign and verify images.
- Debug lockdown: OTP debug disable on the deployed part.
- Key lifecycle: provision the field key from OTP and rotate on a schedule.

<br>

## Troubleshooting

| Symptom | Likely cause | Fix |
| ------- | ------------ | --- |
| No `BOOT` on the console | Wrong console pins / not reset | Check UART0 GP0/GP1 or USB; press RESET |
| `INIT FAIL` with no `0x27` in the scan | LCD not answering | Check LCD VCC=3.3V, SDA=GP2, SCL=GP3, contrast pot |
| LCD shows blocks / nothing | Contrast or address | Turn the backpack contrast pot; confirm address `0x27` vs `0x3F` |
| Store temperature always bad | DHT11 not reading | Check DATA=GP4; add 10K pull-up to 3.3V; wait 1-2 s after power-up |
| IR remote does nothing | Receiver wiring or remote protocol | Check OUT=GP5, VCC=3.3V; confirm the remote is NEC-compatible |
| Siren will not move on a remote command | Command guard, band, or tag | Confirm the gateway holds the field key and the zone is inside 0 to 16 |
| `AT+SEND` sent but gateway sees nothing | Radio unpowered / wrong band | **Power VDD**, attach antenna, use matching band modules |
| Gateway sees nothing but `+OK` | Address/network mismatch | Confirm gateway radio provisioned to `AT+ADDRESS=1`, `AT+NETWORKID=18` |
| `chem_log.csv` stays empty while `+RCV` prints | Gateway parser regression | Ensure `_split_payload` checks the comma at the declared length |
| Command rejected on the controller | Tag, window, command guard, or band | Check the field key matches, the sequence is newer, and the zone is in band |
| LCD shows `M:SAB` or `ST:SAFE` while nothing looks wrong | Sabotage marker present (SANDBOX_ONLY build) | The beacon has written the marker; see Lab 3A |
| Siren stays silent despite an authorized hazard | Sabotage override (SANDBOX_ONLY build) | Expected in the malware-track build; cut the beacon in Lab 3B |
| Marker reappears after a reflash | Reserved-sector persistence | The payload is still in the reserved sector; clear it and remove the code path (Lab 3) |
| Debugger changes implant behavior | CoreDebug `DHCSR` anti-debug | The beacon suppresses itself while a probe is attached; see Lab 3E |
| Node forces an all clear | Local override | In production never define `SANDBOX_ONLY`; see Lab 4 |

<br>

## Testing Philosophy and Coverage

Hardware bugs are expensive to find on the bench, so the firmware is written so
that almost all of it can be tested on the host. The suite compiles the real
`src/*.c` files against mock Pico SDK headers (`test/mock/`), replacing GPIO,
I2C, UART, and time with deterministic fakes, and it compiles `src/implant.c`
with a host mock for the CoreDebug `DHCSR` register and the reserved flash
sector.

- The mock GPIO can replay a recorded DHT11 waveform as an absolute time/level
  timeline, so the exact edge-timing decoder is exercised without a sensor.
- The mock I2C records every LCD byte, so rendered text can be decoded and
  asserted.
- The mock UART records outbound `AT+SEND` bytes and injects inbound `+RCV`
  lines, so the operator-to-gateway-to-siren path runs end to end with no radio.
- The implant host mock lets the tests set the `DHCSR` anti-debug bits and read
  and write the reserved-sector marker without touching real silicon, and it
  exposes the beacon stage and the sabotage override so the `0x58` marker path
  can be asserted.

Run the native test suite:

```bash
python3 scripts/run_tests.py
```

Or configure via CMake and CTest:

```bash
cmake -S test -B build-test -G Ninja && cmake --build build-test && ctest --test-dir build-test --output-on-failure
```

The suite has **145 cases** and **501 checks** with **0 failures**, covering the
full DHT11 waveform and every timeout shape, the siren state machine and its
bounded travel, the sealed command path and its guards, the authorization window
and state tag, the acknowledge no-bypass path, fail safe on link loss, the
declared-length parser with hex-bearing payloads, the cryptographic primitives
against published vectors, and the complete coordinated beacon: the multi-stage
check-in, the forced all clear, the `0x58` marker, re-install on boot, the magic
beacon command, and anti-debug.

Verify **100% line coverage** of owned firmware modules:

```bash
python3 scripts/check_coverage.py
```

The coverage report shows **2123 / 2123 lines, 100.00%**. `main.c` is excluded
from coverage by design. The Python adapter suite (`test/test_field_crypto.py`
and `test/test_chem_node.py`) adds 17 more tests, including the RFC 9106
Argon2id known-answer test.

The harness itself is a small in-repo framework (`test/harness/`) so the repo
vendors no third-party code and every owned file obeys the coding standard.

<br>

## Generating Packet Artifacts

`scripts/gen_packet.py` writes the build-time generated header from the JSON
artifact:

- `scripts/packet_artifact.json` is the source of truth.
- `include/packet_artifact.h` is the generated header, committed for the build
  guardrail.

Why these constants are compiled into firmware:

- The RP2350 firmware has no runtime JSON parser or filesystem on this path.
- `include/packet_artifact.h` is generated from the JSON so the frame size, node
  id, gateway address, wait time, servo pulses, DHT timeout, and provisioning
  constants are embedded in flash.
- This is provisioned data; regenerate whenever you rotate node identity,
  gateway addressing, or key material.

To sync the committed header from the JSON artifact:

```bash
python3 scripts/gen_packet.py --from-json scripts/packet_artifact.json --header-out include/packet_artifact.h
```

The `check_packet_artifact_header` CMake target fails the build when the
committed header is stale.

<br>

## Code Standards

This repository enforces unusually strict standards because the point is to
teach disciplined embedded and tooling practice, not just working code.

### C standard

- Every function body has **no blank lines**.
- Every function body is **at most eight lines** (Doxygen comment blocks and
  lone braces excluded).
- Every file, function, macro, type, and struct member carries Doxygen
  `@brief` documentation.
- Naming: `snake_case` files/functions, `UPPER_SNAKE` macros, `snake_case_t`
  types.

Run the C audit:

```bash
python3 scripts/audit_c_standard.py
```

### Python standard

- Strict PEP8, four-space indents, `snake_case`, 79-character lines.
- Every function has a NumPy-style docstring.
- Every function executable body is **at most eight lines**, with no exceptions.
- No blank lines inside function bodies.

Run the Python audit:

```bash
python3 scripts/audit_python_standard.py
```

Both audits must report nothing.

<br>

## Project Layout

- `src/main.c`: firmware entry point
- `src/monitor.c`: state machine tying the maintenance remote, sealed command path, siren, manual acknowledge request, temperature sensor, and radio together
- `src/implant.c`: SANDBOX_ONLY FROSTLINE coordinated beacon (multi-stage check-in, `ST:SAFE` override, magic beacon command, reserved-sector `0x58` marker, re-install, CoreDebug anti-debug)
- `src/siren.c`: siren state machine and fail-safe policy
- `src/control.c`: sealed hazard command path with a guarded command set and a bounded zone band
- `src/chem_auth.c`: authorization record, monotonic anti-replay window, authenticated state tag
- `src/sensor.c`: DHT11 one-wire sampling and store-temperature-band classifier
- `src/display.c`: 1602 LCD rendering over the PCF8574 I2C backpack
- `src/radio.c`: RYLR998 provisioning, AT-command interface, and `+RCV` parser
- `src/status_led.c`: red/yellow/green HAZARD / WATCH / CLEAR annunciator light
- `src/button.c`: debounced manual acknowledge input
- `src/servo.c`: 50 Hz PWM siren and vent actuator
- `src/ir_remote.c`: VS1838B edge timing and NEC maintenance remote decoder
- `src/crc.c`: CRC-16/CCITT-FALSE helper
- `src/chacha20.c`, `src/poly1305.c`, `src/crypto_aead.c`, `src/blake2b.c`, `src/argon2.c`, `src/crypto_kdf.c`, `src/envelope.c`: the in-repo cryptographic stack
- `include/chem.h`: board-level pin, provisioning, and hazard configuration
- `include/implant.h`, `include/control.h`, `include/chem_auth.h`, `include/siren.h`: beacon, command, authorization, and siren interfaces
- `include/field_secrets.h`: lab-only committed key material
- `include/packet_artifact.h`: generated packet artifact header
- `test/test_chem_node_and_security.c`, `test/test_peripheral_and_crypto.c`: comprehensive test suites
- `test/mock/`: Pico SDK hardware mocks plus the implant CoreDebug and reserved-flash host mock
- `test/harness/`: minimal in-repo test harness (strictly C-standard compliant)
- `scripts/gateway.py`: safety control gateway with radio provisioning, authentication, CSV logging, and sealed command replies
- `scripts/spoof.py`: forged and replayed command injection client
- `scripts/sim_edge.py`: laptop warning terminal simulator
- `scripts/field_crypto.py`: pure-Python interoperable crypto
- `scripts/gen_packet.py` / `scripts/packet_artifact.json`: packet artifact generator and source
- `scripts/run_tests.py`, `scripts/check_coverage.py`: test runner and coverage report
- `scripts/audit_c_standard.py`, `scripts/audit_python_standard.py`: code-standard auditors
- `scripts/gen_banner.py`: banner generator
- `paper.typ` / `paper.pdf`: classroom paper describing the protocol, the coordinated beacon, and the exercise
- `.github/workflows/release.yml`: tag-driven UF2 release workflow

<br>

## Glossary

- **AEAD**: authenticated encryption with associated data; one operation for
  secrecy and integrity.
- **Anti-debug**: a check that detects an attached debugger and changes behavior.
  Here it reads CoreDebug `DHCSR` at `0xE000EDF0` (bits `C_DEBUGEN` and
  `C_HALT`).
- **Anti-replay window**: a monotonic sequence rule that rejects a valid frame
  that has already been used.
- **Argon2id**: the memory-hard password hash (RFC 9106) used to derive the field
  key.
- **AT command**: a short ASCII command (`AT+...`) understood by the radio.
- **Beacon**: the coordinated multi-stage check-in the finale implant runs every
  four ticks.
- **Declared length**: the byte count the sender claims for a payload; the
  receiver slices exactly that many characters.
- **DHT11**: a low-cost temperature/humidity sensor using a custom one-wire
  protocol, used here as the chemical store temperature sensor.
- **Fail safe**: a fault raises the siren to the safe hazard posture and returns
  the fail-safe zone.
- **Field key**: the key that seals frames on the wire and computes the state
  tag.
- **HD44780**: the character-LCD controller inside a 1602 module.
- **I2C**: a two-wire bus (SDA/SCL) used here for the LCD backpack.
- **Implant**: code that runs on the device but is not part of its intended
  function. Here the SANDBOX_ONLY FROSTLINE coordinated beacon.
- **LoRa**: a long-range, low-power sub-GHz radio modulation.
- **Magic beacon command**: the exact 24-byte `IRON-CURTAIN-BEACON-2026` string
  that arms or releases the beacon.
- **Masking**: a local condition that makes a hostile state read as a routine one;
  here the forced all clear and the `ST:SAFE` label.
- **NEC**: the infrared remote encoding the VS1838B decodes.
- **PCF8574**: an I2C I/O expander that drives the LCD's parallel interface.
- **Reserved sector**: the final flash sector at `0x103FF000`, used here to hold
  the one-byte sabotage marker.
- **Sabotage marker**: the `0x58` byte the beacon writes into the reserved
  sector.
- **SANDBOX_ONLY**: the build guard that compiles the benign finale implant. The
  clean firmware does not define it.
- **State tag**: a keyed tag over the authorization record that detects a
  tampered verdict.
- **Tower light**: the red/yellow/green HAZARD / WATCH / CLEAR lamps.
- **UART**: a serial port used to talk to the radio.
- **XChaCha20-Poly1305**: the AEAD used for every sealed frame, with a 192-bit
  nonce and a 128-bit tag.

<br>

## Further Reading

- Act I, the sensor and telemetry chapter:
  https://github.com/mytechnotalent/cold-chain-monitor
- Act II, the access gate chapter:
  https://github.com/mytechnotalent/access-gate
- Act III, the pipeline valve chapter:
  https://github.com/mytechnotalent/pipeline-valve-controller
- Act IV, the HVAC automation node chapter:
  https://github.com/mytechnotalent/hvac-automation-node
- Act V, the industrial tamper system chapter:
  https://github.com/mytechnotalent/industrial-tamper-system
- Act VI, the smart logistics drop-box chapter:
  https://github.com/mytechnotalent/smart-logistics-dropbox
- Act VII, the factory andon station chapter:
  https://github.com/mytechnotalent/factory-andon-station
- Act VIII, the datacenter vent controller chapter:
  https://github.com/mytechnotalent/datacenter-vent-controller
- Act IX, the smart parking barrier chapter:
  https://github.com/mytechnotalent/smart-parking-barrier
- The companion CTF for this act:
  https://github.com/mytechnotalent/CTF_chemical-warning-terminal
- Embedded Hacking course and breadboard:
  https://github.com/mytechnotalent/Embedded-Hacking
- Reverse Engineering self-study course:
  https://github.com/mytechnotalent/Reverse-Engineering
- `paper.typ` / `paper.pdf`: the classroom paper for this project.
- DHT11 datasheet, RYLR998 AT command reference, SG90 datasheet, and VS1838B
  datasheet (module vendors).

<br>

# Next
[OPERATION IRON CURTAIN CTF](https://github.com/mytechnotalent/CTF_chemical-warning-terminal)

<br>

# License
[MIT License](https://github.com/mytechnotalent/chemical-warning-terminal/blob/main/LICENSE)
