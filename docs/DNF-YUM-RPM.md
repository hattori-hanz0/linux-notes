# Zarządzanie pakietami w systemie Fedora / CentOS

## DNF

### Instalacja oprogramowania

```
$ sudo dnf install <nazwa pakietu> <nazwa pakietu>
```

Instalacja pakietów z listy znajdującej się w pliku

```
$ sudo dnf install $(cat pakiety.txt)
```

To samo polecenie z pominięciem linii zaczynających się od znaku `#`

```
$ sudo dnf install $(grep "^[^#]" pakiety.txt)
```

### Usunięcie oprogramowania

```
$ sudo dnf remove <nazwa pakietu>
```

### Aktualizacja oprogramowania

```
$ sudo dnf update
```

### Sprawdzenie czy ostatnia aktualizacja zawierała aktualizację kernela

```
$ dnf history info last|grep kernel-core
```

## Wyświetlenie informacji o pakiecie

```
$ dnf info vim-X11

Ostatnio sprawdzono ważność metadanych: 0:00:15 temu w dniu nie, 20 lut 2022, 16:00:04.
Zainstalowane pakiety
Nazwa        : vim-X11
Epoka        : 2
Wersja       : 8.2.4386
Wydanie      : 1.fc35
Architektura : x86_64
Rozmiar      : 4.6 M
Źródło       : vim-8.2.4386-1.fc35.src.rpm
Repozytorium : @System
Z repoz.     : updates
Podsumowanie : The VIM version of the vi editor for the X Window System - GVim
Adres URL    : http://www.vim.org/
Licencja     : Vim and MIT
Opis         : VIM (VIsual editor iMproved) is an updated and improved version of the
             : vi editor.  Vi was the first real screen-based editor for UNIX, and is
             : still very popular.  VIM improves on vi by adding new features:
             : multiple windows, multi-level undo, block highlighting and
             : more. VIM-X11 is a version of the VIM editor which will run within the
             : X Window System.  If you install this package, you can run VIM as an X
             : application with a full GUI interface and mouse support by command gvim.
             :
             : Install the vim-X11 package if you'd like to try out a version of vi
             : with graphics and mouse capabilities.  You'll also need to install the
             : vim-common package.
```

### Wyszukanie pakietu zawierającego plik

Jako parametr można podać nazwę szukanego pliku lub pełną ścieżkę np. `/usr/sbin/ifconfig`.

```
$ dnf provides ifconfig

Ostatnio sprawdzono ważność metadanych: 0:02:52 temu w dniu nie, 20 lut 2022, 16:00:04.
net-tools-2.0-0.60.20160912git.fc35.x86_64 : Basic networking tools
Repozytorium       : @System
Dopasowano z:
Nazwa pliku : /usr/sbin/ifconfig
```

### Lista zainstalowanych pakietów

```
$ dnf list installed

zsh.x86_64                                    5.8.1-1.fc35                         @updates
```

### Lista zainstalowanych pakietów przez użytkownika

Pominięte zostaną pakiety zainstalowane przy instalacji oraz zależności.

```
$ dnf history userinstalled

zsh-5.8.1-1.fc35.x86_64
```
