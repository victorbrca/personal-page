+++
tags = [
]
categories = [
]
showthedate = false
date = "2016-10-19T23:26:12-05:00"
title = "How to Create A Prompt With Timeout in Bash"

+++

Here's a quick function that will display a prompt with timeout in a bash script:

```bash

_myCountdownFunction () {
echo -e "Hit \"Ctrl+c\" to quit or \"Enter\" to continue...    \c" 
cnt=5
while (( cnt >= 0 )) ; do
  if (( cnt < 9 )) ; then
    echo -e "\b\b${cnt}s\c"
  elif (( cnt == 9 )) ; then
    echo -e "\b\b\b ${cnt}s\c"
  elif (( cnt <= 99 )) ; then
    echo -e "\b\b\b\b ${cnt}s\c"
  elif (( cnt < 999 )) ; then
    echo -e "\b\b\b\b${cnt}s\c"
  fi
  read -t 1 my_reply
  (( $? == 0 )) && exit 1
  let cnt-=1
done
}

```

The user will see the following message on his terminal with the seconds counting down in place:


```
john@ubuntu:~$ Hit "Ctrl+c" to quit or "Enter" to continue... 5s
```

At the end of the specified time in 'cnt', the script (where the function would be) will continue executing, and if the user hits "Ctrl+c" before that, it will exit (both script and function).

The function supports up to 999s (which should be enough).