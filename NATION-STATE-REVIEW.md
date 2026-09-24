# OPERATION IRON CURTAIN - Nation-State Accuracy Review

**An adversarial, evidence-based audit of the entire project where every claim is
verified by a re-runnable command or explicitly labelled as a limitation.**

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

## 1. Scope and Method

This review treats the project as hostile-to-itself. Every module, constant, test
vector, document, and artifact is independently checked. The method is:

1. **Re-run every gate** (`audit_c_standard`, `audit_python_standard`,
   `run_tests`, `check_coverage`) and record the exact output and exit codes.
2. **Re-verify every constant** against the generated artifact header and the
   JSON source of truth, by regenerating the header and diffing it.
3. **Re-verify every cryptographic claim** against a published standard vector,
   and separate vectors that run in the native C suite from vectors that run only
   in the Python suite.
4. **Audit the coordinated finale adversarially**, with a dedicated Coordinated
   Attack and Incident Response section: what it does, how it forces the all
   clear, how it silences the siren, how it beacons, how it persists across a
   reflash, how it is detected and removed, how it is bounded, and what it does
   not prove.
5. **Re-verify every artifact** by SHA-256 and by the in-repo build guardrail,
   because this project ships no CTF firmware artifact.
6. **Read the documents adversarially** for overclaims, stale numbers, and
   omissions, then correct them in this review.

## 2. Gate Results (all re-run for this review)

| gate | command | observed result |
|---|---|---|
| C standard | `python3 scripts/audit_c_standard.py` | exit 0, no output, **0 violations** |
| Python standard | `python3 scripts/audit_python_standard.py` | exit 0, no output, **0 violations** |
| Native tests | `python3 scripts/run_tests.py` | **501 checks, 0 failures**, 145 test cases |
| Coverage | `python3 scripts/check_coverage.py` | exit 0, **100.00% line coverage**, 2123 owned lines |
| Python suites | `python3 -m unittest test.test_field_crypto test.test_chem_node` | **17 tests, OK** |
| Header guardrail | `python3 scripts/gen_packet.py --from-json scripts/packet_artifact.json --header-out /tmp/if_cwt.h --check-header-path include/packet_artifact.h` | exit 0, `Verified header matches` |

The coverage gate passes on line coverage. It does not require 100% branch or
region coverage, and the raw report is not 100% there: regions 99.26% and
branches 93.77%. That gap is real and is stated in the module table below.

## 3. Module-by-Module Audit

Owned lines are the instrumented statement lines reported by `llvm-cov report`
through `check_coverage.py`. Raw `wc -l` over `src/*.c` includes comments and
blank lines; `main.c` is excluded from coverage by design. Every owned module is
at 100.00% line coverage.

