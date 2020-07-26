# Python
> reference: https://github.com/pyenv/pyenv

## install
```
# clone git
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv

# setup environment
#!!!!! ubuntu 改 ~/.profile or ~/.bashrc
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bash_profile
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bash_profile
# 放 .bashrc
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc

# Add pyenv init to your shell
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bash_profile
# 放 .bashrc
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc

# Restart your shell so the path changes take effect.
$ exec "$SHELL"

# Install Python build dependencies
reference: https://github.com/pyenv/pyenv/wiki

# Install Python versions into $(pyenv root)/versions
$ pyenv install 2.7.8
```

## upgrading
```
$ cd $(pyenv root)
$ git pull
```

## uninstall
```
rm -rf $(pyenv root)
```

## .python-version
```
# create file .python-version in directory, auto change python version
```

## commands
> reference: https://github.com/pyenv/pyenv/blob/master/COMMANDS.md

