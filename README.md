# dero-pong-server
Inspired by CaptianDero's pong_server, I rewrote the code base in BASH. So, it's called dero-pong-server. 

This was a fun project.

Behavior:
Generate DERO iAddress to ping server,
Dispatch transfer PONG via DERO Network.

Gist:
`dero-pong-server` makes an integrated address for users to send a hard-coded amount of DERO to the `dero-pong-server` wallet. The `dero-pong-server` scans the wallet every ten seconds for new transfers that match the amount of DERO hard coded into the script. Once the `dero-pong-server` finds a transaction that isn't in the `dero-pong-server` database, the `dero-pong-server` dispatches a DERO transfer with a secret message over the DERO Blockchain.

Assuming you know how to launch a DERO wallet in RPC mode...

Get code:
```
wget https://raw.githubusercontent.com/secretnamebasis/dero-pong-server/main/dero-pong-server
```
Mark `dero-pong-server` executable 
```
chmod +x dero-pong-server
```
Update init variables at the head of the script
```
# Initialize Environment Variables
pong_amount="3771"
ip="192.168.12.109"
port="10107"
user="user"
pass="pass"
in_message="You are purchasing something cool"
out_message="You purchased this rad thing"
```
Run `dero-pong-server`
```
./dero-pong-server
```
