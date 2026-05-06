# 🚀 Restore Neutron Node from [Posthuman](https://snapshots.neutron.posthuman.digital/) Snapshots

This guide explains how to restore your Neutron node using a snapshot from **Posthuman**.

---

## **🛑 Step 1: Stop Neutron Node**
Before restoring, stop the Neutron process to prevent database corruption:

```bash
sudo systemctl stop neutron
```

---

## **📌 Step 2: Backup Validator State (IMPORTANT)**
To avoid double signing issues, **backup your validator state file**:

```bash
cp $HOME/.neutrond/data/priv_validator_state.json $HOME/.neutrond/priv_validator_state.json.backup
```

---

## **🗑 Step 3: Remove Old Blockchain Data**
Delete the old data to **free space** and **prevent conflicts**:

```bash
rm -rf $HOME/.neutrond/data
```

---

## **📥 Step 4: Download & Extract the Latest Posthuman Snapshot**
> **Note:** Since Posthuman updates snapshots **every 24 hours**, use the latest one:

```bash
curl -L https://snapshots.neutron.posthuman.digital/data_latest.zst | zstd -dc - | tar -xf - -C $HOME/.neutrond
```



---

## **📂 Step 5: Restore Validator State**
Move back the **backup validator state file**:

```bash
mv $HOME/.neutrond/priv_validator_state.json.backup $HOME/.neutrond/data/priv_validator_state.json
```

---

## **▶️ Step 6: Restart Neutron Node & Monitor Logs**
Now, restart the service and monitor its logs:

```bash
sudo systemctl restart neutron
sudo journalctl -u neutron -fo cat
```

---

## **✅ Done!**
Your node should now sync from the restored **Posthuman snapshot**. 🚀 
