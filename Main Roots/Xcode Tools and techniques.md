Shortcuts

  

  

  

## **Code Completion (**`**⌃ + Space**`**)**

  

It’s hard to imagine working without code completion - I use it all of the time to explore APIs, and to save time when typing.

## **Moving Lines (**`**⌥ + ⌘ + [**` **and** `**⌥ + ⌘ + ]**`**)**

Moving single lines or entire blocks around in your code is immensely useful, for example when organising code that belongs together. Xcode automatically takes care of indentation o/

  

## **Delete Entire Line (**`**⌘ + D**`**)**

I often need to delete an entire line - Xcode offers an editor command for this, but unfortunately it is not bound to a key combo in the default key bindings. After some consideration I decided to make an exception and include a custom key combo in this list, just because I think it is so useful. To define custom keybindings, go to Xcode settings (press ⌘ + ,), navigate to the _Key Bindings_ tab, and use the filter field to search for “Delete Line”. Double click into the _Key_ field, then press your preferred key combo. I use `⌘ + D` (for **D**elete Line).

  

## **Balance Indentation (**`**⌃ + I**`**)**

Just like many of the other commands above, this works both on single lines and on entire blocks of code. Useful after pasting code from elsewhere (did somebody say Stack Overflow?).

  

## **Going Back and Forth (**`**⌃ + ⌘ + ←**` **and** `**⌃ + ⌘ + →**`**)**

Xcode tracks your entire movement history as soon as you open or create a project. Any file you go to, any symbol you look up - it all is appended to the IDE’s navigation stack. Use `⌃ + ⌘ + ←` and `⌃ + ⌘ + →` to go back and forth between the source code locations you visited.

  

## **Find Call Hierarchy (**`**⇧ + ⌃ + ⌘ + H**`**)**

  

  

Similar to _Find selected symbol in workspace_, but with a focus on methods, this shortcut will open the _Call Hierarchy_ view to show any places in your code that call the specified method, as well as any methods that call those methods in turn, and so on.

  

  

### Retaining Existing Values

To append rather than replace existing definitions, use the `$(inherited)` variable like so:

```Plain
BUILD_SETTING_NAME = $(inherited)additional value
```

You typically do this to build up lists of values, such as the paths in which the compiler searches for frameworks to find included header files (`FRAMEWORK_SEARCH_PATHS`):

```Plain
FRAMEWORK_SEARCH_PATHS = $(inherited) $(PROJECT_DIR)
```

Xcode assigns inherited values in the following order (from lowest to highest precedence):

- Platform Defaults
- Xcode Project xcconfig File
- Xcode Project File Build Settings
- Target xcconfig File
- Target Build Settings

Spaces are used to delimit items in string and path lists. To specify an item containing whitespace, you must enclose it with quotation marks (`"`).

  

### Referencing Values

You can substitute values from other settings by their declaration name with the following syntax:

```Plain
BUILD_SETTING_NAME = $(ANOTHER_BUILD_SETTING_NAME)
```

Substitutions can be used to define new variables according to existing values, or inline to build up new values dynamically.

```Plain
OBJROOT = $(SYMROOT)
CONFIGURATION_BUILD_DIR = $(BUILD_DIR)/$(CONFIGURATION)-$(PLATFORM_NAME)
```

### Setting Fallback Values for Referenced Build Settings

In Xcode 11.4 and later, you can use the `default` evaluation operator to specify a fallback value to use if the referenced build setting evaluates as empty.

```Plain
$(BUILD_SETTING_NAME:default=value)
```

### Conditionalizing Build Settings

You can conditionalize build settings according to their SDK (`sdk`), architecture (`arch`), and / or configuration (`config`) according to the following syntax:

```Plain
BUILD_SETTING_NAME[sdk=sdk] =value for specified sdkBUILD_SETTING_NAME[arch=architecture] =value for specified architectureBUILD_SETTING_NAME[config=configuration] =value for specified configuration
```

Given a choice between multiple definitions of the same build setting, the compiler resolves according to specificity.

```Plain
BUILD_SETTING_NAME[sdk=sdk][arch=architecture] =value for specified sdk and architecturesBUILD_SETTING_NAME[sdk=*][arch=architecture] =value for all other sdks with specified architecture
```

For example, you might specify the following build setting to speed up local builds by only compiling for the active architecture:

```Plain
ONLY_ACTIVE_ARCH[config=Debug][sdk=*][arch=*] = YES
```

### Including Build Settings from Other Configuration Files

A build configuration file can include settings from other configuration files using the same `\#include` syntax as the equivalent `C` directive on which this functionality is based:

```Plain
\#include "path/to/File.xcconfig"
```

Normally when the compiler encounters an `\#include` directive that can’t be resolved, it raises an error. But `xcconfig` files also support an `#include?` directive, that doesn’t complain if the file can’t be found.

There aren’t many cases in which you’d want the existence or nonexistence of a file to change compile-time behavior; after all, builds are best when they’re predictable. But you might use this as a hook for optional development tools like [Reveal](https://revealapp.com/), which requires the following configuration:

```Plain
# Reveal.xcconfig
OTHER_LDFLAGS = $(inherited) -weak_framework RevealServer
FRAMEWORK_SEARCH_PATHS = $(inherited) /Applications/Reveal.app/Contents/SharedSupport/iOS-Libraries
```

  

  

[https://nshipster.com/xcconfig/](https://nshipster.com/xcconfig/)

  

For xcconfig

  

[https://xcodebuildsettings.com/#category-swift](https://xcodebuildsettings.com/#category-swift)