| module | role | owned lines | line coverage | verification performed | honest limitation |
|---|---|---|---|---|---|
| `crc.c` | CRC-16/CCITT-FALSE diagnostic | 20 | 100.00% | `test_crc16_ccitt` check value `0x29B1` | not on the wire; a checksum is not authentication |
| `sensor.c` | DHT11 store-temperature-band classifier | 151 | 100.00% | waveform, all timeout shapes, CRC error, store ok/reject/invalid, negative temperature | mock GPIO replays a recorded waveform, not real silicon |
| `display.c` | HD44780 over PCF8574 | 73 | 100.00% | `test_display_format_lines`, `test_display_render_lines` via recorded I2C | mock I2C, not real HD44780 bus timing |
| `radio.c` | RYLR998 provisioning, `AT+SEND`, `+RCV` parser | 187 | 100.00% | build/parse/reject/pump, oversize guards, spoofed sender attribution | mock UART; the RF band is not simulated |
| `status_led.c` | red/yellow/green HAZARD/WATCH/CLEAR annunciator | 14 | 100.00% | `test_status_led_show` | none |
| `button.c` | manual acknowledge/debounce input | 35 | 100.00% | pressed/consume/debounce/reset | active-low input is exercised only through mocks |
| `servo.c` | 50 Hz siren PWM | 26 | 100.00% | `test_servo_map`, `test_servo_init`, `test_servo_actuate` | mock PWM; no real servo or inrush load |
| `ir_remote.c` | VS1838B NEC maintenance decode | 116 | 100.00% | decode valid/reject/bad leader/mark/ambiguous/address/command, `test_ir_poll_*` | optical path is unauthenticated; no anti-replay |
| `siren.c` | siren state machine and fail-safe policy | 41 | 100.00% | `test_siren_init`, `test_siren_raise_travel`, `test_siren_lower_travel`, `test_siren_fail_safe`, `test_siren_reject_unauthorized` | bounded travel only; no real siren or load |
| `control.c` | sealed hazard command path | 96 | 100.00% | `test_control_handle_success`, bad command, bad zone, bad tag, replay, short body, key guards | shared lab key; guarded set is three commands |
| `chem_auth.c` | anti-replay window and state tag | 74 | 100.00% | `test_chem_auth_state_tag`, apply window/advance/bad tag, null, key, and tag guards | deterministic nonce from sequence; single key |
| `chacha20.c` | ChaCha20 and HChaCha20 | 99 | 100.00% | RFC 8439 block and stream vectors, HChaCha20 draft vector | none |
| `poly1305.c` | Poly1305 one-time authenticator | 169 | 100.00% | RFC 8439 tag vector, aligned path | none |
| `crypto_aead.c` | XChaCha20-Poly1305 seal/open | 38 | 100.00% | round-trip, tamper tag/ct/ad, constant-time `tag_equal` | built from the in-repo primitives, not an audited library |
| `blake2b.c` | BLAKE2b and Argon2 H' | 161 | 100.00% | `test_blake2b_abc`, multiblock, H' 32 and 256 vectors | none |
| `argon2.c` | Argon2id core (BLAMKA, hybrid addressing) | 336 | 100.00% | `test_argon2_lanes`, `test_argon2_type_i`, `test_argon2_clamp` branch coverage | the RFC 9106 KAT runs in Python, not in this C suite |
| `crypto_kdf.c` | Argon2id field key derivation | 28 | 100.00% | reject, empty password, determinism, salt sensitivity | classroom profile `t=3 p=1 m=64`; committed passphrase and salt |
| `envelope.c` | hex nonce/ciphertext/tag codec | 91 | 100.00% | nonce, round-trip, seal/open rejects, uppercase, known vector | none |
| `monitor.c` | warning terminal state machine | 269 | 100.00% | init, idle, render (including sabotage), temperature, maintenance remote, remote hazard/clear/watch/replay/bad tag/bad command/bad zone, acknowledge no-bypass, link loss, link unseen/within, safety interlock, sabotage lie, and sabotage restore | mocks are not the real silicon |
| `implant.c` | SANDBOX_ONLY FROSTLINE coordinated beacon | 99 | 100.00% | first run, re-install on boot, sabotage marker, debug attached, multi-stage tick, arm/release accept/reject/debug, neutralize, clean tick | benign educational payload; build-guarded and breadboard-bound |
| `main.c` | entry point | n/a | excluded | build only | excluded from coverage by design |

**Total owned lines at 100.00% line coverage: 2123.**

Branch coverage below 100% in the same report: `display.c` 85.71%, `monitor.c`
87.76%, `radio.c` 89.87%, `control.c` 90.48%, `chem_auth.c` 92.31%,
`envelope.c` 92.86%, `sensor.c` 94.74%, `ir_remote.c` 96.00%, `implant.c`
96.15%, and `argon2.c` 97.56%. `crc.c`, `status_led.c`, `button.c`, `servo.c`,
`siren.c`, `chacha20.c`, `poly1305.c`, `crypto_aead.c`, `blake2b.c`, and
`crypto_kdf.c` are at 100.00% branch coverage (or have no branches).

## 4. Cryptographic Claim Verification

The native suite asserts the following published vectors. Each name below appears
as a passing case in the `run_tests.py` output for this review.

