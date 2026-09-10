# Chatbox — Chat Styles CSS snippet for Obsidian

[中文](./README.md)

Turn your Obsidian into a chatflow display with nothing but CSS snippets!

Meet Chatbox — CSS written exclusively for Obsidian.

## Table of Contents

- [Style Previews](#style-previews)
  - [Basic + First Line Right](#basic--first-line-right)
  - [Basic + First Line Left](#basic--first-line-left)
  - [bbs](#bbs)
  - [pop](#pop)
  - [wechat](#wechat)
  - [qqchat](#qqchat)
  - [Linshe](#linshe)
  - [Baker](#baker)
  - [Basic + No Name + No Avatar + No Title](#basic--no-name--no-avatar--no-title)
- [Installation](#installation)
- [Recommended Plugins](#recommended-plugins)
- [Chat Generator](#chat-generator)
- [Deletable Files](#deletable-files)
- [Syntax Reference](#syntax-reference)
- [License](#License)
- [Credits](#credits)

## Style Previews

7 styles to choose from, all with super simple syntax — switch freely, with light & dark mode support.

Since everything is built on top of Obsidian's native callout system, you can use all sorts of markdown syntax inside the chat bubbles (images, italics, bold, code blocks, etc.).

Pure CSS — these styles are incredibly durable. The author has been using them for two years without a single bug, and they'll likely keep working just fine.

Currently verified working on Obsidian 1.13.7, and theoretically should continue working on future versions.

Note: The bold and italic colors for **Basic**, **bbs**, and **pop** use your Obsidian theme's accent colors. All colors can be freely customized after installing the [Style Settings](https://github.com/community-archive/obsidian-style-settings) plugin!


### Basic + First Line Right

![Basic style first line right - light mode](./Image/preview-basic-right-light.jpg)
![Basic style first line right - dark mode](./Image/preview-basic-right-dark.jpg)

### Basic + First Line Left

![Basic style first line left - light mode](./Image/preview-basic-left-light.jpg)
![Basic style first line left - dark mode](./Image/preview-basic-left-dark.jpg)

### bbs

![bbs style - light mode](./Image/preview-bbs-light.jpg)
![bbs style - dark mode](./Image/preview-bbs-dark.jpg)

### pop

![pop style - light mode](./Image/preview-pop-light.jpg)
![pop style - dark mode](./Image/preview-pop-dark.jpg)

### wechat

![wechat style - light mode](./Image/preview-wechat-light.jpg)
![wechat style - dark mode](./Image/preview-wechat-dark.jpg)

### qqchat

![qqchat style - light mode](./Image/preview-qqchat-light.jpg)
![qqchat style - dark mode](./Image/preview-qqchat-dark.jpg)

### Linshe

[What's Linshe?](https://github.com/icecranberry/galgame-with-comfyUI)

Matches the chat display style of Linshe.

![Linshe style - light mode](./Image/preview-linshe-light.jpg)
![Linshe style - dark mode](./Image/preview-linshe-dark.jpg)

### Baker

Yep, it mimics Baker from *Arknights: Endfield*.

![Baker style - light mode](./Image/preview-baker-light.jpg)
![Baker style - dark mode](./Image/preview-baker-dark.jpg)

### Basic + No Name + No Avatar + No Title

Combine a few simple attributes, and you can even achieve this look!

![Basic style with no name, avatar, or title - light mode](./Image/preview-basic-minimal-light.jpg)

## Installation

Download the zip from Releases, extract it, then:

1. Copy `chatbox.css` and `chatbox-inputbox.css` from the `Css` folder into your Obsidian CSS snippets folder (Settings → Appearance → CSS snippets → click the folder icon).

   Usually located at `.obsidian/snippets` in your vault.
   
   Then go back to Settings → Appearance → CSS snippets and enable both `chatbox` and `chatbox-inputbox`.

2. Copy the entire `Chat Generator` folder into your vault's root directory. Open the sample notes in Obsidian to verify the styles are working.


## Recommended Plugins

- [Dataview](https://github.com/blacksmithgu/obsidian-dataview)
- [Style Settings](https://github.com/community-archive/obsidian-style-settings)

After installing Dataview, you need to enable the `enable JavaScript queries` option so it supports `dataviewjs` — this is required for the Chat Generator to work.

Style Settings gives you incredibly detailed control over Chatbox!

Customize dialog width, bubble colors, background color, bold & italic text colors — almost every style can be configured individually.

## Chat Generator

A mini-app that runs directly inside Obsidian, helping you generate Chatbox-compatible chatflow text without memorizing any syntax.

It's dead simple — just pick your style and go. For details on adding character avatars, check out the [02-Chat Characters-En](./Chat%20Generator/02%20Material/Character/02-Chat%20Characters-En.md).

↑In GitHub's strict Markdown rendering this may not display correctly. Opening it in Obsidian is recommended.

The generator automatically detects your Obsidian language setting and displays the interface in Chinese or English.

Click a character avatar to open their dialog box, type text and press Enter to generate their chat line.

![Chat Generator - click avatar to chat](./Image/generator-avatar-chat.jpg)

Open the editor panel to drag-and-drop reorder, flip sides, or swap characters (click the avatar to replace).

![Chat Generator - editor drag and sort](./Image/generator-editor-edit.jpg)

Open the code panel to paste existing chat code for editing with the generator.

![Chat Generator - paste code into code panel](./Image/generator-code-paste.jpg)

You can even write dialogue directly in the code panel (no names needed):

```markdown
A Chat
Testing
Alright
Can't be bothered to think of more
Lazy author lol
```

Check `Input as Dialog` and click the import button — it'll turn into:

```markdown
> [!chatbox]+ A Chat
> - Testing
> - Alright
> - Can't be bothered to think of more
> - Lazy author lol
```

Then use the editor panel to assign characters and adjust sides.

When you're done, click the last button above the preview to generate a note in your configured folder. The default template contains variables that the generator can replace directly — you can modify the template too.

![Chat Generator - template preview and generate button](./Image/generator-template-preview.jpg)

If you just want to copy the raw code, the code preview panel at the bottom has Obsidian's native copy button.

## Deletable Files

- All sample notes under `01 Chat Notes`
- `02 Material/Character` — the character table (recommended to edit rather than delete)
- `02 Material/Icon` — all avatars (they're my OCs; feel free to delete them all if you don't need them)
- `02 Material/Template/Chat Template.md` — you can replace it with your own template (recommended to edit rather than delete, since it uses replaceable variables)

If you changed the output folder setting inside the Chat Generator, all of the above folders can be deleted too.

## Syntax Reference

You really don't need to memorize this! But it's nice to understand.

```markdown
> [!chatbox|wechat]+ Chat Title
> - ![face](https://example.com/avatar.jpg) *Name A* Some dialogue here
> + ![face](path/to/local/image.jpg) *Name B* Some dialogue here
> - ![[local-image.png|face]] *Name A* Dialogue… more dialogue? *（italic style）*
> + ![[xxx.png|face]] *Name B* Dialogue… more dialogue **bold style**!!!
> 
> Narrator line
> - ![face](https://example.com/avatar.jpg) *Name A* Dialogue
> This will be attached to A's bubble above
> - Same person, bubble only — no name or avatar
> + ![face](path/to/local/image.jpg) *Name B* Dialogue
> 
> Leave a blank line for narrator text
> 
```

Note that `-` and `+` simply indicate opposite sides — they don't fix which side is left or right. The actual orientation depends on whether you add `swap`.

```markdown
> [!chatbox|wechat-swap]+ Chat Title
> - ![face](https://example.com/avatar.jpg) *Name A* Dialogue
> + ![face](path/to/local/image.jpg) *Name B* Dialogue
> - ![[local-image.png|face]] *Name A* Dialogue… more dialogue? *（italic）*
> + ![[xxx.png|face]] *Name B* Dialogue… more dialogue **bold**!!!
```

There are 7 style values, use only one at a time: plain (nothing), bbs, pop, wechat, qqchat, linshe, baker.

```markdown
> [!chatbox|bbs]
```

There are 9 attribute flags, stackable in any combination: `notitle`, `fix`, `short`, `frame`, `noname`, `noface`, `long`, `point`, `htmltag`.

```markdown
> [!chatbox|notitle-fix-short-frame-noname-noface-long-point-htmltag]
```

| Attribute   | Effect                    |
| ----------- | ------------------------- |
| `notitle`   | Hides the chat title bar  |
| `fix`       | Fixed height (settable)   |
| `short`     | Shortens the bubble       |
| `frame`     | Adds a border             |
| `noname`    | Hides the name            |
| `noface`    | Hides the avatar          |
| `long`      | Uses maximum width regardless of setting |
| `point`     | Changes cursor to pointer on hover |
| `htmltag`   | Uses HTML tags for bold/italic etc. |

The `swap` attribute can get tricky with narrator lines — the generator is highly recommended.

When writing manually with narrator lines, there are rules to keep bubble directions correct. Narrator lines occupy one directional slot and alternate from the previous speaker. If you want a different speaker after a narrator line, the narrator must take an even number of lines. A common trick is adding an invisible `> \n> <span></span>` to adjust the count.

For example, this actually renders both A and B on the left:

```markdown
> [!chatbox]+ Chat Title
> - ![face](http://avatar.jpg) *Name A* Dialogue
> 
> Narrator text
> + ![face](http://avatar.jpg) *Name B* Dialogue
```

Only this will display them on opposite sides:

```markdown
> [!chatbox]+ Chat Title
> - ![face](http://avatar.jpg) *Name A* Dialogue
> 
> Narrator text
> 
> <span></span>
> + ![face](http://avatar.jpg) *Name B* Dialogue
```

But honestly, **you really don't need to remember any of this**. Use the **Chat Generator** and it'll handle everything automatically!

## License

- CSS code and Chat Generator scripts are open-sourced under **GPLv3**
- OC avatar artworks under `02 Material/Icon/` are copyrighted by the author and are **not** covered by the GPLv3 license

## Credits

Huge thanks to **稻米鼠 (DaoMiShu)** for their TimeLine and chat-bubble CSS code!

Chatbox is built entirely on top of those two foundations.

Also many thanks to Obsidian's native callout system, Style Settings plugin authors, and Dataview plugin authors!