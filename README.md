
--- Смотрите этот текст на русском внизу. See this text in Russian below. ---

--- English ---

rbfl is an effective script for regular backups using rsync.
The script uses rsync, sshfs, cifs-utils, expect.

The script is preferably to run from the root account using cron.
Backups are created on the computer on which the script rbfl is running.

Description of variables whose value must be specified in the script:
$broot - directory for backups starting from the root directory.
$bgrp - group for backup. You can combine backups into groups
(for example "office", "hostings", "office2" etc)

The names of computers and disks for backups are passed in the arguments
of the copy_files function. For the copy_files function must be passed 1 argument
for linux computers (computer name) and 2 arguments for Windows computers
(computer name and drive letter).
These arguments are used in the names of mount scripts and source list files.
The mount scripts have filenames mount_<$fpath>, where fpath=$bgrp"_$1" (Linux) or
fpath=$bgrp"_$1_$2" (Windows).

Examples of mount scripts are given (files with names mount_* in the distribution).
By default the mount scripts should be in the folder "mount".
It is recommended to limit access rights to them as much as possible,
because scripts may contain passwords.

If for some reason the source for backup is not mounted after an attempt to mount,
the previous backup is set as the source.

Lists of files and folders for backup are in files with names backup_<$fpath>
(about $fpath see above).
Examples are given (files with names backup_* in the distribution).
Explanation for masks in the lists: one asterisk means any number of characters
or all files in the directory after the last slash;
two asterisks mean all files and directories after the last slash, i.e. recursion.

Backup folder structure: $broot/$bgrp/<date_and_time>/<computer_name>/<disk_letter (Windows only)>,
where <date_and_time> is the backup date and time in the format +%F--%H-%M,
and <computer_name> (Linux and Windows) and <disk_letter> (Windows only) are passed
as arguments of the function copy_files (see above).

Disk space for backups is used very efficent, rsync only copies new and changed files.
For all files that have not been changed after the previous backup, hardlinks are created.
All this is determined by the rsync startup parameters in the script.

The script writes backup logs to the directory /var/log/rsync
In addition, an emergency.log file is created in the same place,
in which mount errors are written.

--- Russian ---

rbfl - это эффективный скрипт для регулярных бэкапов при помощи rsync.
Использует rsync, sshfs, cifs-utils, expect.

Скрипт предпочтительно запускать из-под учетной записи root при помощи cron.
Бэкапы создаются на том компьютере, на котором запускается скрипт.

Описание переменных, значение которых необходимо указать в скрипте:
$broot - каталог для бэкапов, начиная с корня
$bgrp - группа файловых систем для бэкапа. Можно объединять бэкапы в группы
(например, "office", "hostings", "office2" и т.п.)

Имена компьютеров и дисков задаются в аргументах функции copy_files.
Функция copy_files принимает 1 аргумент для linux-компьютеров (имя компьютера)
и 2 аргумента для windows-компьютеров (имя компьютера и буква диска).
Эти аргументы используются в именах скриптов монтирования и файлов со списками источников.
Скрипты монтирования имеют имена вида mount_<$fpath>, где fpath=$bgrp"_$1" (Linux) или
fpath=$bgrp"_$1_$2" (Windows).

Примеры скриптов монтирования приведены (файлы с именами mount_*).
Скрипты монтирования по умолчанию должны находиться в папке mount
Рекомендуется максимально ограничить к ней доступ, так как в скриптах могут быть пароли.

Если по каким-то причинам источник не смонтирован после попытки монтирования,
в качестве источника задается предыдущий бэкап.

Списки файлов и папок для бэкапа находятся в файлах с именами backup_<$fpath>
(об этой переменной смотри выше).
Примеры списков приведены (файлы с именами backup_*).
Пояснение для масок в списках: одна звездочка означает любое количество символов
или все файлы в каталоге после последнего слеша;
две звездочки означают все файлы и каталоги после последнего слеша, то есть рекурсию.

Структура папки бэкапов: $broot/$bgrp/<дата и время>/<имя компьютера>/<буква диска (для Windows)>,
где <дата и время> - это дата и время бэкапа в формате +%F--%H-%M,
а <имя компьютера> (Linux и Windows) и <буква диска> (только для Windows) задаются
в качестве аргументов функции copy_files (смотри выше).

Место на диске для бэкапов используется очень экономно,
rsync копирует только новые и измененные файлы.
Для всех файлов, не измененных после предыдущего бэкапа, создаются хардлинки.
Все это определяктся параметрами запуска rsync в скрипте.

Скрипт ведет логи бэкапов в каталоге /var/log/rsync
Кроме того, там же создается файл emergency.log, в который пишутся ошибки монтирования.