| claim | standard | vector | observed |
|---|---|---|---|
| ChaCha20 block function | RFC 8439 section 2.3.2 | key 00..1f, nonce 000000090000004a00000000 | `test_chacha20_block` PASS |
| ChaCha20 stream cipher | RFC 8439 section 2.4.2 | "Ladies and Gentlemen..." 114-byte ciphertext | `test_chacha20_stream` PASS |
| HChaCha20 subkey | XChaCha20 draft (irtf-cfrg-xchacha) | published subkey vector | `test_hchacha20` PASS |
| Poly1305 tag | RFC 8439 section 2.5.2 | "Cryptographic Forum Research Group" tag `a8061dc1305136c6c22b8baf0c0127a9` | `test_poly1305`, `test_poly1305_aligned` PASS |
| BLAKE2b-512 | BLAKE2 reference | digest of "abc", multiblock, long-input | `test_blake2b_abc`, `test_blake2b_multiblock` PASS |
| Argon2 variable-length hash H' | RFC 9106 section 3.3 | H' of {1,2,3,4} at 32 and 256 bytes | `test_blake2b_long_short`, `test_blake2b_long` PASS |
| Argon2id known-answer | RFC 9106 section 5.3 | `0d640df58d78766c08c037a34a8b53c9d01ef0452d75b65eb52520e96b01e659` | `test.test_field_crypto.TestFieldCrypto.test_rfc9106_argon2id_vector` PASS (Python suite) |
| Envelope layout | project vector | known nonce, node id 7, fixed body | `test_envelope_known_vector` PASS |
| Firmware and Python interop | project vector | shared field key and envelope | `test_field_key_matches_firmware`, `test_envelope_matches_firmware` PASS (Python suite) |

The RFC 9106 Argon2id known-answer test is a Python `unittest` in
`test/test_field_crypto.py`; it is not part of the 501 native checks. Running the
Python suites directly confirms all 17 tests pass, including the KAT and the
firmware-interop vectors.

### 4.1 Sealed hazard path, guarded set, and bounded zone band

`src/control.c` opens the envelope under the field key with the warning node id
as associated data, then `control_parse` rejects the body unless the command byte
is one of `CHEM_COMMAND_HAZARD` (`0x01`), `CHEM_COMMAND_CLEAR` (`0x02`), or
`CHEM_COMMAND_ACK` (`0x03`), and the decoded zone lies between `CHEM_ZONE_MIN`
(`0`) and `CHEM_ZONE_MAX` (`16`). The guarded set is therefore exactly those
three commands, and the accepted zone band is exactly 0 to 16. The behavior is
asserted by `test_control_handle_success`, `test_control_command_set`,
`test_control_authorize`, `test_control_replay`, `test_control_bad_command`,
`test_control_bad_zone`, `test_control_bad_tag`, `test_control_short_body`, and
`test_control_key_guards`. All pass in this review.

Note that `scripts/gateway.py` sends `CHEM_COMMAND_HAZARD = 1`, which agrees with
the firmware decoding `0x01` as hazard, and `scripts/spoof.py` forges
`CHEM_COMMAND_CLEAR = 2`, which agrees with the firmware decoding `0x02` as
clear. There is no tooling/firmware command-constant mismatch in this act.

### 4.2 Anti-replay sequence window

`chem_auth_apply` in `src/chem_auth.c` accepts a command only when `seq >
auth->last_seq`, then verifies the keyed tag against the candidate record, then
advances the floor. The behavior is asserted by `test_chem_auth_apply_window`
(accept once, reject the same sequence, reject an older sequence),
`test_chem_auth_apply_advance` (a newer sequence advances `last_seq`),
`test_chem_auth_bad_tag`, and the end-to-end `test_monitor_remote_replay`. All
pass in this review.

Honest limitation: `last_seq` is plain SRAM and resets to zero on every boot, so
a command captured before a reboot can be replayed after one. The paper's Threat
Model states this; the README does not. A production controller would persist the
floor in non-volatile memory.

### 4.3 Authenticated state tag

`chem_auth_state_tag` seals a nine-byte record (`granted`, `seq[4]`,
`last_seq[4]`) under the field key with a nonce built from the sequence and the
domain byte `0xA7`; `chem_auth_state_ok` recomputes and compares in constant
time (`crypto_aead_tag_equal` is a branchless XOR accumulator).
`test_chem_auth_state_tag` proves a modified record fails, and the monitor paths
prove the end-to-end denial before the siren moves.

