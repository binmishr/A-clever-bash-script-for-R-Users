# A-clever-bash-script-for-R-Users

You can find the bash script in https://github.com/msperlin/UBUNTU-Fresh-Install.
How to use it

    Download the github repository as a zip file
    Unpack the zip file and check all .txt files in all sub-folders. Remove or add software/R packages as needed.
    Within a terminal, execute the main script:

./UBUNTU_Install-Bash.sh

    type your sudo password and wait…

Installed Software

The bash script includes the following software:
Using apt

    libreoffice (lastest)
    texstudio (latest)
    obstudio (latest)
    many others (see file apt-to-install/list_to_install.txt)

Using custom bash scripts

    R (latest)
    R Packages
        See file R-pkgs/pkgs_to_install.txt
    RStudio (latest
        RStudio configuration – color scheme, size font, .. (see file Rstudio-Config/my-rstudio-prefs.json). You can get your own Rstudio preference file locally at ~/.config/rstudio/rstudio-pref.json.
    Google Chrome (latest)

Using snap

    Microsoft code (latest by snap)

Generating R package list

You can generate your own list of used R packages based on your existing code. For that, use the R code below, which will scan your files and retrieve all calls to existing packages. Do notice you’ll need to change the base folder in renv::dependencies.

library(dplyr)

my_r_dir <- 'YOUR-FOLDER-HERE'
df <- renv::dependencies(my_r_dir)

n_to_colect <- 50 # number of pkgs to collect (most to least frequent)

tbl_pkgs <- df %>%
  group_by(Package) %>%
  count() %>%
  arrange(-n) %>%
  #view() %>%
  ungroup() %>%
  slice(1:n_to_colect)

tbl_pkgs

