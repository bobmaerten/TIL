# Specify tmux panes layout with Tmuxinator

[Tmuxinator](https://github.com/tmuxinator/tmuxinator) is a tool for creating and manage tmux session easily. It handles configuration files in which you can specify windows and layouts, in order to organise you work.

Here is a way to be not limited to the 5 types of tmux layouts. The `tmux list-windows` command lets you get the actual layout parameters, which you can replicate in your tmuxinator config file:

    $ tmux list-windows
    1: editor* (2 panes) [178x51] [layout 1971,178x51,0,0[178x42,0,0,0,178x8,0,43,5]] @0 (active)

    $ cat ~/.tmuxinator/test.yml
    windows:
      - editor:
          layout: 1971,178x51,0,0[178x42,0,0,0,178x8,0,43,5]
          panes:
            - vim
            - guard