Honest limitations: the lab derives the field key and the state-tag key from one
committed secret, so a compromised device can compute tags the gateway accepts;
the tag protects against casual tamper and a debugger that flips `granted`, not a
physical attacker who can read the key out of SRAM and recompute the tag; there
is no per-device key or rotation; and the nonce is deterministic in the sequence,
so two distinct records that ever share a sequence would violate AEAD nonce
uniqueness.

## 5. Coordinated Attack and Incident Response Audit

Act X is the coordinated-finale act, so the implant gets its own dedicated audit.
The review asks seven questions: what it does, how it forces the all clear, how it
silences the siren, how it stays underneath the authenticated path, how it
persists and beacons, how it is detected and removed, how it is bounded, and what
it does not prove.

### 5.1 What it does

`src/implant.c` is compiled only under `SANDBOX_ONLY`. The clean firmware build
does not define the guard, so the shipping image has no implant. In the
`SANDBOX_ONLY` build:

- **Sabotage marker with the real flash API.** `implant_init` reads the marker
  byte at `CHEM_IMPLANT_RESERVE_ADDR` (`0x103FF000`). On the first run the marker
  is absent, so `implant_infect` erases the sector and programs `0x58`
  (`CHEM_IMPLANT_SABOTAGE_MARKER`) with the Pico SDK flash API exactly once. This
  is a real sector erase and program: in the non-mock build the `IMPLANT_FLASH_WRITE`
  macro expands to `flash_range_erase(CHEM_IMPLANT_RESERVE_OFFSET,
  FLASH_SECTOR_SIZE)` followed by `flash_range_program(CHEM_IMPLANT_RESERVE_OFFSET,
  page, FLASH_PAGE_SIZE)` against the final 4 KiB sector of the 4 MiB flash, not a
  simulated memory-mapped store. `implant_marker_set` reports the marker by
  comparing the reserved byte to `0x58`.
- **Re-install on boot.** On every later boot the marker is present, so
  `implant_init` arms the beacon, sets `g_implant_reinstalled`, and the forced all
  clear is live again without any firmware change. A reflash of the program region
  does not touch the reserved sector.
- **The forced all clear.** While `implant_beacon_armed()` is true and
  `implant_marker_set()` is true, `monitor_sabotage` returns true.
  `monitor_effective_state` returns `CHEM_STATE_CLEAR`, `monitor_siren_target`
  returns false, `monitor_led_for` returns `CHEM_CLEAR`, and `monitor_state_text`
  returns `SAFE`. The implant never builds an envelope and never presents a key;
  it overrides the output after the authenticated decision.
- **The silenced siren.** `monitor_apply_state` calls `siren_apply_command(false,
  true)` whenever `monitor_siren_target` is false, so an authorized hazard
  command can arrive and the siren will not sound. `monitor_sync_sabotage`
  re-applies the siren whenever the sabotage state changes. The operator is told
  the store is in a routine, safe state.
- **The multi-stage beacon.** `implant_tick` advances a monotonic counter and,
  while the beacon is resident and no probe is attached, advances one stage every
  `CHEM_IMPLANT_BEACON_INTERVAL` (4) ticks and re-writes the marker. A full
  check-in cycle is `CHEM_IMPLANT_BEACON_STAGES` (3) stages.
- **The magic beacon command.** `implant_beaconize` calls `implant_token_ok`,
  which is a `memcmp` against the exact 24-byte `CHEM_IMPLANT_BEACON_MAGIC`
  (`IRON-CURTAIN-BEACON-2026`). A wrong token, a null pointer, a wrong length, or
  an attached probe leaves the terminal disarmed. `implant_disable` uses the same
  exact-match check, and on success it stands the beacon down and writes zero to
  the reserved sector.
