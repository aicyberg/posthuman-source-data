# 🚀 Restore Zetachain Node from [Posthuman](https://snapshots.zetachain.posthuman.digital/) Snapshots

This guide explains how to restore your Zetacored node using a snapshot from **Posthuman**.

---

## **🛑 Step 1: Stop Zetachain Node**
Before restoring, stop the Zetachain process to prevent database corruption:

```bash
sudo systemctl stop zetacored
```

---

## **📌 Step 2: Backup Validator State (IMPORTANT)**
To avoid double signing issues, **backup your validator state file**:

```bash
cp $HOME/.zetacored/data/priv_validator_state.json $HOME/.zetacored/priv_validator_state.json.backup
```

---

## **🗑 Step 3: Remove Old Blockchain Data**
Delete the old data to **free space** and **prevent conflicts**:

```bash
rm -rf $HOME/.zetacored/data
```

---

## **📥 Step 4: Download & Extract the Latest Posthuman Snapshot**
> **Note:** Since Posthuman updates snapshots **every 24 hours**, use the latest one:

```bash
curl -L https://snapshots.zetachain.posthuman.digital/data_latest.zst | zstd -dc - | tar -xf - -C $HOME/.zetacored
```



---

## **📂 Step 5: Restore Validator State**
Move back the **backup validator state file**:

```bash
mv $HOME/.zetacored/priv_validator_state.json.backup $HOME/.zetacored/data/priv_validator_state.json
```

---

## **▶️ Step 6: Restart Zetachain Node & Monitor Logs**
Now, restart the service and monitor its logs:

```bash
sudo systemctl restart zetacored
sudo journalctl -u zetacored -fo cat
```

---

## **✅ Done!**
Your node should now sync from the restored **Posthuman snapshot**. 🚀 

