# 🚀 Restore Axelar Node from [Posthuman](https://snapshots.axelar.posthuman.digital/) Snapshots

This guide explains how to restore your Axelar node using a snapshot from **Posthuman**.

---

## **🛑 Step 1: Stop Axelar Node**
Before restoring, stop the axelar process to prevent database corruption:

```bash
sudo systemctl stop axelar
```

---

## **📌 Step 2: Backup Validator State (IMPORTANT)**
To avoid double signing issues, **backup your validator state file**:

```bash
cp $HOME/.axelar/data/priv_validator_state.json $HOME/.axelar/priv_validator_state.json.backup
```

---

## **🗑 Step 3: Remove Old Blockchain Data**
Delete the old data to **free space** and **prevent conflicts**:

```bash
rm -rf $HOME/.axelar/data
```

---

## **📥 Step 4: Download & Extract the Latest Posthuman Snapshot**
> **Note:** Since Posthuman updates snapshots **every 24 hours**, use the latest one:

```bash
curl -L https://snapshots.axelar.posthuman.digital/data_latest.zst | zstd -dc - | tar -xf - -C $HOME/.axelar
```



---

## **📂 Step 5: Restore Validator State**
Move back the **backup validator state file**:

```bash
mv $HOME/.axelar/priv_validator_state.json.backup $HOME/.axelar/data/priv_validator_state.json
```

---

## **▶️ Step 6: Restart Axelar Node & Monitor Logs**
Now, restart the service and monitor its logs:

```bash
sudo systemctl restart axelar
sudo journalctl -u axelar -fo cat
```

---

## **✅ Done!**
Your node should now sync from the restored **Posthuman snapshot**. 🚀 