- **Anti-debug.** `implant_debug_attached` reads CoreDebug `DHCSR` at
  `0xE000EDF0` (`CHEM_IMPLANT_DHCSR_ADDR`). Bit 0 is `C_DEBUGEN` and bit 1 is
  `C_HALT`. `implant_init`, `implant_beaconize`, `implant_disable`, and
  `implant_tick` all return early or suppress the beacon when either bit is set,
  so the marker and the forced all clear are suppressed while a probe is
  attached.

Every one of these behaviors is asserted by a native test:
`test_monitor_sabotage_lies`, `test_monitor_sabotage_restores`,
`test_implant_init_first_run`, `test_implant_reinstall_on_boot`,
`test_implant_marker`, `test_implant_debug_attached`, `test_implant_init_debug`,
`test_implant_beaconize_debug`, `test_implant_tick_advance`,
`test_implant_tick_debug`, `test_implant_tick_unarmed`,
`test_implant_disable_accepts`, `test_implant_disable_rejects`,
`test_implant_disable_debug`, and `test_implant_neutralize`. All pass in this
review.

### 5.2 How it forces the all clear, and why a green lamp is not a safe store

The implant is deliberately local and deliberately quiet. An armed, unobserved
node with the marker present renders `ST:SAFE` and lights the green CLEAR lamp,
even when the guard state is `HAZRD`. Nothing in the path opens an envelope,
presents a key, or changes a byte that an AEAD tag covers, so an integrity check
over content is blind to it. The state is the `0x58` marker in the reserved
sector and the runtime latches in SRAM, and the loop is the four-tick
re-assertion. A firmware reflash writes the program region and leaves the marker
alone, so the node comes back lying.

### 5.3 How it silences the siren

The silence is the half of the attack that makes it survivable for the attacker.
A terminal that silenced the siren and still displayed `HAZRD` would be a fault an
operator would investigate. A terminal that reports `SAFE` and lights green is a
store an operator accepts. The silence is one predicate, `monitor_sabotage`, and
it is compiled under the same `SANDBOX_ONLY` guard, so the clean build always
reports the true hazard state. The lesson is that warning failures are often
social as much as technical: the device does not only stay quiet, it explains the
quiet.

### 5.4 How it stays underneath the authenticated path

The implant is not a stealth protocol client. It never builds an envelope, never
holds a key, and never calls `control_handle_frame`. Its entire effect is a
boolean read in `monitor_sabotage`, a state rewrite in `monitor_effective_state`,
a boolean read in `monitor_siren_target`, and a string in `monitor_state_text`.
That is the architectural point: the sealed hazard path can be correct, tested,
and replay-resistant, and a local condition that changes the output is unaffected
by every one of those properties. A valid hazard command can arrive, pass every
check, and the siren will still stay silent.

### 5.5 How it persists and beacons

The persistence is the `0x58` marker in the reserved sector, written once with the
real flash API and re-written on each due tick while the beacon is armed. The
beacon is the multi-stage check-in: a three-stage cycle every four ticks, counted
by `implant_advance_stage`, with the stage exposed by `implant_stage` and the
completed cycles by `implant_beacon_count`. The re-assertion is what makes the
payload coordinated rather than a one-shot fault: a device that forced the all
clear once and then drifted would not hold a campaign.

### 5.6 How it is detected and removed

- **By build comparison.** The clean and `SANDBOX_ONLY` images differ by the
  beacon translation unit and its symbols, which is the simplest and strongest
  detection: the payload is absent from the shipping build.
- **By reserved-sector inspection.** The marker at `0x103FF000` is state the
  firmware image does not own, and it is visible with the Debug Probe or
  `picotool`. Because it is written with the real flash API, a read of the sector
  returns the `0x58` byte on physical silicon.
- **By display mismatch.** The `M:SAB` marker field and the `ST:SAFE` state next
  to a quiet control link are the implant's fingerprint.
- **By static analysis.** The `0x58` marker, the `IRON-CURTAIN-BEACON-2026`
  command, the stage count, the tick interval, and the `DHCSR` read address are
  all literal constants in the image.
- **By controlled observation.** Because the anti-debug branch is a single early
  return, a student can break after it under GDB and observe the beacon and the
  forced all clear resume, which proves the payload rather than merely suspecting
  it.
