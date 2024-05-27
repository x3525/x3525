---
glightbox: true
icon: material/help
---

# Working with Files and Directories

## Create an Empty File

```bash
touch readme.txt
```

## Create a Directory

```bash
mkdir -p Storage/local/user/documents
```

## Rename File

```bash
mv info.txt information.txt
```

## Move Files to Specific Directory

```bash
mv information.txt readme.txt Storage
```

## Questions

```text
What is the name of the last modified file in the "/var/backups" directory?
```

??? tip "Steps"

    Değişiklik zamanına göre sırala (en yenisi en önce):

    ```bash
    ls -lt
    ```

```text
What is the inode number of the "shadow.bak" file in the "/var/backups" directory?
```

??? tip "Steps"

    ```bash
    ls -i /var/backups/shadow.bak
    ```
