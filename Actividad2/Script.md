# Script Bash 

### read the variable
read -p "Pleas, enter your github username: " GH_USER

### Consult Github's API
URL="https://api.github.com/users/$GH_USER"

RESPONSE=$(curl -s $URL)

### Get JASON values
github_user=$(echo $RESPONSE | jq -r '.login')

id=$(echo $RESPONSE | jq -r '.id')

created_at=$(echo $RESPONSE | jq -r '.created_at')

### Print results on screen
echo "Hi $github_user. User ID: $id. the account was created on : $created_at."

### Creates a directory /tmp/<date_ac> if not existing
date_ac=$(date +"%Y%m%d")

dir_log="/tmp/$date_ac"

mkdir -p $dir_log

### Create log file
log_file="$log_dir/regards.log"

echo "Hi $github_user. User ID: $id. the account was 
created on : $created_at." > $log_file

echo "Message saved in: $log_file"