- **By incident response.** The documented removal is a procedure, not a patch:
  cut the coordinated beacon with the command, break the boot persistence by
  clearing the marker (`implant_neutralize`), erase the reserved sector, remove
  the re-install check and the `SANDBOX_ONLY` build flag, and add a fail-safe
  policy so no future boot trusts the marker. The incident-response order matters:
  neutralization restores the warning now, and the sector erasure removes the
  ability to lie on the next boot.

### 5.7 How it is bounded

The implant is bounded by construction and by test. It touches only its own
outputs, its runtime latches, and the one reserved sector. It has no network, no
filesystem, and no host impact. Its only physical effect is on the mock siren
servo and the mock LCD readout. It never reads the field key, never opens the
sealed path, and never writes anywhere except the reserved sector on the same
chip. The `SANDBOX_ONLY` guard is the containment boundary, the reserved sector
holds nothing else, and the native implant tests assert both the behavior and its
limits.

### 5.8 What it does not prove, and the honest limitation

The implant is a **benign educational payload**. It is confined to the
breadboard, guarded by `SANDBOX_ONLY`, and has no network. **The implant affects
only the mock siren servo and the mock LCD readout.** No person is in the store
and no evacuation is delayed; the store temperature is synthetic and the siren is
a servo. **It holds no real hazard.** The sabotage marker is a real sector erase
and program, but it is a single byte in a reserved sector that holds nothing else.
There is no external address, no internet path, no remote server, and no
command-and-control endpoint. The magic command is a literal constant, the beacon
is a counter, and the forced all clear is one predicate. **No external network
exists** anywhere in this project. It is a demonstration of technique, not
tradecraft: it does not encrypt anything, it does not randomize its command, it
does not survive a deliberate sector erase, and it does not resist physical
forensics. Any claim that this module is operationally representative of a real
coordinated campaign or a real cyber-physical attack would be an overclaim, and
this review records that plainly.

The deeper honest limitation is architectural and does not go away with a cleaner
implementation: a local condition that overrides an authorized output or forces a
false all clear is not a wire-authentication problem, and no amount of sealing
the command path fixes it. Mitigating it is an authorization-boundary, policy,
state-erasure, and debug-lockdown control, which is why the blue half names those
controls rather than pretending the protocol covers them.

## 6. Artifact Verification

This project ships no CTF firmware artifact (`build/` holds only untracked local
test binaries). The companion CTF is external:
`https://github.com/mytechnotalent/CTF_chemical-warning-terminal`, which ships the
compromised image with the coordinated beacon and its verifier. What is verified
in this repository is the source tree and the provisioning artifact.

Source-tree aggregate SHA-256 over all 44 `.c` and `.h` files under `src/` and
`include/`, computed as `find src include \( -name '*.c' -o -name '*.h' \) |
sort | xargs shasum -a 256 | shasum -a 256`:

```
30f90853723025fdf07da08a5e1486714663cf059c8bd60655d80c88964db632
```

Key artifacts by SHA-256:

```
paper.pdf                      4173118a7c7aea6f67fec12c331ac2b9a9364f0b79acda73352e02b0cec9ad95
paper.typ                      13c8998a07911b02c4f803f65e9a9a3081aa285e9fa628aadef3e9b559791af4
chemical-warning-terminal.png  bf49d5bdee5ea48c86111882708e69e4daf7e7ba9760aecb1b6b94b683ce5257
scripts/packet_artifact.json   54795bfb661bca308a6ce945524750b9575770da02550ac7de3b2e46b23bf7d1
include/packet_artifact.h      85ba576cae06f7e3104588a46f303c8bd956d266f2a509285c7b628e58d6acd0
include/field_secrets.h        63cffbbeb9e4740c4031865d6bcf5bb8302ede090579eb4fbf0ef41764135d07
```

The build guardrail `check_packet_artifact_header` regenerates
`include/packet_artifact.h` from `scripts/packet_artifact.json` and fails if the
committed header is stale. Re-run for this review:

