<table align="center">
  <tr>
    <td style="text-align: center;vertical-align: middle;border:0px solid black; "><center><img width="180px" src="https://iili.io/HWivpNs.png" /></td>
     <td style="border:0px;"><h1 style="font-family: 'Prompt', sans-serif;font-size: 36px;letter-spacing: 0px;word-spacing: 0px;color: #f08000;font-weight: normal;text-decoration: none;font-style: normal;font-variant: normal;text-transform: none;">Nolus Protocol</h1> 
     </br> <h2 style="font-family: 'Prompt', sans-serif;font-size: 20px;color: #f08000;font-weight: normal;text-decoration: underline;font-style: italic;">Dashboard by und3r</h2></td> 
     <td style="text-align: center;vertical-align: middle;border:0px solid black; "><center><img width="180px" src="https://github.com/garaed/garaed/blob/main/ninja_logo.png?raw=true" /></td>
  </tr>
</table> </br>


> Snapshot parameters:
>- Pruning: 100 | 0 | 10; Indexer:null; Update: Every 12 hours; 



### Install dependencies
```
sudo apt update
sudo apt install lz4 -y
```
### Stop service
```
sudo systemctl stop nolusd
```
### Backup priv_validator_state
```
cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/priv_validator_state.json.backup 
```
### Reset data and download snapshot
```
nolusd tendermint unsafe-reset-all --home $HOME/.nolus --keep-addr-book 
curl http://95.216.241.112/nolus_snapshot/latest_snapshot.tar.lz4 | lz4 -dc - | tar -xf - -C $HOME/.nolus
```
### Restore priv_validator_state
```
mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json 
```
### Start service and check logs
```
sudo systemctl start nolusd
sudo journalctl -u nolusd -f --no-hostname -o cat
```
