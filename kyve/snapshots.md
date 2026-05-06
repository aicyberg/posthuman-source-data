# 🚀 Restore Kyve Node from [Posthuman](https://snapshots.kyve.posthuman.digital/) Snapshots

This guide explains how to restore your Kyve node using a snapshot from **Posthuman**.

---

## **🛑 Step 1: Stop Kyve Node**
Before restoring, stop the Kyve process to prevent database corruption:

```bash
sudo systemctl stop kyved
```

---

## **📌 Step 2: Backup Validator State (IMPORTANT)**
To avoid double signing issues, **backup your validator state file**:

```bash
cp $HOME/.kyve/data/priv_validator_state.json $HOME/.kyve/priv_validator_state.json.backup
```

---

## **🗑 Step 3: Remove Old Blockchain Data**
Delete the old data to **free space** and **prevent conflicts**:

```bash
rm -rf $HOME/.kyve/data
```

---

## **📥 Step 4: Download & Extract the Latest Posthuman Snapshot**
> **Note:** Since Posthuman updates snapshots **every 24 hours**, use the latest one:

```bash
curl -L https://snapshots.kyve.posthuman.digital/data_latest.zst | zstd -dc - | tar -xf - -C $HOME/.kyve
```



---

## **📂 Step 5: Restore Validator State**
Move back the **backup validator state file**:

```bash
mv $HOME/.kyve/priv_validator_state.json.backup $HOME/.kyve/data/priv_validator_state.json
```

---

## **▶️ Step 6: Restart Kyve Node & Monitor Logs**
Now, restart the service and monitor its logs:

```bash
sudo systemctl restart kyved
sudo journalctl -u kyved -fo cat
```

---

## **✅ Done!**
Your node should now sync from the restored **Posthuman snapshot**. 🚀 

