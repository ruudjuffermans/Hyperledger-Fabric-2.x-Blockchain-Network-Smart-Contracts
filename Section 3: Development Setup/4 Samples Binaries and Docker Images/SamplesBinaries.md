##################################
#                                #
#    SAMPLES AND BINARIES        #
#                                #
##################################


# move to the mount folder
cd ~/mount

# download the package
curl -sSL https://bit.ly/2ysbOFE | bash -s -- 2.2.0 1.4.7

# checkout the network
cd ~/fabric-samples 

# copy the binaries to our usr/local/bin directory
sudo cp ./bin/* /usr/local