```
$ python3 scripts/gen_packet.py --from-json scripts/packet_artifact.json \
      --header-out /tmp/if_cwt.h --check-header-path include/packet_artifact.h
Wrote generated firmware header: /private/tmp/if_cwt.h
Verified header matches: .../include/packet_artifact.h
exit=0
```

Constants re-read from `include/packet_artifact.h` and matched to the README and
the pin map: `PACKET_NODE_ADDRESS` 7, `PACKET_GATEWAY_ADDRESS` 0x0001,
`PACKET_FRAME_SIZE` 48, `PACKET_LINK_WAIT_MS` 5000,
`PACKET_SIREN_RAISE_PULSE_US` 1500, `PACKET_SIREN_LOWER_PULSE_US` 500,
`PACKET_DHT_TIMEOUT_US` 240, `PACKET_LCD_I2C_ADDRESS` 0x27,
`PACKET_MAX_RCV_LEN` 256, plus the shared pin map.

The banner is generated by `scripts/gen_banner.py` and is 1500 x 1500 pixels,
matching the other acts.

## 7. Adversarial Document Review

| document claim | audit verdict |
|---|---|
| README does not imply the device is unhackable | **accurate**; it states the hazard path is sealed, that the implant overrides the output underneath it, and that removal is a procedure rather than a single patch |
| README states the implant is benign, guarded, and confined | **accurate**; it appears in the narrative, the implant section, Lab 3, PARTS.md, and this review |
| README states the implant affects only the mock siren and LCD and holds no real hazard | **accurate**; it is stated in the narrative, the FROSTLINE Coordinated Beacon section, Lab 3, PARTS.md, and this review |
| README gives the marker, command, stage count, interval, forced all clear, and anti-debug details | **accurate**; the `0x58` marker, `IRON-CURTAIN-BEACON-2026` command and its 24-byte length, the 4-tick interval, the 3-stage cycle, `ST:SAFE`, the `DHCSR` bits, and the reserved address all match the firmware |
| README states the clean build does not define `SANDBOX_ONLY` | **accurate**; the CMake option defaults to OFF and the module is guarded |
| README "The suite has **145 cases** and **501 checks**" | **accurate**; the native runner reports exactly 145 cases and 501 checks |
| README claims 100% line coverage of owned modules | **accurate**; the report is 2123 / 2123 lines |
| README claims the sabotage marker uses the real flash API | **accurate**; the non-mock `implant_flash_write` calls `flash_range_erase` and `flash_range_program` |
| README does not mention per-device key rotation | **omission**; the paper's Threat Model is the only place that states the single-key limitation |
| README anti-replay section does not mention the reboot reset | **omission**; the paper states it, the README does not |
| README states the implant is local with no external network | **accurate**; the implant section, Lab 3, PARTS.md, and this review all state it |
| Gateway/firmware command constant | **accurate**; `gateway.py` `CHEM_COMMAND_HAZARD = 1` matches the firmware `0x01` hazard code, and `spoof.py` `CHEM_COMMAND_CLEAR = 2` matches the firmware `0x02` clear code |

Corrections: the README's anti-replay and key-model sections should carry the
same reboot-reset and no-per-device-rotation caveats the paper already carries.
No claim of unhackability was found, and there is no tooling command-constant
mismatch in this act.

## 8. Honest Limitations

- **Physical access wins.** A Debug Probe over SWD can read the field key from
  SRAM. The authenticated state tag detects a flipped verdict, but a probe that
  can read the key and recompute the tag defeats the design. Only OTP debug
  disable closes this.
- **Key extraction from flash.** `include/field_secrets.h` commits the passphrase
  and salt. Anyone holding the image holds the key. This is a lab convenience,
  not a deployment.
- **Single shared field key.** Both the wire key and the state-tag key derive
  from one committed secret, so a compromised device can compute tags the gateway
  accepts. There is no per-device key and no rotation in this build.
- **Replay after reboot.** `last_seq` resets to zero, so a command captured
  before a power cycle can be replayed after it. The floor is not persisted.
