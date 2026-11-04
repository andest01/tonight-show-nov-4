# tonight-show-nov-4

The hosted script for the Tonight Show texts gag. The board reads `script.json` from this repo; editing the file here changes what the board shows. It is the same file as `client/src/services/tonightShow/script.json` in the hitboard repo, which the board also ships as its built-in fallback.

## How the board reads it
1. GitHub's contents API for `script.json` on `main` (cached about 1 minute).
2. If that fails: `raw.githubusercontent.com` (cached up to 5 minutes, and a query string does not get around that).
3. If both fail, the last good copy the browser saved, then the script built into the board.

After a commit, wait up to about a minute, then press `R` on the board to pull it. Only press `R` between beats.

## `script.json`
```json
{
  "options": { "bubble": "blue", "sound": false, "typeSpeedMs": 55, "scale": 1, "width": 760, "avatarUrl": "" },
  "rows": [ { "row": 0, "direction": "in", "from": "Name", "text": "...", "clear": true, "typing": false, "typed": false, "note": "" } ]
}
```

| Field | Meaning |
|---|---|
| `direction` | `in` = a text arrives, `out` = the presenter sends one |
| `from` | the contact name shown on the banner |
| `text` | the message; `...` is the typing dots |
| `clear` | `true` wipes the thread and shows only this message; `false` continues under the previous ones |
| `typing` | `true` exactly when `text` is `...` |
| `typed` | `out` rows only: type it into the compose field before it sends |
| `note` | for the operator, never shown |
| `imageUrl` (optional) | a photo bubble; `text` is then `""` |
| `bubble` (optional) | `blue` or `green`, overrides the default for that row |

`options.avatarUrl` is the contact photo: empty for the grey silhouette, or an `https://` URL.

Easiest way to produce a valid file is the script builder in the hitboard repo (`tools/tonight-show-script-builder`): edit or paste the rows, then export `script.json` and commit it here.

## Notes
- This repo is public. Anything committed here can be read by anyone before it airs.
- Whoever can push to this repo controls what the board shows.
