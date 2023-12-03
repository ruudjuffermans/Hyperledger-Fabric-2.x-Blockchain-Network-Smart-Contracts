# Install
./minifab install -n simple -l go

# Approve
./minifab approve

# Commit
./minifab commit

# Query
./minifab invoke -p '"query", "a"'
./minifab invoke -p '"query", "b"'

# Blockquery
./minifab blockquery
./minifab blockquery -b 3

# Combine commands for updating the chaincode
./minifab install,approve,commit,initialize -n simple -v 2.0 -p '"init","a","20","b","25"'

