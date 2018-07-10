U-boot для платы miniEUSO
=====================

Название файла  | Содержание файла
----------------|----------------------
1.py            | Скрипт на python. Правильно генерирует BIN файл из BITSTREAM (с swap битами).
BOOT.bin        | Загрузчик U-Boot. Без bitstream внутри. 
fpga.bin        | BIN файл (с swap битами) сгенерированный из bitsream (fpga.bit)
fpga.bit        | BITSTREAM
FSBL_1.bif      | Файл из которого можно сгенерировать BOOT.bin
u-boot.elf      | Собранный U-boot для разработанной платы. Этот файл необходим для создания FSBL_1.
uEnv.txt        | файл uEnv.txt — это способ вставлять скрипты в u-boot на "лету".

*** 
С помощью скрипта на python из fpga.bit можно сгенерировать fpga.bin.

        $ python 1.py --flip fpga.bit fpga.bin
***
Если что-то случится с файлом BOOT.bin, то с помощью файла FSBL_1.bif его можно будет восстановить командой:

        $ bootgen -image FSBL_1.bif -o BOOT.bin -w on
***
На SD-карту необходимо скинуть следующие файлы:

1. BOOT.bin
2. fpga.bin
3. u-boot.elf
4. uEnv.txt
***
В папку TFTP сервера скидывеам следующие файлы:

1. fpga.bin
2. u-boot.elf


