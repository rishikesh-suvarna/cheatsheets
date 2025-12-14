# tmuxp YAML Config Cheatsheet

## Basic Structure

```yaml
session_name: mysession
windows:
  - window_name: editor
    layout: main-vertical
    panes:
      - shell_command:
          - vim
      - shell_command:
          - htop
  - window_name: server
    panes:
      - shell_command:
          - python manage.py runserver
```

## Key Sections

- `session_name`: Name of the tmux session.
- `windows`: List of windows in the session.
  - `window_name`: Name of the window.
  - `layout`: (Optional) tmux layout (e.g., `tiled`, `main-vertical`).
  - `panes`: List of panes in the window.
    - `shell_command`: List of commands to run in the pane.

## Example: Multiple Commands in a Pane

```yaml
panes:
  - shell_command:
      - cd ~/project
      - git status
      - npm start
```

## Tips

- Use `start_directory` to set the working directory for a window or pane.
- Use `focus: true` to focus a specific pane on startup.

```yaml
windows:
  - window_name: docs
    start_directory: ~/docs
    panes:
      - shell_command:
          - less README.md
        focus: true
```
