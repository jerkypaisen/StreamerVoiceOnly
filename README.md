# StreamerVoiceOnly

An [Oxide/uMod](https://umod.org/) plugin for **Rust** that restricts in-game voice chat so that **only players with the proper permission (e.g. streamers) can be heard**. Every other player's voice is blocked.

- **Author:** jerky
- **Version:** 1.0.0

> 🇯🇵 日本語版は [README.ja.md](README.ja.md) を参照してください。

## How it works

The plugin hooks into the `OnPlayerVoice` event. When a player transmits voice:

- If the player **has** the `streamervoiceonly.use` permission → their voice is transmitted normally.
- If the player **does not have** the permission → the voice data is blocked (other players will not hear them).

This is useful for streamer-only servers or events where you only want designated broadcasters to speak in voice chat while everyone else stays muted.

## Installation

1. Make sure your Rust server is running [Oxide/uMod](https://umod.org/).
2. Copy `StreamerVoiceOnly.cs` into your server's `oxide/plugins/` directory.
3. The plugin loads automatically (or run `oxide.reload StreamerVoiceOnly` from the server console).

## Permission

| Permission | Description |
|---|---|
| `streamervoiceonly.use` | Players who have this permission are allowed to use voice chat. |

### Granting the permission

Grant it to an individual player:

```
oxide.grant user <steamID or name> streamervoiceonly.use
```

Grant it to a whole group (e.g. a "streamer" group):

```
oxide.group add streamer
oxide.grant group streamer streamervoiceonly.use
oxide.usergroup add <steamID or name> streamer
```

### Revoking the permission

```
oxide.revoke user <steamID or name> streamervoiceonly.use
```

## Notes

- Players **without** the permission are muted server-wide — they cannot be heard by anyone.
- No configuration file is required.

## License

Provided as-is for use on your Rust server.
