# mephi-linuxsecurity-2026
Георгий Ш
№:374975
________________________________________________________________
Создание пользователя
sudo useradd -u 1234 user1

Создание группы и добавление user1
sudo groupadd students
sudo usermod -aG students user1

Установка пароля
sudo passwd -e user1 

Настройка срока действия пароля
sudo chage -m 0 -M 90 -W 5 -I 10 user1

Проверка результата
sudo grep user1 /etc/shadow

__________________________________________________________________
Поиск файлов с установленным битом set-UID
sudo find / -perm -4000 -fprintf /root/suid.txt '%#m %u %p\n'

Поиск процессов, у которых эффективный UID = 0, а реальный UID ≥ 1000
 sudo ps -eo pid,ruid,euid,comm | awk '$2 >= 1000 && $3 == 0' > UID.txt
 cat UID.txt
___________________________________________________________________

Копирование
cp /usr/bin/cat .

Смена привелегий
sudo chown root:root ./cat
sudo chmod u+s ./cat

Выполнение привилегированной операции
./cat /etc/shadow

____________________________________________________________________

Копирование
cp /usr/bin/chown .

Смена привелегий
sudo setcap "cap_chown=ep" chown

Выполнение привилегированной операции
./chown root UID.txt
./chown user1 UID.txt

____________________________________________________________________

Редактирование конфигурационного файла /etc/sudoers
sudo visudo

Выдача прав в файле
user1   ALL=(root) /usr/bin/date

Смена времени в терминале user1
sudo date --set="Tue Oct 30 11:11:11 EEST 2026"

____________________________________________________________________

Сбор артефактов
history > ~/history.out 
stat /home/user1/ > ~/stat.out
stat /home/admin/cat > ~/stat.out
tat /home/admin/chown >> ~/stat.out
getcap /home/admin/chown > ~/getcap.out
