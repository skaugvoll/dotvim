References: 
	-http://vimcasts.org/episodes/synchronizing-plugins-with-git-submodules-and-pathogen/
	

To install:
	1. First Clone the repo and rename to .vim in your home folder	
		git clone http://github.com/skaugvoll/dotvim.git ~/.vim
	2. Then create Symbolic links so that VIM knows where to find the config files. (rc stands for run commands)	
		ln -s ~/.vim/vimrc ~/.vimrc
		ln -s ~/.vim/gvimrc ~/.gvimrc
