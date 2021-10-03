# Your first YED!
You should [read this](https://your-editor.org/user_guide.html) after you're done with this short tutorial.
#### Things to know before we get started
* This guide assumes your XDG Config Home is at `~/.config/`
* Also assumes no previous knowledge of yed

With that, let's get to it.

## Part 1: Initial greeting

Hello and welcomed to a simple config tutorial for `yed`.

After downloading and [instaling](https://your-editor.org/install.html) `yed`, the first time you run it you will be greeted by our octopus friend, Charlie (name pending), followed by a pop-up like this one

![image](https://user-images.githubusercontent.com/71751817/135678302-496c5315-9308-499b-8a1d-31424c08d1d4.png)

followed by this

![20211001_14h49m12s_grim](https://user-images.githubusercontent.com/71751817/135678366-2b78b3b6-7b5d-46b1-adfe-660c7466f85f.png)

The first one is `yed` offering you a simple bare-bones configuration, I would recommend you press `y` since we are going to work based off of this. <br />
The second one is `yed` offering to install it's package manager, `ypm`, not necessary, but again I recommend you press `y` because we will be working based off of this.

After `ypm` does it's initial magic, you will be greeted by a screen like this one
![20211001_15h03m08s_grim](https://user-images.githubusercontent.com/71751817/135683181-873925c8-431d-4fab-ba4b-0f2aa333f601.png)

here you will pick the plugins you want, say you scroll down a bit and see `style_use_term_bg`, it catches your attention because no one can get any work done if they can't see the wallpaper of their computer, so you install it and... nothing? <br />
`ypm` is very neat because it autoloads everything you have installed, so now we just restart and open `yed` and get amazed at the full glory of our terminal's ~~transparency~~ background colour an- <br />
![20211001_15h44m48s_grim](https://user-images.githubusercontent.com/71751817/135684105-1e0e36c4-3bab-482b-b08d-541e5f5a3869.png)

**what the fuck is this?**
Ok so if we go full sherlock and run `man ~/.config/yed/ypm/man/man7/style_use_term_bg.7` you will see that there is a function called `style-term-bg` and it takes 1 parameter, `<style>`, so we gotta go and open our `yedrc`, find the line that says `style casey` and replace it with `style-term-bg casey`, save and exit and you will finally see a very beautiful `yed`.

Now to do some work...

## Part 2: Wait what? I have to write my own keybindings?

That is correct, if you press `ctrl-y` when in `yed` you will get a prompt at the bottom, type `show-bindings` and you will see you have almost no keybindings!
<br />
Keybindings get mapped to functions, be it custom or [the ones that come by default](https://your-editor.org/cmd_ref.html), theres A LOT of them, [Sir CEO of yed, kammerdiener](https://github.com/kammerdienerb/yed) likes to keep his programs portable and clean so while `yed` does not get features every single release, the features it does get added to the core are stable and work everywhere, the rest is left up to the users, `yed` gets it's power from its flexibility (where have I heard that one before).

I will not go through the keybindings in this tutorial, but for some emacs-like to get you started I will give you this, paste it at the end of your `yedrc`
``` bash
bind "ctrl-x ctrl-c" quit
bind "ctrl-x ctrl-u" undo
bind "ctrl-x ctrl-r" redo
bind "ctrl-x ctrl-s" write-buffer 
bind "meta-w" yank-selection
bind "ctrl-y" paste-yank-buffer
bind "meta-x" command-prompt
bind "ctrl-a" cursor-line-begin
bind "ctrl-e" cursor-line-end 
bind "meta-v" select
bind "meta-;" comment-toggle
bind "ctrl-f" cursor-right
bind "ctrl-c ctrl-b" find-in-buffer
bind "meta-n" find-next-in-buffer
bind "meta-p" find-prev-in-buffer
bind "bsp" multi "yank-selection 1" "delete-back"
bind "del" multi "yank-selection 1" "delete-forward"
bind "ctrl-d" multi "yank-selection 1" "delete-forward"
bind "ctrl-z" multi "cursor-line-end" "insert 13"
bind "ctrl-q" cursor-prev-word
bind "ctrl-w" cursor-next-word 
bind "ctrl-g" multi "jump-stack-push" "ctags-jump-to-definition"
bind "ctrl-o" jump-stack-pop 
bind "meta-bsp" multi "select-lines" "yank-selection 1" "delete-forward"
bind "meta-1" "command-prompt" "cursor-line " 
bind "meta-h" frame-prev
bind "meta-l" frame-next
bind "meta-3" frame-vsplit
bind "meta-2" frame-hsplit
bind "meta-0" frame-delete    
```

If you read it carefully you will notice a couple of things, first no combination of modifiers, second no `ctrl+numbers`, third a strange keyword, `multi`. <br />
So first and second can be explained by the fact that `yed` tries to stay portable, `yed` will run on anything with RAM if it has a POSIX compliant OS running on it but due to terminal emulator memes and other such things we cannot do the first 2. While this might seem like a problem at first sight, if you stop and think about it for a moment, in other text editors (in my experience) finding keybindings that do not shadow previous ones is always a headache, but here you have all the keybindings free, so with ctrl + letters you get 26 combinations, then with alt you get another 47, that's 73, that seems decent enough for me, then if you use `vimish` or `drill` you get even MORE.
<br />
The last one is because of modularity, while not explicitly stated, `yed` sticks to this very famous UNIX principle very well, so if you want to accomplish something like cutting a line (like i do with `meta-bsp`) you will have to do `multi` commands.

To explain `meta-bsp` command further, we first write `bind meta-bsp` then we have to add the `multi` since we want this one to do more than one thing, then we follow it with `"select-lines"`, starts selection but instead of being char based it's line based, we only do this and no movement or anything else dealing with selections because we want just the line we are on, after this we do `"yank-selection 1"` the `1` paramater makes it so when we run yank-selection, it doesn't copy the selection then instantly takes us out of selection mode, finally we actually delete the line with `"delete-forward"`, you can change this to `"delete-backward"` if you like.

Now we can just type `meta-x` then `quit` to exit, if you want to save, simply type `write-buffer`. Orrrrrr just `ctrl-x ctrl-s` followed by `ctrl-x ctrl-c` to accomplish the same.

## More?
Maybe later, this is just a quick little something I wanted to write to get started.

For now you know how to install plugins and load them and where to look for configuration, including the man pages and the [command reference](https://your-editor.org/cmd_ref.html).

and also [read this](https://your-editor.org/user_guide.html) 😡
