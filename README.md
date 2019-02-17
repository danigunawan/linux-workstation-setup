***NOTE: There are some configs and tutorials here extracted from others websites and Github users (https://github.com/Rocketseat/ambiente-react-native, https://github.com/leonardoazeredo, Insomnia, Visual Code, Genymotion, Android), as I said, it's the full configuration for my workstation, so use it for the good.***

# Initial-linux-configs
A personal guide to configure the full development environment with Ruby, Rails, Node, Postgres, ReactJS and React Native.

# System dependencies

- Adds yarn to the repositories

```bash
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
```

- Adds PostgreSQL to the repositories

```bash
sudo sh -c "echo 'deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main' > /etc/apt/sources.list.d/pgdg.list"
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
```

- Install Linux Dependencies 

```bash
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev software-properties-common libffi-dev nodejs yarn postgresql-common postgresql-9.5 libpq-dev
```
- Install Node.js 10.x and some development tools to build native addons
  
```bash
curl -sL https://deb.nodesource.com/setup_10.x | sudo bash -
sudo apt install nodejs gcc g++ make -y
```

- To install the Yarn package manager, run:
```bash
curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt-get update && sudo apt-get install yarn
```

- Install rbenv for Ruby Environment

```bash
cd
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL
```

- Install ruby

```bash
rbenv install 2.5.3
```

- Use that version as Global

```bash
rbenv global 2.5.3
ruby -v
```

- Configure Git

```bash
git config --global color.ui true
git config --global user.name "username"
git config --global user.email "username@email.com"
ssh-keygen -t rsa -b 4096 -C "username@email.com"
```

- The next step is to take the newly generated SSH key and add it to your Github account. You want to copy and paste the output of the following command and paste it here(https://github.com/settings/ssh).

```bash
cat ~/.ssh/id_rsa.pub
```

- Once you've done this, you can check and see if it worked:

```bash
ssh -T git@github.com
```

- You should get a message like this:

```bash
Hi YOURNAME! You've successfully authenticated, but GitHub does not provide shell access.
```

- Install Rails Dependencies inside the project

```bash
gem install bundler ruby-debug-ide debase rubocop solargraph reek fasterer
gem install rails -v 5.2.1
rbenv rehash
rails -v
```

# PostgreSQL Configuration:

- The postgres installation doesn't setup a user for you, so you'll need to follow these steps to create a user with permission to create databases. Feel free to replace chris with your username.

```bash
sudo -u postgres createuser username -s
```

- If you would like to set a password for the user, you can do the following

```bash
sudo -u postgres psql
postgres=# \password username
```

# ReactJS Configuration

- The ReactJS only needs the NodeJS to run, but you can need to install the create-react-app package.

```bash
sudo npm install -g create-react-app -y
```

# React Native Configuration

- Just use the command below to get the React Native CLI.

```bash
sudo npm install -g react-native-cli
```

# Preparing Android Studio Environment 

- You might need it to run Genymotion or another emulator

- So first, lets add Java JDK dependencies

```bash
sudo add-apt-repository ppa:openjdk-r/ppa
sudo apt-get update
sudo apt-get install openjdk-8-jdk
```
Check your version ```bash java -version ```

-  After checking, install some 32-bits libraries

```bash
sudo apt-get install gcc-multilib lib32z1 lib32stdc++6
```

### Configuring SDK Android on Linux

 - To configure the Android SDK create a folder called `yourplace/Android/Sdk`. Ex: `~/Android/Sdk`

Enter https://developer.android.com/studio/#downloads, search for "Command line tools only" and download SDK for Linux distros. 

After that, extract the content of the folder at the folder created above.

Now, search for `~/.bash_profile` , `~/.profile` or `~/.zshrc` , then add those 3 lines below at the beginning of one:

```sh
export ANDROID_HOME=~/Android/Sdk
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/platform-tools
```
*If you didn't find any, create `~/.bash_profile`*

Now, finish it using that command:

```sh
~/Android/Sdk/tools/bin/sdkmanager  "platform-tools" "platforms;android-27" "build-tools;27.0.3" 
```

### Configuring Genymotion (chosen Android Emulator for React Native development)

- First, you'll need to install the Virtual Box (don't forget to enable the Virtualization at your BIOS on Motherboard):

```bash
sudo apt-get install virtualbox
```
- Now, download Genymotion (https://www.genymotion.com/fun-zone/) and enter the code below:

```bash
chmod +x genymotion-X.X.X_x64.bin
./genymotion-X.X.X_x64.bin
```

***WARNING: Don't forget to change the Genymotion Version.***

 - Then, go to Genymotion Settings at 'ADB' tab, and choose the path of your Android SDK.
 
# Extras (Tools, etc) 

- Fira Code ( https://github.com/tonsky/FiraCode)

- Visual Studio Code (https://code.visualstudio.com/docs/setup/linux)

For VSCode extensions, I use those Settings: 

```json
{
     "editor.fontFamily": "Fira Code, 'Droid Sans Mono', 'monospace', monospace, 'Droid Sans Fallback'",
    "editor.fontSize": 12,
    "editor.fontLigatures": true,
    "editor.formatOnSave": true,
    "editor.formatOnPaste": false,
    "workbench.iconTheme": "vscode-icons",
    "workbench.colorTheme": "One Dark Pro Bold",
    "workbench.startupEditor": "newUntitledFile",
    "terminal.integrated.fontSize": 12,
    "terminal.integrated.fontFamily": "Fira Code",
    "terminal.integrated.cursorStyle": "line",
    "terminal.integrated.cursorBlinking": true,
    "editor.occurrencesHighlight": false,
    "editor.selectionHighlight": false
}
```

And those Extensions, just put at Terminal: 
```bash
code --install-extension blanu.vscode-styled-jsx
code --install-extension cliffordfajardo.hightlight-selections-vscode
code --install-extension HookyQR.beautify
code --install-extension jpoissonnier.vscode-styled-components
code --install-extension mrmlnc.vscode-scss
code --install-extension naumovs.color-highlight
code --install-extension rebornix.ruby
code --install-extension robertohuertasm.vscode-icons
code --install-extension rocketseat.RocketseatReactJS
code --install-extension rocketseat.RocketseatReactNative
code --install-extension zhuangtongfa.Material-theme
```

- Insomnia (REST Client) (https://support.insomnia.rest/article/23-installation#ubuntu)

```bash
# Add to sources
echo "deb https://dl.bintray.com/getinsomnia/Insomnia /" \
    | sudo tee -a /etc/apt/sources.list.d/insomnia.list

# Add public key used to verify code signature
wget --quiet -O - https://insomnia.rest/keys/debian-public.key.asc \
    | sudo apt-key add -

# Refresh repository sources and install Insomnia
sudo apt-get update
sudo apt-get install insomnia
```



