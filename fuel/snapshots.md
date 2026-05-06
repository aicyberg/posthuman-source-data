# 🚀 Restore FUEL Node from [Posthuman](https://snapshots.fuel.posthuman.digital/) Snapshots

This guide explains how to restore your FUEL node using a snapshot from **Posthuman**.

---

## **🛑 Step 1: Stop FUEL Node**
Before restoring, stop the FUEL process to prevent database corruption:

```bash
sudo systemctl stop fuelsequencerd
```

---

## **📌 Step 2: Backup Validator State (IMPORTANT)**
To avoid double signing issues, **backup your validator state file**:

```bash
cp $HOME/.fuelsequencerd/data/priv_validator_state.json $HOME/.fuelsequencerd/priv_validator_state.json.backup
```

---

## **🗑 Step 3: Remove Old Blockchain Data**
Delete the old data to **free space** and **prevent conflicts**:

```bash
rm -rf $HOME/.fuelsequencerd/data
```

---

## **📥 Step 4: Download & Extract the Latest Posthuman Snapshot**
> **Note:** Since Posthuman updates snapshots **every 24 hours**, use the latest one:

```bash
curl -L https://snapshots.fuel.posthuman.digital/data_latest.zst | zstd -dc - | tar -xf - -C $HOME/.fuelsequencerd
```



---

## **📂 Step 5: Restore Validator State**
Move back the **backup validator state file**:

```bash
mv $HOME/.fuelsequencerd/priv_validator_state.json.backup $HOME/.fuelsequencerd/data/priv_validator_state.json
```

---

## **▶️ Step 6: Restart FUEL Node & Monitor Logs**
Now, restart the service and monitor its logs:

```bash
sudo systemctl restart fuelsequencerd
sudo journalctl -u fuelsequencerd -fo cat
```

---

## **✅ Done!**
Your node should now sync from the restored **Posthuman snapshot**. 🚀 
