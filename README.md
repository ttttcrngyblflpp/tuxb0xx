**On indefinite hiatus due to lack of specification in the exact rules
behind the timing lockouts and the weirdness around implementation when
the logical controller is not polled at the same rate as a real GC
controller is polled.**

# tuxb0xx

Emulates b0xx on keyboard for Linux by listening for evdev keyboard events and
sending input to Dolphin via pipe input.

## Summary of Rules

- [x] 2.1. (Accidental Side-B) While B is held, Mod-Y modifies left/right to be
  0.6625 rather than 0.3375.
- [ ] 2.2. (SDI Nerf) After cardinal, adjacent diagonal, block the other adjacent diagonal for 4
  frames.
- [ ] 2.3. (Pivot Tilt Nerf) After cancelling a dash with a dash in the opposite direction (must be
  executed within 15 frames), A will be disabled for 9 frames within up-tilt
  region and 4 frames within down-tilt region.
- [x] 5.1. SOCD is handled by overriding the previously-held direction.
- [x] 5.2. If one direction is released after holding opposing directions, the held
  direction will remain a no-op until it is released.
- [x] 5.3. If both left and right are held (neither up nor down is held), both
modifiers become no-ops.
- [x] 8.1. (Angled fsmash) Holding mod-X with Up or Down then inputting C-left or C-right will produce
   C-stick co-ordinates of (0.8125, 0.2875).
- [x] 10.1. Light shield is 49/140, medium shield is 94/140.
- [x] 11.1. Holding down both modifiers turns C-stick cardinals into D-pad inputs.
- [x] 5. When both modifiers are held, analog stick modifications will not apply until
   one of the modifiers is released.
- [x] Crouch/Walk Option-Select: when enabled, the A-stick diagonals in Q3/4 are modified to
      (0.7125, 0.6875).

|Modifier   |X     |Y     |Diagonal        |
|---|---|---|---|
|NULL         |1.0   |1.0   |(0.7000, 0.7000)|
|X+\[LR\]     |      |      |(0.6375, 0.3750)|
|X+C-Down     |      |      |(0.7000, 0.3625)|
|X+C-Left     |      |      |(0.7875, 0.4875)|
|X+C-Up       |      |      |(0.7000, 0.5125)|
|X+C-Right    |      |      |(0.6125, 0.5250)|
|X            |0.6625|0.5375|(0.7375, 0.3125)|
|Y+\[LR\](Q12)|      |      |(0.4750, 0.8750)|
|Y+\[LR\](Q34)|      |      |(0.5000, 0.8500)|
|Y+C-Right    |      |      |(0.6375, 0.7625)|
|Y+C-Up       |      |      |(0.5125, 0.7000)|
|Y+C-Left     |      |      |(0.4875, 0.7875)|
|Y+C-Down     |      |      |(0.3625, 0.7000)|
|Y            |0.3375|0.7375|(0.3125, 0.7375)|
|C-stick      |1.0000|1.0000|(0.5250, 0.8500)|

## Known Bugs

- [x] It seems impossible to have the analog stick co-ordinates perfect due to the way dolphin maps
  a uinput device's inputs to a gamecube controller's raw input values.
