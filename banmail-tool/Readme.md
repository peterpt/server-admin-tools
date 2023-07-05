# Banmail Tool
- i uploaded this tool just for backup , however anyone may used it , but to put it working it is needed some changes in code
- This tool checks dovecot imap and pop3 errors and ban those ips directly in iptables with a DROP rule permanently .
- This tool also check in webserver logs (apache or nginx) for specific patterns in a config file (nginx.conf)
- and if it matches any of those patterns in config file then it will ban permanently that ip with a drop rule in iptables .
- this tool does a first backup of your current firewall rules for future need of you


## Adjustments in code
- **Green** square (This file is already in this git , are the patterns to search in nginx log and ban ips)
  more catterns can be added by you or remove any of those according to your server configuration , this file
  must be placed in /usr/local/share/banmail directory that this tool will create automatically on first run

- **Blue** squares are the configuration of the location of your firewall rules file that is loaded on system startup
  also the log files from dovecot and apache or nginx location for this tool to work .
  Those paths must be changed according to your server logs and firewall rules location   

**Notes** these are the only lines that must be adjusted in script , nothing more or will not work .
<img src="https://i.postimg.cc/BnM80RrY/codebanmail.jpg">

## Adjustments in your original firewall rules file
- This tool requires a Manual tag with the line #BANNED in original firewall rules for it to work
  this tag is an identifier for the tool insert new banned ips after that tag , however the tool will
  inform you of this in case it does not find it .
  
  <img src="https://i.postimg.cc/rFLCD7fy/firwall.jpg">

## Tool interface menu
 <img src="https://i.postimg.cc/J4kJptrx/menu.jpg">

## Banned ips
- Next image will show how it works , after adding the new banned ips to firewall rules it will
  reload iptables firewall rules and will check if everything is ok , in case anything fails
  on reloading the firewall rules then it will automatically revert to your previous rules saved
  and will load those rules .
  
  <img src="https://i.postimg.cc/pdYy11DC/bannedips.jpg">

  ## Log file
  - a log file is automatically created if an ip is banned , that log file is located in : /usr/local/share/banmail/banned.log
     , and will show you the ip that was banned and the reason why it was , next image shows a part of log file with email         bans , important data was retracted .
    
  <img src="https://i.postimg.cc/sgRv3rDy/maillog.jpg">

  - This part of the log shows banned ips with invalid requests in to webserver , these ips were banned because a pattern was found in their requests on webserver that is configured in nginx.conf in /usr/local/share/banmail directory
  - 
  <img src="https://i.postimg.cc/gJnYVYHC/weblog.jpg">
## Requirements
- iptables , dovecot , postfix , nginx or apache2 , nmap
- (apt install iptables dovecot postfix nginx nmap)
  
    ## Note : i did this tool for myself and uploaded to github for backup , do not expect much or any support on it in case you use it

    
