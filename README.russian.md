
Я написал утилиту на perl, chpkgf, которая умеет выполнить две произвольные
программы над списком файлов полученным от третьей программы. Я пользуюсь для
обработки (chown,chmod) файлов из установленных rpm пакетов. Можно через
опции командной строки адаптировать к почти любому манагеру файлов - к любому
который способен выводить список файлов 1 на строку. 

BUGS: Последовательность выполнения не гарантиуется. То есть две программы 
выполняются, похоже, в произвольном порядке. Других не замечено. ;)

Пример использования:

# ./chpckgf -packagelist \
egcs-objc-1.1.2-24,egcs-g77-1.1.2-24,compat-egcs-objc-5.2-1.0.3a.1

# ./chpckgf -packagelist \
egcs-objc-1.1.2-24,egcs-g77-1.1.2-24,compat-egcs-objc-5.2-1.0.3a.1 \
-chmodprog `which chattr` -chmodopts "-V +i" -disablechown

Пример вывода программы:

[20:05:22 root@olli Change-RPM-PackageFiles]# ./chpckgf -packagelist egcs-objc-1.1.2-24,egcs-g77-1.1.2-24
using defaults for package manager options: -ql .
using defaults for package manager programm: /bin/rpm .
using defaults for chmod (1) options: ug-w,o-rwx .
using defaults for chmod programm: /bin/chmod -v  .
using defaults for chown programm: /bin/chown -v  .
using defaults for package manager files extention: .rpm .
owner of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/cc1obj retained as root.wheel
mode of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/cc1obj retained as 0550
(r-xr-x---)
owner of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/include/objc retained as root.wheel
mode of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/include/objc retained as 0550 (r-xr-x---)
owner of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/include/objc/NXConstStr.h retained as root.wheel
mode of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/include/objc/NXConstStr.h retained as 0440 (r--r-----)
owner of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/include/objc/Object.h retained as root.wheel
mode of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/include/objc/Object.h retained as 0440 (r--r-----)
owner of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/include/objc/Protocol.h retained as root.wheel
mode of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/libobjc.a retained as 0440 (r--r-----)
owner of /usr/bin/f77 retained as root.wheel
mode of /usr/bin/f77 retained as 0550 (r-xr-x---)
owner of /usr/bin/g77 retained as root.wheel
mode of /usr/bin/g77 retained as 0550 (r-xr-x---)
owner of /usr/info/g77.info.gz retained as root.wheel
mode of /usr/info/g77.info.gz retained as 0440 (r--r-----)
owner of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/f771 retained as root.wheel
mode of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/f771 retained as 0550 (r-xr-x---)
owner of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/include/g2c.h retained
as root.wheel
mode of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/include/g2c.h retained as 0440 (r--r-----)
owner of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/libg2c.a retained as root.wheel
mode of /usr/lib/gcc-lib/i386-redhat-linux/egcs-2.91.66/libg2c.a retained as 0440 (r--r-----)
owner of /usr/man/man1/f77.1 retained as root.wheel
mode of /usr/man/man1/f77.1 retained as 0440 (r--r-----)
owner of /usr/man/man1/g77.1 retained as root.wheel
mode of /usr/man/man1/g77.1 retained as 0440 (r--r-----)



