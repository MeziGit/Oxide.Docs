---
title: Getting Started
after: 0
---

# Getting started with plugin development

Welcome to the world of game modding using the Oxide framework! This guide is the first step on your journey towards creating unique and immersive plugins<sup><a href="/glossary#plugins">[3]</a></sup> that can add new layers of functionality to supported games.

## Introduction to Oxide Plugin Development

Oxide is a powerful modding framework that allows developers to create plugins<sup><a href="/glossary#plugins">[3]</a></sup> to modify and enhance gameplay on game servers. With Oxide, you can build plugins<sup><a href="/glossary#plugins">[3]</a></sup> that introduce new features, tweak gameplay elements, and fundamentally transform the player experience.

## Key Concepts

Before you dive in, there are a few key concepts to understand:

- **Plugins**: These are self-contained bits of code which modify game server behavior. Plugins<sup><a href="/glossary#plugins">[3]</a></sup> are distributed as CSharp (C#) files with a `.cs` file extension.

- **Hooks**: These are functions that get called by the game or by Oxide. By using hooks<sup><a href="/glossary#hooks">[7]</a></sup> in your plugins<sup><a href="/glossary#plugins">[3]</a></sup>, you can define what happens when certain game events occur.

- **Configuration**: Most plugins<sup><a href="/glossary#plugins">[3]</a></sup> generate a JSON<sup><a href="/glossary#json">[8]</a></sup> configuration file that server administrators can use to change how the plugin works. Understanding how to create and manage config files<sup><a href="/glossary#config-files">[9]</a></sup> is essential.

- **Data Files**: Plugins<sup><a href="/glossary#plugins">[3]</a></sup> can create data files<sup><a href="/glossary#data-files">[10]</a></sup> in JSON<sup><a href="/glossary#json">[8]</a></sup> format to store persistent information. These files are saved in the `oxide/data` directory.

- **Permissions**: Many plugins<sup><a href="/glossary#plugins">[3]</a></sup> have permissions<sup><a href="/glossary#permissions">[11]</a></sup> which must be assigned to users or groups<sup><a href="/glossary#groups">[12]</a></sup> in order to use certain plugin features. Implementing a proper permission system is crucial for server administration.

- **Commands**: Plugins<sup><a href="/glossary#plugins">[3]</a></sup> can add new commands that may be used by players or server administrators. This can include both console commands and chat commands.

- **Testing and Debugging**: A significant part of plugin development is testing your creations and fixing any bugs that arise. Familiarizing yourself with debugging tools will save you time and frustration.

## Next Steps

With these basic concepts in mind, you're ready to embark on your journey as an Oxide plugin developer! In the following sections, we'll dive into:

1. Setting up your [Development Environment](development-environment)
2. Creating [Your First Plugin](my-first-plugin)
3. Following [Best Practices](best-practices) for plugin development
4. Understanding [Plugin Guidelines](plugin-guidelines) for publishing

Let's get started on your plugin development journey!
