# ДЗ по защите ОС: права, set-UID, привилегии, sudo

Игольников С. А., зачётка М265234. Fedora Linux 45, ВМ `ws-lab01`.

| Файл | Раздел |
| --- | --- |
| mephi-screenshot.png | 6.1 |
| history.out | все |
| stat.out | 1, 3, 4 |
| getcap.out | 4 |
| suid_files.out | 2.1 |
| privileged_procs.out | 2.2 |
| etc/passwd, etc/shadow, etc/group | 1 |
| etc/sudoers | 5 |

Кратко по разделам:

1. `user1` (uid 1234), группа `students`, `chage -M 90` — пароль меняется раз в 90 дней.
2. Файлы с set-UID: `find / -xdev -type f -perm -4000`. Процессы: `ps -eo pid,ppid,ruid,user,euid,cmd` с фильтром; пока искал, во втором терминале висел `sudo passwd user1`.
3. Копия `cat` с `chmod u+s` и владельцем root — от `user1` читает `/etc/shadow`, обычный `cat` не может.
4. Копия `chown` с `setcap cap_chown+ep` — от `user1` меняет владельца файла, обычный `chown` получает отказ.
5. В `/etc/sudoers` добавил `user1 ALL=(root) /usr/bin/date, /usr/bin/timedatectl`.

После перезагрузки проверил — настройки сохранились. `/etc/shadow` в репозитории лежит копией, снятой через `sudo cat`.
