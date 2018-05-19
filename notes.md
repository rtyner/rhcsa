# Misc. Notes

* Input and Output Redirection
  * \> - redirect and overwrite
  * \>> - appends file
  * 2> - redirect stderr to something and hide from stdout
    * 2 represents error
  * 2>&1 - redirects stderr to stdout
    * can be used as input with |
  * /dev/null - redirect here to dump into nothingness
  * head - first 10 lines to stdout
    * ex. head messages - first 10 lines of messages file
  * tail -f - continue appending as it's added to the file

* Using grep and regex to Analyze Text
  * grep '^#' /etc/ssh/sshd_config
    * ^ - means to search for lines that start with
    * searches that file and looks for lines that start with #
  * grep -i 'rsaauth' /etc/ssh/sshd_config
    * -i - ignore case
    * finds all occurances of rsaauth, ignoring case

