# Praktická písemka - Linux a SAMBA server
## IT výuka - čas: 1,5 hodiny (90 minut)

---

**Jméno a příjmení:** Filip Podeszwa
**Datum:** 11.3. 2026
**Skupina:** ___________

---

## Oblast 1: Základní orientace v OS Linux (30 bodů)

### Úkol 1.1 (5 bodů)
Napište příkaz, kterým zjistíte obsah adresáře včetně skrytých souborů a atributů (práv).

**_Příkaz:** ls -l

### Úkol 1.2 (5 bodů)
Napište příkaz pro výpis prvních 15 řádků z textového souboru `data.txt`.

**_Příkaz:** head -n 15 <soubor>

### Úkol 1.3 (5 bodů)
Napište příkaz pro zjištění obsazené paměti v systému.

**_Příkaz:** free -h

### Úkol 1.4 (5 bodů)
Napište příkaz pro zobrazení rozdělení disků (partition).

**_Příkaz:** df

### Úkol 1.5 (5 bodů)
Vypište procesy běžící pod uživatelem "root".

**_Příkaz:** ps aux | grep root

### Úkol 1.6 (5 bodů)
Napište, k čemu slouží systém GRUB a uveďte umístění jeho konfiguračního souboru.

**_Odpověď:** GRUB je Bootloader, který funguje na zavádění BIOSU, konf. soubor je umístěn v kořenovém adresáři v '/etc'
______________________________________________________________________________

---

## Oblast 2: Instalace a konfigurace SAMBA serveru (35 bodů)

### Úkol 2.1 (5 bodů)
Nainstalujte na server program SAMBA.

**_Příkaz:** sudo apt install samba

### Úkol 2.2 (10 bodů)
Vytvořte dva uživatele systému Linux a následně je přidejte jako uživatele SAMBA:
- Uzivatel 1: **student1** (heslo: Student123)
- Uzivatel 2: **student2** (heslo: Student456)

**_Příkaz pro vytvoření uživatele Linux:** useradd student1 -p Student123, useradd student2 -p Student456
**_Příkaz pro pridani uzivatele do SAMBA:** smbpasswd -a student1, smbpasswd -a student1

### Úkol 2.3 (10 bodů)
Vytvořte adresář `/data` a nastavte následující práva:
- Vlastník: student
- Skupina: users
- Vlastník a skupina: čtení, zápis, prohlížení
- Ostatní: žádná práva

**_Příkazy:** mkdir data, chown student data/, chgrp users data/, chmod 770 data/

### Úkol 2.4 (5 bodů)
Napište, kde se nachází log soubory SAMBA s informacemi o přihlášení/odmítnutí uživatelů.

**_Odpověď:** /etc/samba/smb.conf

### Úkol 2.5 (5 bodů)
Napište příkaz, kterým zjistíte, na jakém portu naslouchá služba smbd.

**_Příkaz:** systemctl status smbd

---

## Oblast 3: Skenování sítě, zálohování a skripty (35 bodů)

### Úkol 3.1 (10 bodů)
Vytvořte skript `backup.sh`, který:
- Zazálohuje adresář `/data` do souboru `data_DDMMYYYY.tar.gz` (DD = den, MM = měsíc, YYYY = rok)
- Zkontroluje, zda soubor existuje - pokud ano, přejmenuje ho na `*.old`
- Vypíše informaci o úspěšném vytvoření zálohy

**_Skript:** _________________________________________________________________
______________________________________________________________________________
______________________________________________________________________________
______________________________________________________________________________
______________________________________________________________________________
______________________________________________________________________________

### Úkol 3.2 (10 bodů)
Vytvořte rsync příkaz pro zkopírování adresáře `/home/student` na SAMBA server do adresáře `/zaloha`.
Server: `192.168.1.100`, sdílená složka: `backup`

**_Příkaz:** rsync /home/student [student]192.168.1.100::/zaloha

### Úkol 3.3 (5 bodů)
Napište příkaz pro vyhledání počítačů v síti 192.168.10.0/24 a zobrazení jejich MAC adres.

**_Příkaz:** arp-scan 192.168.10.0/24

### Úkol 3.4 (5 bodů)
Nastavte cron úlohu, která bude spouštět skript `backup.sh` každý den ve 21:00.

**_Záznam do crontab:** 0 21 * * * backup.sh

### Úkol 3.5 (5 bodů)
Napište příkaz pro zálohu celého adresáře včetně atributů souborů s použitím gzip komprese.

**_Příkaz:** tar -cvzpf zaloha.tar.gz data/

---

## Celkem: 100 bodu

| Oblast | Body |
|--------|------|
| Oblast 1 | /30 |
| Oblast 2 | /35 |
| Oblast 3 | /35 |
| **Celkem** | **/100** |

**Známka:** __________
            Chtěl bych 1-2
---
