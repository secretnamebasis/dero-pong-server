# dero-pong-server
Inspired by CaptianDero's pong_server, I rewrote the code base in BASH. 

This was a fun project.

Behavior:
Generate DERO iAddress to ping server,
Dispatch transfer PONG via DERO Network.

Gist:
`pong_server` makes an integrated address for users to send a hard-coded amount of DERO to the `pong_server` wallet. The `pong_server` scans the wallet every ten seconds for new transfers that match the amount of DERO hard coded into the script. Once the `pong_server` finds a transaction that isn't in the `pong_server' database, the `pong_server` dispatches a DERO transfer with a secret message over the DERO Blockchain.

Assuming you know how to launch a DERO wallet in RPC mode...

Get code:
```
wget https://raw.githubusercontent.com/secretnamebasis/dero-pong-server/main/pong_server
```
Mark `pong_server` executable 
```
chmod +x pong_server
```
Run `pong_server`
```
./pong_server
```
