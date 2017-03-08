## The Perfect Terminal

Being a Mac User, We clearly understand how boring the default terminal shell looks. Today we will be configuring the terminal for mac systems which is both aesthetically pleasing and also extremely useful.

After following this tutorial, the terminal for your mac will look something like this :

![](/assets/iTERM2.png)

As you can see, the color combination definitely looks appealing and it also tells you which branch you are using if you are inside a git repository. So Let's get started !



_**Note: **_Steps are documented below the video.

### iTerm 2 :

Firstly, download and install [iTerm2](https://www.iterm2.com/). It's a free replacement for the default terminal that comes with your OS X installation. The installation is pretty straightforward.

### ZSH \( Z Shell \):

Zsh is a shell designed for interactive use though it's also a powerful scripting language.

To install Oh My Zsh \( Zsh Framework\), just run below command in your iTerm2 terminal.

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

Visit their [GitHub page ](https://github.com/robbyrussell/oh-my-zsh)for more information.

### Solarized Color Scheme

To get the color scheme just like the one used in this tutorial \([Solarized](https://github.com/altercation/solarized/tree/master/iterm2-colors-solarized)\), you can run following command :

```
curl -o ~/Desktop/solarized.itermcolors https://raw.githubusercontent.com/altercation/solarized/master/iterm2-colors-solarized/Solarized%20Dark.itermcolors
```

This will download the latest Solarized Dark Colors scheme to your desktop. You can then open up the **iTerm's preferences pane**, select **Profiles**, select the **Colors tab** and click **load presets &gt; import and choose the solarized.itermcolors** file from your desktop.

After successfully importing the scheme file, you can **pick the theme from same dropdown.**

### Meslo Font

i'm using the **Powerline Meslo Font,** which is a really nice and comes with variety of symbols that are used in Zsh prompt. To install Powerline fonts, run the following command :

```
git clone https://github.com/powerline/fonts.git && cd fonts && ./install.sh 
```

Now From **iTerm's preferences pane**, click **profiles** again, go into **Text **tab and **change the font to Meslo LG L Regular For Powerline**. You can also play around other Powerline fonts.

### Agnoster Oh My Zsh Theme

When you installed Zsh on your system, its** .zshrc** file which is **similar to .profile of your bash shell in mac** is created in your users directory. **\( ~/.zshrc \)**. inside this file, change the **ZSH\_THEME **to** agnoster**. Now you should have a terminal looking similar to the screenshot in the beginning of this tutorial and you can start leveraging the powers of ZSH.

To improve your productivity even more, you can have a look at this [cheatsheet](https://github.com/robbyrussell/oh-my-zsh/wiki/Cheatsheet) which has some handy aliases for the Zsh, they're really useful.

Have fun with your new terminal.



