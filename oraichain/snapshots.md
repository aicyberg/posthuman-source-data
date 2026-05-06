# 🚀 Restore Oraichain Node from [Posthuman](https://snapshots.oraichain.posthuman.digital/) Snapshots

This guide explains how to restore your Oraichain node using a snapshot from **Posthuman**.

---

## **🛑 Step 1: Stop Oraichain Node**
Before restoring, stop the Orai process to prevent database corruption:

```bash
sudo systemctl stop oraid
```

---

## **📌 Step 2: Backup Validator State (IMPORTANT)**
To avoid double signing issues, **backup your validator state file**:

```bash
cp $HOME/.oraid/data/priv_validator_state.json $HOME/.oraid/priv_validator_state.json.backup
```

---

## **🗑 Step 3: Remove Old Blockchain Data**
Delete the old data to **free space** and **prevent conflicts**:

```bash
rm -rf $HOME/.oraid/data
```

---

## **📥 Step 4: Download & Extract the Latest Posthuman Snapshot**
> **Note:** Since Posthuman updates snapshots **every 24 hours**, use the latest one:

```bash
curl -L https://snapshots.oraichain.posthuman.digital/data_latest.zst | zstd -dc - | tar -xf - -C $HOME/.oraid
```



---

## **📂 Step 5: Restore Validator State**
Move back the **backup validator state file**:

```bash
mv $HOME/.oraid/priv_validator_state.json.backup $HOME/.oraid/data/priv_validator_state.json
```

---

## **▶️ Step 6: Restart Side Node & Monitor Logs**
Now, restart the service and monitor its logs:

```bash
sudo systemctl restart oraid
sudo journalctl -u oraid -fo cat
```

---

## **✅ Done!**
Your node should now sync from the restored **Posthuman snapshot**. 🚀 

