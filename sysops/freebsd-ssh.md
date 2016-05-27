# FreeBSD Debugging pubkey ssh login

Created a new user in FreeBSD. Had some trouble getting `~/.ssh/authorized_keys` to work. Everything looked like it was set up correctly. 

Useful debugging: 

```sh
sudo tail -f /var/log/auth.log
.
.
... sshd[723]: Authentication refused: bad ownership or modes for directory /usr/home/<user>
```

Turns out the new user's home directory was created with the permissions `770`. That wasn't restrictive enough for sshd. So a quick `chmod 700 $HOME` fixed it. Just a matter of knowing where to look. 