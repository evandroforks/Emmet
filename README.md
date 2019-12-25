# Emmet for Sublime Text

Official [Emmet](http://emmet.io) plugin for Sublime Text.

* [How to install](#how-to-install)
* [Available actions](#available-actions)
* [Extensions support](#extensions-support)
* [Overriding keyboard shortcuts](#overriding-keyboard-shortcuts)
* [How to expand abbreviatoins with Tab key in other syntaxes](#how-to-expand-abbreviations-with-tab-in-other-syntaxes)
* [Notes about Tab key handler](#tab-key-handler)

## How to install

*Warning:* this plugin may not work at all in some OSes since it written in JavaScript and uses [PyV8](http://code.google.com/p/pyv8/) and [Google V8](https://developers.google.com/v8/) binaries to run. If you experience problems or editor crashes please [fill an issue](https://github.com/sergeche/emmet-sublime/issues).

### By Package Control

1. Download & Install **`Sublime Text 3`** (https://www.sublimetext.com/3)
1. Go to the menu **`Tools -> Install Package Control`**, then,
   wait few seconds until the installation finishes up
1. Now,
   Go to the menu **`Preferences -> Package Control`**
1. Type **`Add Channel`** on the opened quick panel and press <kbd>Enter</kbd>
1. Then,
   input the following address and press <kbd>Enter</kbd>
   ```
   https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json
   ```
1. Go to the menu **`Tools -> Command Palette...
   (Ctrl+Shift+P)`**
1. Type **`Preferences:
   Package Control Settings – User`** on the opened quick panel and press <kbd>Enter</kbd>
1. Then,
   find the following setting on your **`Package Control.sublime-settings`** file:
   ```js
       "channels":
       [
           "https://packagecontrol.io/channel_v3.json",
           "https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json",
       ],
   ```
1. And,
   change it to the following, i.e.,
   put the **`https://raw.githubusercontent...`** line as first:
   ```js
       "channels":
       [
           "https://raw.githubusercontent.com/evandrocoan/StudioChannel/master/channel.json",
           "https://packagecontrol.io/channel_v3.json",
       ],
   ```
   * The **`https://raw.githubusercontent...`** line must to be added before the **`https://packagecontrol.io...`** one, otherwise,
     you will not install this forked version of the package,
     but the original available on the Package Control default channel **`https://packagecontrol.io...`**
1. Now,
   go to the menu **`Preferences -> Package Control`**
1. Type **`Install Package`** on the opened quick panel and press <kbd>Enter</kbd>
1. Then,
search for **`Emmet`** and press <kbd>Enter</kbd>

See also:

1. [ITE - Integrated Toolset Environment](https://github.com/evandrocoan/ITE)
1. [Package control docs](https://packagecontrol.io/docs/usage) for details.


--------------

**WARNING**: When plugin is installed, it will automatically download required PyV8 binary so you have to wait a bit (see _Loading PyV8 binary_ message on status bar). If you experience issues with automatic PyV8 loader, try to [install it manually](https://github.com/emmetio/pyv8-binaries).

## Available actions ##

* [Expand Abbreviation](http://docs.emmet.io/actions/expand-abbreviation/) – <kbd>Tab</kbd> or <kbd>Ctrl+E</kbd>
* Interactive “Expand Abbreviation” — <kbd>Ctrl+Alt+Enter</kbd>
* [Match Tag Pair Outward](http://docs.emmet.io/actions/match-pair/) – <kbd>⌃D</kbd> (Mac) / <kbd>Ctrl+,</kbd> (PC)
* [Match Tag Pair Inward](http://docs.emmet.io/actions/match-pair/) – <kbd>⌃J</kbd> / <kbd>Shift+Ctrl+0</kbd>
* [Go to Matching Pair](http://docs.emmet.io/actions/go-to-pair/) – <kbd>⇧⌃T</kbd> / <kbd>Ctrl+Alt+J</kbd>
* [Wrap With Abbreviation](http://docs.emmet.io/actions/wrap-with-abbreviation/) — <kbd>⌃W</kbd> / <kbd>Shift+Ctrl+G</kbd>
* [Go to Edit Point](http://docs.emmet.io/actions/go-to-edit-point/) — <kbd>Ctrl+Alt+→</kbd> or <kbd>Ctrl+Alt+←</kbd>
* [Select Item](http://docs.emmet.io/actions/select-item/) – <kbd>⇧⌘.</kbd> or <kbd>⇧⌘,</kbd> / <kbd>Shift+Ctrl+.</kbd> or <kbd>Shift+Ctrl+,</kbd>
* [Toggle Comment](http://docs.emmet.io/actions/toggle-comment/) — <kbd>⇧⌥/</kbd> / <kbd>Shift+Ctrl+/</kbd>
* [Split/Join Tag](http://docs.emmet.io/actions/split-join-tag/) — <kbd>⇧⌘'</kbd> / <kbd>Shift+Ctrl+`</kbd>
* [Remove Tag](http://docs.emmet.io/actions/remove-tag/) – <kbd>⌘'</kbd> / <kbd>Shift+Ctrl+;</kbd>
* [Update Image Size](http://docs.emmet.io/actions/update-image-size/) — <kbd>⇧⌃I</kbd> / <kbd>Ctrl+U</kbd>
* [Evaluate Math Expression](http://docs.emmet.io/actions/evaluate-math/) — <kbd>⇧⌘Y</kbd> / <kbd>Shift+Ctrl+Y</kbd>
* [Reflect CSS Value](http://docs.emmet.io/actions/reflect-css-value/) – <kbd>⇧⌘R</kbd> / <kbd>Shift+Ctrl+R</kbd>
* [Encode/Decode Image to data:URL](http://docs.emmet.io/actions/base64/) – <kbd>⇧⌃D</kbd> / <kbd>Ctrl+'</kbd>
* Rename Tag – <kbd>⇧⌘K</kbd> / <kbd>Shift+Ctrl+'</kbd>

[Increment/Decrement Number](http://docs.emmet.io/actions/inc-dec-number/) actions:

* Increment by 1: <kbd>Ctrl+↑</kbd>
* Decrement by 1: <kbd>Ctrl+↓</kbd>
* Increment by 0.1: <kbd>Alt+↑</kbd>
* Decrement by 0.1: <kbd>Alt+↓</kbd>
* Increment by 10: <kbd>⌥⌘↑</kbd> / <kbd>Shift+Alt+↑</kbd>
* Decrement by 10: <kbd>⌥⌘↓</kbd> / <kbd>Shift+Alt+↓</kbd>

## Extensions support ##

You can easily [extend](http://docs.emmet.io/customization/) Emmet with new actions and filters or customize existing ones. In `Emmet.sublime-settings`, define `extensions_path` setting and Emmet will load all `.js` and `.json` files in specified folder at startup.

The default value of `extensions_path` is `~/emmet`, which points to _emmet_ folder inside your OS user’s home folder.

Also, you can create sections named as extension files (e.g. `snippets`, `preferences` and `syntaxProfiles`) inside user’s `Emmet.sublime-settings` file and write your customizations there. See [original settings file](https://github.com/sergeche/emmet-sublime/blob/master/Emmet.sublime-settings#L61) for examples.

## Overriding keyboard shortcuts ##

Sublime Text is a great text editor with lots of features and actions. Most of these actions are bound to keyboard shortcuts so it’s nearly impossible to provide convenient plugin shortcuts for third-party plugins.

If you’re unhappy with default keymap, you can disable individual keyboard shortcuts with `disabled_keymap_actions` preference of `Emmet.sublime-settings` file.

Use a comma-separated list of action names which default keyboard shortcuts should be disabled. For example, if you want to release <kbd>Ctrl+E</kbd> (“Expand Abbreviation”) and <kbd>Ctrl+U</kbd> (“Update Image Size”) shortcuts, your must set the following value:

    "disabled_keymap_actions": "expand_abbreviation, update_image_size"

You should refer `Default (Your-OS-Name).sublime-keymap` file to get action ids (look for `args/action` key).

To disable all default shortcuts, set value to `all`:

    "disabled_keymap_actions": "all"

Not that if you disabled any action like so and you’re create your own keyboard shortcut, you **should not** use `emmet_action_enabled.ACTION_NAME` context since this is the key that disables action.

## How to expand abbreviations with Tab in other syntaxes

Emmet expands abbreviations in limited syntaxes only: HTML, CSS, LESS, SCSS, Stylus and PostCSS. The reason to restrict Tab handler to a limited syntax list is because it breaks native Sublime Text snippets.

If you want to abbreviation with Tab in other syntaxes (for example, JSX, HAML etc.) you have to tweak your [keyboard shorcuts settings](http://sublime-text-unofficial-documentation.readthedocs.org/en/sublime-text-2/reference/key_bindings.html): add `expand_abbreviation_by_tab` command for `tab` key for required syntax *scope selectors*. To get current syntax scope selector, press <kbd>⇧⌃P</kbd> (OSX) or <kbd>Ctrl+Alt+Shift+P</kbd>, it will be displayed in editor status bar.

Go to `Preferences` > `Key Bindings — User` and insert the following JSON snippet with properly configured scope selector instead of `SCOPE_SELECTOR` token:

```js
{
  "keys": ["tab"],
  "command": "expand_abbreviation_by_tab",

  // put comma-separated syntax selectors for which
  // you want to expandEmmet abbreviations into "operand" key
  // instead of SCOPE_SELECTOR.
  // Examples: source.js, text.html - source
  "context": [
    {
      "operand": "SCOPE_SELECTOR",
      "operator": "equal",
      "match_all": true,
      "key": "selector"
    },

    // run only if there's no selected text
    {
      "match_all": true,
      "key": "selection_empty"
    },

    // don't work if there are active tabstops
    {
      "operator": "equal",
      "operand": false,
      "match_all": true,
      "key": "has_next_field"
    },

    // don't work if completion popup is visible and you
    // want to insert completion with Tab. If you want to
    // expand Emmet with Tab even if popup is visible --
    // remove this section
    {
      "operand": false,
      "operator": "equal",
      "match_all": true,
      "key": "auto_complete_visible"
    },
    {
      "match_all": true,
      "key": "is_abbreviation"
    }
  ]
}
```

### Tab key handler ###

Emmet plugin allows you to expand abbreviations with <kbd>Tab</kbd> key, just like regular snippets. On the other hand, due to dynamic nature and extensive syntax, sometimes you may get unexpected results. This section describes how Tab handler works and how you can fine-tune it.

By default, Tab handler works in a limited _syntax scopes_: HTML, XML, HAML, CSS, SASS/SCSS, LESS, PostCSS and _strings in programming languages_ (like JavaScript, Python, Ruby etc.). It means:

* You have to switch your document to one of the syntaxes listed above to expand abbreviations by Tab key.
* With <kbd>Ctrl-E</kbd> shortcut, you can expand abbreviations everywhere, its scope is not limited.
* When you expand abbreviation inside strings of programming languages, the output is generated with special [output profile](http://docs.emmet.io/customization/syntax-profiles/) named `line` that generates output as a single line.

To fine-tune Tab key handler, you can use the following settings in user’s `Emmet.sublime-settings` file:

* `disable_tab_abbreviations_for_scopes` — a comma-separated list of syntax scopes where Tab key handler should be disabled. For example, if you want disable handler inside strings of programming languages and HAML syntax, your setting will look like this:

```json
"disable_tab_abbreviations_for_scopes": "text.haml, string"
```

* `disabled_single_snippet_for_scopes` — a comma-separated list of syntax scopes where Tab handler should be disabled when expanding a single abbreviation. Currently, ST doesn’t provide API for getting list of native snippets. So, for example, if you try to expand a `php` abbreviation, it will be passed to Emmet which outputs `<php></php>` instead of PHP block as defined in native ST snippets. As a workaround, if you’re trying to expand a single abbreviation inside scope defined in `disabled_single_snippet_for_scopes` setting Emmet will look for its name inside its own [snippets catalog](http://docs.emmet.io/cheat-sheet/) first, inside `known_html_tags` setting second and if it’s not found, it allows ST to handle it and expand native abbreviation, if matched.
* `known_html_tags` — a space-separated list of all known HTML tags used for lookup as described above.

If you’re unhappy with Emmet tab handler behavior, you can disable it: just add `"disable_tab_abbreviations": true` into user’s `Preferences.sublime-settings` file.

## Disable automatic vendor prefixes insertion
If your workflow already includes an automated task for CSS vendor prefixing (such as [Autoprefixer](https://github.com/postcss/autoprefixer)), you can disable Emmet's automatic vendor prefixes insertion adding this option to your user’s `Emmet.sublime-settings` file:
```json
{
  "preferences": {
    "css.autoInsertVendorPrefixes": false
  }
}
```
