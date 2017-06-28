* #### References: 
  - http://vimcasts.org/episodes/synchronizing-plugins-with-git-submodules-and-pathogen/
	

* #### To install and get configs (not plugins):
1. First Clone the repo and rename to `~/.vim` in your home folder	
  * `git clone http://github.com/skaugvoll/dotvim.git ~/.vim`

2. Then create Symbolic links so that VIM knows where to find the config files. (rc stands for run commands)	
  * `ln -s ~/.vim/vimrc ~/.vimrc`
  * `ln -s ~/.vim/gvimrc ~/.gvimrc`

* #### To install plugins after geting configs:
  1. `cd ~/.vim/bundle/`
  2. `git submodule init`
  3. `git submodule update`
  
* #### To install new plugins:
  1. `cd ~/.vim`
  2. `git submodule add <plugin-git-repo-url> bundle/<what-you-what-to-call-it-locally>`
  3. Optinally if needed by the plugin, do some changes to `vimrc` and or run some commands in `vim` 
