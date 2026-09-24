---
title: Templates
source: https://obsidian.md/help/plugins/templates
author:
published:
created: 2026-08-14
description: Templates - Obsidian Help
---
Templates is a [core plugin](https://obsidian.md/help/plugins) that lets you insert pre-defined snippets of text into your active note.

## Set your template folder

1. In the bottom-left corner, select **[Settings](https://obsidian.md/help/settings)** .
2. Under **Core plugins → Templates → Template folder location**, enter the folder containing your templates.

## Template variables

You can add dynamic information to your templates, using *template variables*. When you insert a template containing a template variable, Templates replaces it with its corresponding value.

| Variable | Description |
| --- | --- |
| `{{title}}` | Title of the active note. |
| `{{date}}` | Today's date. **Default format:** `YYYY-MM-DD`. |
| `{{time}}` | Current time. **Default format:** `HH:mm`. |

Both `{{date}}` and `{{time}}` allow you to change the default format using a *format string*.

To set a format string, add a colon (`:`) followed by a string of [Moment.js format tokens](https://momentjs.com/docs/#/displaying/format/), for example `{{date:YYYY-MM-DD}}`.

You can use `{{date}}` and `{{time}}` with format strings in the same way, for example `{{time:YYYY-MM-DD}}`.

You can change the default date and time formats under **[Settings](https://obsidian.md/help/settings) → Core plugins → Templates → Date format** and **[Settings](https://obsidian.md/help/settings) → Core plugins → Templates → Time format**.

> [!tip]- Use date and time variables in other plugins
> You can also use the `{{date}}` and `{{time}}` template variables in the [Daily notes](https://obsidian.md/help/plugins/daily-notes) and [Unique note creator](https://obsidian.md/help/plugins/unique-note) plugins.

## Create a template

In the [template folder](https://obsidian.md/help/plugins/templates#Set%20your%20template%20folder), [create a note](https://obsidian.md/help/manage-notes#Create%20a%20new%20note) containing the text you want to appear when you use the template. You can use [template variables](https://obsidian.md/help/plugins/templates#Template%20variables) for dynamic text like the current date.

For example, here's a template for study notes:

```markdown
---
topic: 
date: "{{date}}"
course: 
tags:
  - studies
---

# {{title}}

## Key Concepts

## Important Details

## Examples

## Questions
- 

## Summary

## Related Topics
- [[]]
```

> [!warning]+ Edit templates in Source mode
> In [Live Preview](https://obsidian.md/help/edit-and-read#Live%20Preview), the **Properties in document** panel can overwrite template variables that do not have quotation marks.
> 
> To avoid this, edit templates in [Source mode](https://obsidian.md/help/edit-and-read#Source%20mode), or set **[Settings](https://obsidian.md/help/settings) → Editor → [Properties in document](https://obsidian.md/help/settings#Properties%20in%20document)** to **Source**.

## Insert a template into the active note

> [!todo] Set your template folder before inserting a template.
> 

1. In the ribbon, select **Insert template**.
2. Select the template to insert at the cursor position in the active note.

To insert a template using the [Command palette](https://obsidian.md/help/plugins/command-palette) or [a custom keyboard shortcut](https://obsidian.md/help/hotkeys#Set%20a%20hotkey), use the command `Templates: Insert template`.

The content of the template is inserted at your current cursor position. If your cursor is not in the note body, the content is inserted at your last cursor position.

### Template properties

When you insert a template into the active note, all the properties from the template will be added to the note. Obsidian will also merge any properties that exist in your note with properties in the template.

## Insert current date and time into the active note

Use the commands `Templates: Insert current date` and `Templates: Insert current time` to insert the current date and time at your current cursor position. Like the `Insert template` command, you can also perform these with the Command palette or a custom keyboard shortcut.

The inserted date and time uses the [formatting set in the plugin settings](https://obsidian.md/help/plugins/templates#^template-settings-date-time-formatting).