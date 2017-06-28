
## Hvordan lage et github repo som hoster vim config filer.

Path : `~/`  Betyr home-directory, dette er mappene hvor Documents og Downloads befinner seg. 

**Diverse filer som vi blir å trenge og hva de er:**

`.vimrc`    # vanlige vim konfig filen (mandatory)

`.gvimrc` # (graphicalVim) for å gjore visuelle konfigurerering av vim (denne filen er optional)

`.vim/`  # En directory / mappe for å holde vim plugins konfigureringer osv. Denne skal bli et repo.

Siden dette er en mappe for å holde konfigureringsfiler og slikt, så flytter vi `.vimrc` og `.gvimrc` inn hit

 `$ mv .vimrc  .vim/vimrc` # gjør ikke den til en skult fil, siden den er i en skult mappe, bare for ordensskyld

 `$ mv .gvimrc  .vim/gvimrc` # gjør ikke den til en skult fil, siden den er i en skult mappe, bare for ordensskyld

Men når vi starter opp `vim` vil det lete etter `.vimrc` og `.gvimrc` i home-directory ( `~/` ), så vi må lage en symlink fra `~/` til våre `vimrc` og `gvimrc` filer, slik at `vim` vet hvor den skal finne konfigureringene sine. Dette gjør vi med

`$ ln -s ~/.vim/vimrc ~/.vimrc`

`$ ln -s ~/.vim/gvimrc ~/.gvimrc`

Nå kan vi gjøre `~/.vim/ diretory` til et git repository, 

`$ cd .vim`

`$ git init `

$ touch (eller vim) README.md

- Burde også legge til Instruksjoner på hvordan installere og bruke vim konfigureringene.

- Altså hva en bruker som ønsker å bruke våre konfigureringer må gjøre for at det skal funke

- Det første er å klone repoet til `~/` som `~/.vim` og ikke som navne vi har gitt repoet. 

- Også må det lages symboliske linker slik som vi gjorde, `ln -s ~/.vim/vimrc ~/.vimrc` og samme for `gvimrc` slik at denne maskinens vim vet hvor konfigureringene er. 

Kommandoene er: 

`git clone http://github.com/dudarev/dotvim.git ~/.vim`

`ln -s ~/.vim/vimrc ~/.vimrc`

`ln -s ~/.vim/gvimrc ~/.gvimrc`

Then we have to add the new new `README` file to the git repo and then commit it.

`$ git add .`

`$ git commit -m “initial commit”`

Now all we have to do is create a git repository online, 

