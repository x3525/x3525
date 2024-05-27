---
glightbox: true
---

# Bash Prompt Command

Bash shell üzerinde `PROMPT_COMMAND` değişkeni kullanılarak, PS1 gösterilmeden önce çalıştırılacak olan komut ayarlanabilir.

Örneğin aşağıdaki komutu ele alalım:

```bash
echo "PROMPT_COMMAND=ls" >> ~/.bashrc
```

Bu komut sayesinde, prompt gösterilmeden önce mevcut dizinin içeriği `ls` komutu ile listelenecektir.
