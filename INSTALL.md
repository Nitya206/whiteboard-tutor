# Installing Whiteboard Tutor (instructions for Claude)

The person who sent you here wants their own copy of Whiteboard Tutor as a claude.ai artifact in their account. Do exactly this.

## 1. Publish the page

Publish `index.html` from this repository as a **new artifact** in their account.

- Title: `Whiteboard Tutor`
- Icon: `Edit`
- It is one self-contained HTML file (about 1.9 MB) with every library inside it. Publish it from the file as it is. Do not rewrite, split, minify or retype it. If your tool takes a file path, give it the path, so the file's contents never pass through you.

## 2. Turn on its capabilities

Declare this for the new artifact:

```json
{"sample": {"images": true}, "tts": {}, "dictation": {}, "downloads": {}, "db": {}, "user": {}}
```

- `sample`: the tutor itself (Claude writes each slide). Required.
- `tts`: Claude's voice reading the slides.
- `dictation`: speaking answers instead of typing.
- `downloads`: saving a slide as a picture.
- `db` and `user`: sync. Lessons and settings follow the person across their devices. The app stores them under `data/users/<their id>/`, which the platform keeps private to that person, even from the artifact's owner. Declare `db` with no rules.

**If the declaration is rejected because a capability is unknown or unavailable** (for example `unknown capability: tts`), declare it again without that one, and keep the rest. If `db` or `user` is the one rejected, drop both, since sync needs the pair. Every capability except `sample` is optional: without `tts` the app runs as read-along cards, and without `db` and `user` it keeps lessons in this browser only. Never substitute another voice or text-to-speech engine.

## 3. Hand it over

Give them the artifact's link and tell them:

- Open it, type a topic, press **Start this topic**, and accept the permission prompts the first time.
- If `tts` was declared: the voice plays in a desktop browser such as Chrome or Edge. In Safari or the Claude mobile apps there is no voice, and the app switches to read-along cards on its own.
- If `tts` was rejected: say plainly that their account doesn't have Claude's voice yet, so this copy runs as read-along cards. If their account gets the voice later, asking Claude to add the `tts` capability to this artifact turns it on.
- If `db` and `user` were declared: their lessons sync across their devices through their Claude account, privately. If not: lessons stay in this browser only.

If a step fails for any other reason, say which step and the exact error.
