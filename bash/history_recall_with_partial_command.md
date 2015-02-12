## How to recall a command from history with a partially typed command on the prompt?

Here a neat feature from bash. Simply add these lines in your `.bahsrc` to enable history search with arrow keys:

    # Key bindings, up/down arrow searches through history
    bind '"\e[A": history-search-backward'
    bind '"\e[B": history-search-forward'
    bind '"\eOA": history-search-backward'
    bind '"\eOB": history-search-forward'

On your prompt, type a few characters from a previous command, then <Up> key and, voilà!
