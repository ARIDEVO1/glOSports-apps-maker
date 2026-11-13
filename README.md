# glOSsports-apps-maker skill

A skill that helps build, package and test apps and games for the **goodluckOS** handheld (GA36 / R36S clone, CodeZombie firmware) that run from the **kennel** launcher.

It produces one zip per app with this layout:

```
<app>.zip
├── ports/<app>/                              run.sh, love, lib/, <app>.love, optional assets
├── .local/share/applications/<app>.puppy     first build only
└── .local/share/icons/<app>.png              if the app has an icon
```

## What it covers

- Writing LÖVE (Lua) apps at a fixed 640x480 design, scaled to the panel
- Gamepad input (A/B/X/Y, D-pad, sticks, Start/Select) with keyboard fallback for PC testing
- Reading folders and files on the device with `io.popen` and `io.open`, and loading images from bytes
- Building the `.love` file and the zip, then testing from a terminal on the device with `run.log`
- Launcher entries (`.puppy`) and icons

## Install (Claude)

1. Download the `glOSapp maker-v4.zip` file
2. Add that folder as a skill in Claude (Settings → Capabilities → Skills, or your skills folder if you use Claude Code).
3. Start a new chat and say, for example, "make a goodluckOS app that…".

## Using it with other AI tools

Gemini, Grok and other assistants are not known to load `SKILL.md` folders the way Claude does, so you can't count on automatic triggering there. You can still use the content:

- **Paste it as instructions.** Copy the text of `SKILL.md` into the assistant's custom instructions, a project or gem, or the start of a chat. Then describe your app.
- **Keep it in context.** Attach `SKILL.md` to the chat if the tool accepts files.
- The **build steps and launcher format** work the same with any tool. Only the automatic skill loading depends on Claude.

Check each tool's current documentation for how it handles instructions or skills, since this changes often.

## Reference

The skill was written from a working desktop tester app (`glosports-desktop-test.zip`). Its input, file-access and loading patterns are the reference the skill follows. The tester's own files are not included here.

## Notes

- Paths on the device are under `/mnt/HOME` (the home folder). Don't use `/home/player`.
- The launcher uses the `[Desktop Entry]` format shown in `SKILL.md`.
- LÖVE is zlib-licensed; keep its licence text in `lib/licenses/` in each app.
