- The netntlm hashes are not usable to do pass the hash, but you can crack them to retrieve the password.
- For strong, "uncrackable" hash, we can relay them (only works if signing:False)
    - `cme smb 192.168.56.10-23 --gen-relay-list relay.txt`

