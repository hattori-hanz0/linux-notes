# Void Linux - Notatki

## Oprogramowanie dla dystrybucji Void

- `vpm` - uproszczony menadżer pakietów
- `fuzzypkg` - menadżer pakietów pod terminal
- `octoxbsp` - graficzny menadżer pakietów
- `vsv` - zarządzanie usługami
- `xtools` - narzędzia typowe dla dystrybucji Void

## Uruchomienie usługi

Uruchomienie usługi SSHD

```bash
$ ln -s /etc/sv/sshd /var/service
$ sv start sshd
```

## Aktualizacja repozytorium pakietów

Za pomocą komendy `xbps-install`

```
$ xbps-install -S
```

Za pomocą komendy `vpm`

```
$ vpm update
```

## Instalacja pakietu

Za pomocą komendy `xbps-install`

```
$ xbps-install -S [nazwa pakietu]
```

Za pomocą komendy `vpm`

```
$ vpm install -S [nazwa pakietu]
```

## Lista zainstalowanych pakietów

```
$ xbps-query -l
```

## Lista ręcznie zainstalowanych pakietów

```
$ xbps-query -lm
```

## Wyszukiwanie pakietów zawierających plik

Służy do tego narzędzie `xlocate` z pakietu `xtools`

Przy pierwszym uruchomieniu należy pobrać aktualną bazę używając parametru `-S`.
Tą operację należy co jakiś czas powtarzać.

Wyszukiwanie pakietów zawierających plik `/bin/bash`:

```
$ xlocate /bin/bash

xlocate: database outdated, please run xlocate -S.
bash-5.1.016_1  /usr/bin/bash
bash-5.1.016_1  /usr/bin/bashbug
bash-5.1.016_1  /usr/bin/rbash -> /usr/bin/bash
bash-preexec-0.4.1_1    /usr/bin/bash-preexec.sh
bashmount-4.3.2_1       /usr/bin/bashmount
bcc-tools-0.24.0_1      /usr/bin/bashreadline
chroot-bash-5.1.004_1   /usr/bin/bash
chroot-bash-5.1.004_1   /usr/bin/bashbug
chroot-bash-5.1.004_1   /usr/bin/sh -> /usr/bin/bash
```

## Sprawdzenie jakie usługi należy zrestartować po aktualizacji

Za pomocą polecenia `xcheckrestart`, które jest dostępne w pakiecie `xtools`
można sprawdzić czy i jakie usługi należy zrestartować po aktualizacji pakietów.

## Sprawdzenie zmian w /etc

Program `xetcchanges` znajduje się w pakiecie `xtools`.

Należy go uruchomić z uprawnieniami administratora za pomocą polecenia `sudo`.

```
$ sudo xetcchanges > etc-changes.diff
```

## Wyświetlenie informacji o pakiecie

Informacje o pakiecie można wyświetlić za pomocą polecenia `xbps-query` lub `vpm`

```
$ xbps-query -R xtools

architecture: x86_64
filename-sha256: b69dc6edc3e9ae8b9b8472e950db874adffdce22f1b1e1945cba9e93f9fce91d
filename-size: 21KB
homepage: http://git.vuxu.org/xtools
installed_size: 49KB
license: Public Domain
maintainer: Leah Neukirchen <leah@vuxu.org>
pkgname: xtools
pkgver: xtools-0.63_1
repository: https://alpha.de.repo.voidlinux.org/current
run_depends:
        bash>=0
        curl>=0
        findutils>=0
        git>=0
        make>=0
        spdx-licenses-list>=0
        xbps>=0
short_desc: Opinionated helpers for working with XBPS
source-revisions: xtools:0db3fef018
```

```
$ vpm info xtools

architecture: x86_64
filename-sha256: b69dc6edc3e9ae8b9b8472e950db874adffdce22f1b1e1945cba9e93f9fce91d
filename-size: 21KB
homepage: http://git.vuxu.org/xtools
installed_size: 49KB
license: Public Domain
maintainer: Leah Neukirchen <leah@vuxu.org>
pkgname: xtools
pkgver: xtools-0.63_1
repository: https://alpha.de.repo.voidlinux.org/current
run_depends:
        bash>=0
        curl>=0
        findutils>=0
        git>=0
        make>=0
        spdx-licenses-list>=0
        xbps>=0
short_desc: Opinionated helpers for working with XBPS
source-revisions: xtools:0db3fef018
```

## Wyłączenie uśpienia przy zamkniętym ekranie Laptopa

```
echo $(grep LID /proc/acpi/wakeup | awk '{print $4}' | cut -f 2,3 -d ':') >> /etc/rc.local
```

w pliku `/etc/rc.local` dodajemy:

```
echo PNP0C0D:00 > /sys/bus/acpi/drivers/button/unbind
```

gdzie `PNP0C0D:00` to wartość pobrana z pliku `/proc/acpi/wakeup` za pomocą pierwszego polecenia.
