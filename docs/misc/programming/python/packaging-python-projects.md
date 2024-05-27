---
glightbox: true
---

# Packaging Python Projects

Gereklilikleri yükle:

```bash
python -m pip install -U twine build
```

Geçerli dizindeki dosyaları derle:

```bash
python -m build
```

Dosyaları karşıya (PyPI) yükle:

```bash
python -m twine upload dist/*
```

!!! info ".pypirc"

    Yükleme esnasında kimlik bilgilerinin sorulmaması için, `.pypirc` dosyası kullanılabilir. Bunun için, `.pypirc` dosyasını `$HOME` dizine aşağıdaki bilgiler ile kaydet:

    ```ini title="~/.pypirc" linenums="1"
    [pypi]
    username = __token__
    password = <PyPI token>
    ```

PIP ile istenen kurulumu gerçekleştir:

```bash
python -m pip install avsub
```
