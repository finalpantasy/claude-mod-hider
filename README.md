# hide-mods

One button above the prompt in Claude Code that hides or shows everything mods draw there. The button itself always stays, and your choice is remembered across sessions.

Handy when the window is narrow and the mod bands push the prompt up.

## Install

```
/plugin marketplace add finalpantasy/hide-mods
/plugin install hide-mods@hide-mods
```

Restart Claude Code. Click **Hide mods** (top right, above the prompt) or type `/hide-mods`. Click **Show mods** or type `/hide-mods` again to bring them back.

## How it works

While hidden, hide-mods draws only its button and does not hand the band on, so every mod drawn beneath it in the chain disappears. Claude Code does not document the order mods draw in, so a mod drawn above hide-mods can still show. To make your own mod hide reliably, read the switch and pass while it is on:

```tsx
const modsHidden = atom({ plugin: 'hide-mods', key: 'hidden' } as const, false)

on('ui.render', { component: 'AbovePrompt' }, async ($, e, next) => {
  if (e.props.hasSurvey || (await read($, modsHidden))) return next(e)
  // ...draw as usual
})
```

and declare it in your mod's type contract, inside `interface PluginState`:

```ts
'hide-mods': { hidden: boolean }
```

A survey always gets the band, hidden or not.

## License

MIT
