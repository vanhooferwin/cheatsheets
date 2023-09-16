# Shell cheats

## Customization

Start a new line after the prompt. 

### How? 
Edit your ```.bashrc``` file to include a custom bashrc script by adding the following code: 
```
## Check for a custom bashrc and load it
##
if [ -f ~/.bashrc_custom ]; then
    . ~/.bashrc_custom
fi
```

Create the ```.bashrc_custom``` file and add the following:
```
# Add a new line at the end of the command prompt
#PS1=${PS1}\\n
PS1=${PS1%?}
PS1=${PS1%?}\n'$ '
```

Start a new terminal session and now you get a new line after the prompt.


