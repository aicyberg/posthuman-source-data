# 🚀 Restore Pell Testnet Node from [Posthuman](https://snapshots.pell-testnet.posthuman.digital/) Snapshots

> ⚠ **Snapshot service unavailable.** The public endpoint for this chain currently does not resolve (DNS missing). Use a community snapshot provider until the service is restored. See the chain's installation-guide.md for state-sync alternatives.


This guide explains how to restore your Pell testnet node using a snapshot from **Posthuman**.

---

## **🛑 Step 1: Stop Pell Node**
Before restoring, stop the Pell process to prevent database corruption:

```bash
sudo systemctl stop pellcored
```

---

## **📌 Step 2: Backup Validator State (IMPORTANT)**
To avoid double signing issues, **backup your validator state file**:

```bash
cp $HOME/.pellcored/data/priv_validator_state.json $HOME/.pellcored/priv_validator_state.json.backup
```

---

## **🗑 Step 3: Remove Old Blockchain Data**
Delete the old data to **free space** and **prevent conflicts**:

```bash
rm -rf $HOME/.pellcored/data
```

---

## **📥 Step 4: Download & Extract the Latest Posthuman Snapshot**
> **Note:** Since Posthuman updates snapshots **every 24 hours**, use the latest one:

```bash
curl -L https://snapshots.pell-testnet.posthuman.digital/data_latest.lz4 | lz4 -dc - | tar -xf - -C $HOME/.pellcored
```



---

## **📂 Step 5: Restore Validator State**
Move back the **backup validator state file**:

```bash
mv $HOME/.pellcored/priv_validator_state.json.backup $HOME/.pellcored/data/priv_validator_state.json
```

---

## **▶️ Step 6: Restart Pell Node & Monitor Logs**
Now, restart the service and monitor its logs:

```bash
sudo systemctl restart pellcored
sudo journalctl -u pellcored -fo cat
```

---

## **✅ Done!**
Your node should now sync from the restored **Posthuman snapshot**. 🚀 

