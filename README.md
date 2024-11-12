# DOS Director 1.1

> [!NOTE]
> This documentation is for DOS Director 1.1<br/>
> For other versions [click here](https://github.com/MattStypa/DOS-Director/releases)

Welcome to **DOS Director**! This project is designed to simplify your experience with DOS environments, making it easy to launch your favorite DOS programs without the hassle.

<img width="1440" alt="DOS Director screenshot" src="https://github.com/user-attachments/assets/cbe5a21c-e43d-498b-ac96-0e9f9fa9ff99">

## What is DOS Director?
**DOS Director** is a menu-driven command runner that allows you to easily configure and launch DOS programs. Originally developed to enhance my own DOSBOX experience, it has evolved into a flexible tool compatible with any DOS setup.

## Features
- **Easy Configuration**: Quickly create your own menu using a simple config file.
- **Nested Menus**: Organize your commands into groups and submenus.
- **Meta Commands**: Define commands to run before and after each selection for setup and cleanup.
- **Compatibility**: Ideal for DOSBOX but works well in any DOS environment.

## Downloading DOS Director
[Click here to download DOS Director](https://github.com/MattStypa/DOS-Director/releases)

## Freeware
**DOS Director** is released as freeware, meaning it is available for use at no cost. Freeware software can be freely distributed and used without any financial obligation, making it accessible to everyone. While you can use DOS Director without charge, it is important to note that it cannot be modified.

## How to Use DOS Director
To run **DOS Director**, pass a configuration file as a parameter when starting the program:

```
DIRECTOR.EXE MENU.CFG
```

For convenience, a `start.bat` file is included in the release. 

You can set it up in your `dosbox-x.conf` file as follows:

```
mount x drives/dos-director
x:
start
```

## Configuration File Setup
### Basic Setup
The configuration file defines options by wrapping the option name in square brackets. The commands for that option follow on the next lines.

Empty lines and indentation are ignored, and lines prefixed with `#` are treated as comments and also ignored.

```
[Doom II]
  # Use novert to disable vertical mouse movement
  mount c drives/doom2
  c:
  novert
  capmouse /c
  doom2
  capmouse /r
  novert /u
```

### Advanced Setup
For more complex configurations, you can use special tags and nested menus.

#### Meta Commands
You can execute specific commands before and after every selected option using `{before}` and `{after}` tags. This is especially useful for unmounting drives.

```
{before}
  mount -u c
```

#### Nested Menus
To create nested menus, wrap them in curly brackets.

```
[Utilities] {
  [QuickBASIC 4.5]
    mount c drives/qb45
    mount d drives/code
    c:
    qb

  [DOS prompt]
    command

  [Windows 95]
    config -bootconf drives/win95/dosbox-x.conf

  *[BACK]
}
```

Notice the option prefixed with an asterisk `*`. This tells **DOS Director** that this option exits the current menu.

#### Nested Meta Commands
Each nested menu can have it's own `{before}` and `{after}` tags. All meta tags in the hierarchy will be executed in the top-to-bottm order.

```
{before}
  echo Runs first

{after}
  echo Runs fourth

[Submenu]
  {before}
    echo Runs second

  {after}
    echo Runs fifth

  [Command]
    echo Runs third
```

## Feedback and Support
For bugs and issues, please [click here](https://github.com/MattStypa/DOS-Director/issues). For questions, ideas, or other discussions, feel free to [click here](https://github.com/MattStypa/DOS-Director/discussions).

Thank you for checking out **DOS Director**! I look forward to your feedback and hope you find it useful for your DOS adventures!