- **Classroom crypto profile.** Argon2id runs at `t=3 p=1 m=64` to fit SRAM; the
  state-tag nonce is deterministic in the sequence; both are teaching parameters,
  not hardening parameters.
- **All effects are confined to the breadboard.** The implant affects only a mock
  siren and a mock LCD. No person is in the store and no evacuation is delayed.
  This is a hard scope limit, not an implementation detail.
- **The implant holds no real hazard.** The sabotage marker is a single byte in a
  reserved sector on the same chip that holds nothing else. There is no asset to
  seize and no target to strike.
- **The magic command is a literal constant.** It is a filter, not a key. It is
  legible in the image and it is not randomized or derived.
- **The implant is inert, guarded, and breadth-limited.** It is benign,
  breadboard-bound, `SANDBOX_ONLY`-guarded, networkless, and confined to a
  reserved sector on the same chip. Its persistence is persistence against a
  firmware reflash, not against a deliberate sector erase or physical forensics.
  It demonstrates technique, not tradecraft.
- **The implant bypasses the protocol.** A local condition that overrides the
  output is an authorization-boundary, policy, and debug-lockdown problem, not a
  wire-authentication problem. Policy, gating, and debug lockdown are named as
  the real controls.
- **The forced all clear is the attack.** A local predicate that reports the
  store clear is a warning-integrity failure; no amount of wire authentication
  removes it.
- **Anti-debug detectability is not taught to deployment depth.** The `DHCSR`
  check is deliberately simple; hardening against a determined analyst is out of
  scope.
- **Unauthenticated optical input.** Any NEC remote can send a manual
  acknowledge. The optical surface is a documented exposure; the sealed radio
  path is the authorization path.
- **Manual acknowledge is a single input.** It is debounced and it never
  bypasses authorization, but it is one button; a failed button or a stuck line
  is a hardware reliability problem outside the firmware's control.
- **Supply chain and sensor trust are out of scope.** The DHT11 is checksummed,
  not authenticated, and the firmware is only as trustworthy as the toolchain and
  the parts.
- **Warning integrity is not protected by authentication.** An attacker on the
  band can jam or flood the receiver, and a local override can ignore a valid
  command or force a false all clear.
- **Coverage is line coverage.** Branch coverage is not 100%, and the harness
  mocks are not the real silicon.

## 9. Conclusion

The project is internally consistent and candid: 20 owned modules, 2123
instrumented lines, 100.00% line coverage, 501 native checks passing with 0
failures, 145 native cases, and 17 passing Python tests, every cryptographic
primitive anchored to a published vector. The six gates all pass with exit 0.
Act X combines every prior technique into one coordinated finale over Acts I to
IX: a three-stage beacon that checks in every four ticks, a boot persistence that
re-installs from the reserved sector, an exact-match `IRON-CURTAIN-BEACON-2026`
magic command, and a reserved-sector `0x58` sabotage marker written with the real
Pico SDK flash API that survives a firmware reflash. While the marker is present
the terminal forces a false all clear, silences the siren, and lights the green
lamp, so it lies about a chemical hazard. It keeps the sealed and guarded hazard
command path, the strictly monotonic anti-replay window, and the keyed tag over
the authorization record, all exercised end to end, and it adds a manual
acknowledge request that asks for authorization instead of bypassing it plus a
fail-safe policy that raises the hazard siren on a lost link. Every implant
behavior is asserted by a native test and every limit is stated, including the
two that matter most: the implant affects only the mock siren and the mock LCD,
and it holds no real hazard, with all effects confined to the breadboard. The
documentation is unusually honest about the shared key, the open debug port, the
inert payload, the mock outputs, and the no-real-hazard scope, with minor
omissions (reboot reset and no per-device rotation) that should be folded into
the README. The core lesson holds and is stated: the wire is sealed, the verdict
is tagged, the acknowledge cannot bypass, and the remaining risk is the key, the
probe, the local override, and the quiet of a terminal that has decided to lie.

---

*This review is reproducible: run the six commands in section 2, the header
check in section 6, and the Python suites in section 4.*

This is Act X of the ten-act OPERATION COLD IRON saga. See SAGA.md.
