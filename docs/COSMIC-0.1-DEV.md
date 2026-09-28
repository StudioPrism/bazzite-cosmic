# Bazzite COSMIC — 0.1-dev

This branch is the first bring-up of a COSMIC desktop variant of Bazzite Deck.

## 0.1 goal

The goal is deliberately narrow:

1. Preserve the existing Bazzite Deck / Gamescope gaming session.
2. Install Fedora's native `cosmic-session`.
3. Point Desktop Mode at `cosmic.desktop`.
4. Keep KDE Plasma and SDDM installed as a known-good fallback.
5. Make failure recoverable from a TTY or a previous bootc deployment.

This is **not** the phase where Plasma is removed.

## Expected session flow

```text
Boot
  -> Gamescope / Steam Game Mode
      -> Switch to Desktop
          -> COSMIC
              -> Return to Game Mode
```

Plasma remains installed for recovery and comparison.

## TTY recovery

If COSMIC fails to start or leaves a black screen:

1. Press `Ctrl+Alt+F3`.
2. Sign in with your normal user.
3. Check the image/session state:

   ```bash
   cosmic-deck-recovery status
   ```

4. Launch Plasma directly:

   ```bash
   cosmic-deck-recovery plasma
   ```

You can also test COSMIC directly from the TTY:

```bash
cosmic-deck-recovery cosmic
```

To request Bazzite Game Mode:

```bash
cosmic-deck-recovery game
```

## Deployment rollback

Before testing on important hardware, keep the previous Bazzite deployment available.

Inspect deployments with:

```bash
bootc status
```

If 0.1-dev is not usable, boot the previous deployment from the bootloader or use the normal bootc/rpm-ostree rollback workflow appropriate to the installed Bazzite version.

## 0.1 acceptance checklist

- [ ] Image builds and passes `bootc container lint`.
- [ ] `cosmic.desktop` is present.
- [ ] `plasma.desktop` remains present.
- [ ] `start-cosmic` is present.
- [ ] `startplasma-wayland` remains present.
- [ ] Game Mode boots normally.
- [ ] Switch to Desktop opens COSMIC.
- [ ] Wi-Fi works in COSMIC.
- [ ] Bluetooth works in COSMIC.
- [ ] PipeWire audio works in COSMIC.
- [ ] Flatpak applications launch from COSMIC.
- [ ] Suspend/resume works.
- [ ] Controller input remains functional after returning to Game Mode.
- [ ] Return to Game Mode works from COSMIC.
- [ ] Plasma recovery works from TTY.
- [ ] Game -> COSMIC -> Game can be repeated ten times without a forced reboot.

## Non-goals for 0.1

- Removing KDE/Plasma.
- Replacing SDDM with COSMIC Greeter.
- NVIDIA-specific optimization.
- Custom COSMIC Settings pages.
- Custom handheld/touch layout.
- Final branding.

Those come after basic session switching is reliable.
