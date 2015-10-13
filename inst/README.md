

# logon to the server using a sudo user
ssh -X sfl@oncoclass.hpc.aau.dk

# Installing the latest version of R

#Start a terminal 

#Start a super user session
sudo su 

#Add the R mirror to the source list
echo "deb http://mirrors.dotsrc.org/cran/bin/linux/ubuntu trusty/ #enabled-manually" >> /etc/apt/sources.list

# Exit the super user session
exit

#Add the key
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E084DAB9

#Intall R
sudo apt-get update && sudo apt-get install r-base r-base-dev

#Install shiny according to 
http://www.rstudio.com/products/shiny/download-server/

# open port 3838 for shiny
sudo ufw allow 3838
sudo ufw allow 8787
sudo ufw allow 8080
sudo ufw allow 80

# In order to install devtools:
apt-get -y build-dep libcurl4-gnutls-dev
apt-get -y install libcurl4-gnutls-dev







# install the packages needed to run the scripts

sudo -i R

source("http://bioconductor.org/biocLite.R")
biocLite("affy")
biocLite("affyio")
biocLite("preprocessCore")

# Then form CRAN
install.packages("shiny")
install.packages("matrixStats")
install.packages("Rcpp")
install.packages("RcppArmadillo")
install.packages("RcppEigen")
install.packages("testthat")
install.packages("gdata")
install.packages("survival")
install.packages("WriteXLS")

# Finally the package is installed.
install.packages("devtools")  # Uncomment if devtools is not installed
devtools::install_github("oncoclass/hemaClass", 
                        dependencies = TRUE)

devtools::install_github("analytixware/shinysky")

# To gain support for reading xlsx files
gdata::installXLSXsupport(perl = "perl", verbose = FALSE)


#################################
# General editing
#################################

# installing shiny applications


# In a local terminal the following command copies the current homepage to the server
scp -r /Users/Falgreen/Documents/R-packages/hemaClass/inst/website/. sfl@oncoclass.hpc.aau.dk:~/hemaClass/

# logon to the server using a sudo user
ssh -X sfl@oncoclass.hpc.aau.dk

# After you have logged in you can copy the file into the shiny server
sudo cp -r  ~/hemaClass/ /srv/shiny-server/hemaClass/website/





# In a local terminal the following command copies the current homepage to the server
scp -r /Users/mboegsted/Documents/R-packages/hemaClass/inst/website/. m_boegsted@dcm.aau.dk@oncoclass.hpc.aau.dk:~/hemaClass/

# logon to the server using a sudo user
ssh -X m_boegsted@dcm.aau.dk@oncoclass.hpc.aau.dk

# After you have logged in you can copy the file into the shiny server
sudo cp -r  ~/hemaClass/. /srv/shiny-server/hemaClass/website/


##########################################
# In order to only submit changes made to the homepage and not the database use
scp -r /Users/Falgreen/Documents/R-packages/hemaClass/inst/website/. sfl@oncoclass.hpc.aau.dk:~/

ssh -X sfl@oncoclass.hpc.aau.dk

sudo cp -r  ~/ /srv/shiny-server/hemaClass/website
#########################################

#########################################
scp -r /Users/mboegsted/Documents/R-packages/hemaClass/inst/website/ m_boegsted@dcm.aau.dk@oncoclass.hpc.aau.dk:~/

ssh -X m_boegsted@dcm.aau.dk@oncoclass.hpc.aau.dk

sudo cp -r  ~/ /srv/shiny-server/hemaClass/website
#########################################



# install new version of the package

sudo -i R
devtools::install_github("oncoclass/hemaClass", dependencies = TRUE)



# apache stuff

# To enable the oncoclass configuration file for apache2 write
sudo a2ensite oncoclass.conf

# restarting the apache server
sudo service apache2 restart

# restarting the shiny server

sudo restart shiny-server