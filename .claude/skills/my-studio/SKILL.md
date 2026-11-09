---
name: my-studio
description: Use whenever the user sends a video to edit, gives a note on an edit, or approves a video. Edits with the brand-nat-styles skill (105 styles) and lets the user's saved preferences in MY-STYLE.md and NOTES.md guide every choice.
---

# My Studio

The user's personal video editing studio, built on top of the 105 styles skill at `../brand-nat-styles/` (read its `SKILL.md` and `styles.md`).

Two files in this folder hold the user's taste:

- `MY-STYLE.md`: their look (captions, colours, pacing) and anything they never want.
- `NOTES.md`: every note they have given, dated.

## First time: find the style

If `MY-STYLE.md` has no real preferences yet:

1. Check ffmpeg and ffprobe are set up, the way the brand-nat-styles skill does it (`ffmpeg -version`; ask before installing anything).
2. Ask for 1 to 3 video files they love, or their own videos. If they have none, help them pick styles from the 105 style guide.
3. Pull frames from those videos (`ffmpeg -i in.mp4 -vf fps=1,scale=360:-1 frames/%03d.png`, plus a contact sheet), look at them, and save what they like to `MY-STYLE.md`: caption look, colours, fonts, pacing, layout, which style codes match. Learn the style, never copy the video.
4. Never invent preferences. Only write what the user said or what you saw in videos they gave you.

## Every edit

1. Read `MY-STYLE.md` and `NOTES.md` first and follow them. Rules in `MY-STYLE.md` beat defaults in brand-nat-styles; brand-nat-styles house rules (never cover the face, safe zone, etc.) always stay on.
2. Never render without a source video the user asked you to edit.
3. Read both files again right before you render, so nothing gets forgotten halfway through.
4. After rendering, check the finished video against every rule in `MY-STYLE.md` and the house rules, one by one, and label each check:
   - **Measured**: measured on the actual video file (words per line, gaps, how long nothing moves, loudness, resolution, duration).
   - **Visually reviewed**: you looked at frames from the actual video.
   - **Unverified**: you couldn't check it on the video; only the plan or an estimate says it's fine.
   Never say a check passed if it was only based on the plan or an estimate.
5. Fix anything that fails before showing the user, then give them the list with its labels.

## Every note

1. Save it to `NOTES.md` the moment it is given (date + the note in their words), before fixing anything.
2. If they have said the same thing before, add it to `MY-STYLE.md` as a rule and tell them: "You've said this before, so it's now a rule."
3. When they approve a video, save what worked to `MY-STYLE.md` (codes used, caption look, pacing).

## Keeping it

This studio lives in a git repo. After changing `MY-STYLE.md` or `NOTES.md`, commit and push so the next chat has it.