[github.com](http://github.com); create new repository, call it whatever you want, I’ll call it dot vim

Then we have to push our `.vim` repo to this new remote repository. 

`$ git remote add origin [https://github.com/skaugvoll/dotvim.git](https://github.com/skaugvoll/dotvim.git)`

`$ git push -u origin master`

Now we are all set to clone and install the configurations on another machine. Just follow the `README` commands under “Installing”

**Now we can make changes to our configuration files, add, commit and then push them to the remote repository from our local machine / repo. **

Then the other user can pull the changes and they should be ready to use. 
*NOTE* if modules / plugins are installed. These are jet not installed. Need to read along to read about submodules to get them installed.

##

##Installere & Synke Plugins - 

Det vi blir å gjøre er å installere plugins som git submoduler (repo inni repo) 

**Den første plugin vi installere er Pathogen og den hjelper og gjør det enklere å installere andre plugins.**

Pathogen plugin makes it easy to install plugins as a bundle, thus we don’t have to download a vim plugin, copy the doc file into ~/.vim/doc and the plugin into ~/.vim/plugin now we can install the hole thing under another subdirectory of ~/.vim/autoload (We have to make this directory)

`$ cd ~/.vim`

`$ mkdir autoload` # this will host our Pathogen plugin installer

We also have to make another directory to hold all the plugins we want to install using Pathogen

`$cd ~/.vim`

`$ mkdir bundle`

Then we can download pathogen from their site ([http://www.vim.org/scripts/script.php?script_id=2332](http://www.vim.org/scripts/script.php?script_id=2332)) as `.vim` file and copy / move it into `~/.vim/autoload/`

There are two ways of downloading and installing

One way is to go to their site, download the file, as of now, the most reason update is downloadable as a `.zip`, so u can download the `.zip` and then just move the `pathogen.vim` file to `~/.vim/autoload` or you can use the following command ` curl -LSso ~/.vim/autoload/pathogen.vim [https://tpo.pe/pathogen.vim](https://tpo.pe/pathogen.vim) `. 

Hvis du gikk for å laste ned `.zip` så kan du skrive navigere til plassen `pathogen.vim` eller `autoload/pathogen.vim` ble lastet ned også skrive

`$ mv pathogen.vim ~/.vim/autoload/`

Nå for å aktivere pathogen I `vim`, må vi åpne  `~/.vim/vimrc` filen vår å legge til en linje øverst.

`$ cd ~/.vim`

`$ vim vimrc`

Legg til linjen øverst i filen.

`execute pathogen#infect() `

Det denne linjen gjør er : Now any plugins you wish to install can be extracted to a subdirectory under `~/.vim/bundle`, and they will be added to the 'runtimepath'.  And now you can use `:Helptags` to run `:helptags` on every doc/ directory in your 'runtimepath'.  Super sweet. `:Helptags` makes doc files for our plugins.

Så Pathogen tillåter oss nå å ha alle plugins som mapper inni en mappe som heter `~/.vim/bundle/`

**Installere plugins I /bundle/**

Beste måten å gjøre dette på er å bruke ` git submodules xxxx ` Dette tillater å ha git repo inni git repo.

Nå kan vi installere en plugin som heter fugitive, som er en plugin for å wrappe Github kommandoer, og de sier selv at de vim-fugitive er the best Git wrapper of all time

Det første vi må gjøre er å skifte til vim repoet vårt.

`$ cd ~/.vim`

Så finne git url-en til plugin vi ønsker å installere. Dette er samme url som om man skal klone repoet til plugin.

F.eks, vim-fugitive sin url er:

- [https://github.com/tpope/vim-fugitive.git](https://github.com/tpope/vim-fugitive.git)

**Så nå kan vi installere plugin som en submodule **

`$ git submodule add https://github.com/tpope/vim-fugitive.git bundle/fugitive `

Det vi gjør her er at vi ønsker å `git submodule add` <__plugin__url__repo__> <til lokal filbane>, hvis vi ønsker å endre navn kan vi gjøre det. F.eks så heter plugin `vim-fugitive`, men vi ønsker å kalle den bare `fugitive` siden det er ganske openbart at det er en vim plugin ut ifra at den er med i `~/.vim` repoet vårt. 

Nå ble det laget en ny skult filen (starter med .) den heter `.gitmodules` og inneholder innformasjon om alle submodules.

**Recap of installing a plugin.**

Nå har vi installert en plugin som heter vim-fugitive. 

Det vi måtte gjøre er 

`$ git submodule add <plugin-GITrepo-url> <to our bundle directory>`

`$ Possibly add a few lines to the vimrc file to make vim activate and use the plugin.`

##

## Hvordan andre kan pulle configs og installere plugins / submodules:**

De må pulle siste versjon av vårt remote reposetory (dotvim)

`$ cd ~/.vim`

`$ git pull`

Sjekk at `~/.vim/bundle/` directory finnes. Det vil ikke være noen submodules filer der, eller bare de man allerede har installert. For å få siste endringer må man

`$ git submodule init` # registerer alle submodule som er i `.gitmodules` filen og dermed havner de her i `/bundle/`

`$ git submodule update` # seeker ut og oppdaterer versjonen av pluginen  

**Oppsummering:**
Denne måten å gjøre det på er superbra hvis det er mange submodules / plugins som må / skal installeres da man trenger bare å utføre de to kommandoene en gang og alle plugins / submodules blir installert. Hvis de ikke funker, sjekk at de er lagt til i `vimrc` filen - hvis det trengs. (Dette finner / står på github siden eller hjemmesiden til plugin’en).

 
