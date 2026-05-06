# POSTHUMAN snapshot service for Agoric

> ⚠ **Snapshot service unavailable.** The public endpoint for this chain currently does not resolve (DNS missing). Use a community snapshot provider until the service is restored. See the chain's installation-guide.md for state-sync alternatives.

Updated every 24 hours

## Stop the service
```
sudo systemctl stop agoric
```
## Backup priv_validator_state.json
```
cp ~/.agoric/data/priv_validator_state.json ~/.agoric/priv_validator_state.json.backup
```
## Remove old data
```
rm -rf ~/.agoric/data
```
## Download and Extract the snapshot
```
curl https://snapshots.agoric.posthuman.digital/data_latest.lz4 | lz4 -dc - | tar -xf - -C ~/.agoric/
```
## Restore priv_validator_state.json
```
mv ~/.agoric/priv_validator_state.json.backup ~/.agoric/data/priv_validator_state.json
```

## Restart the service
```
sudo systemctl start agoric && sudo journalctl -u agoric -f -o cat
```
