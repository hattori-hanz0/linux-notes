# Git

## Generowanie klucza SSH

```
ssh-keygen -f github-hattori -t ed25519 -C "adres email lub komentarz"
```

W przypadku kiedy nasz klient SSH nie obsługuje algorytmu ED25519 najlepiej skorzystać z RSA

```
ssh-keygen -f github-hattori -t rsa -C "adres email lub komentarz"
```

Polecenie `ssh-keygen` utworzy parę kluczy, klucz prywatny i klucz publiczny. Klucz publiczny należy
dodać do naszego konta na Githubie.

## Przygotowanie konfiguracji

Konfiguracja klienta SSH znajduje się w pliku `~/.ssh/config`

Standardowo nie trzeba tego robić, ale używając kilku kont na Githubie warto rozważyć taką
konfigurację.

Tutaj stworzymy własną nazwę hosta np: `github-hattori`, która będzie rozwiązywana na nazwę hosta
`github.com` za pomocą parametru `Hostname`, kolejnym parametrem jest `User` gdzie ustawiamy swoją
nazwę użytkownika, ostatnim parametrem jest `IdentityFile` czyli ścieżkę i nazwę pliku klucza SSH.

```
Host github-hattori
    Hostname github.com
    User hattori-hanz0
    IdentityFile ~/.ssh/klucze/github-hattori
```

Pobranie repozytorium należy wykonać przez hosta, którego skonfigurowaliśmy w pliku `~/.ssh/config`

```
git@[nazwa-hosta-z-ssh-config]:[nazwa-użytkownika]/[nazwa-repozytorium]
```

dla tego repozytorium URL będzie wyglądał tak:

```
git clone git@github-hattori:hattori-hanz0/linux-notes
```
