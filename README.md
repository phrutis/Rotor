Brute force Bitcoin private keys random 
![alt text](Others/2.jpg "Rotor")
# Rotor (OpenCL)
Это модифицированная версия [oclexplorer](https://github.com/svtrostov/oclexplorer) от svtrostov.
Огромная благодарность [kanhavishva](https://github.com/kanhavishva) и всем разработчикам, чьи коды были использованы в Rotor OpenCL
## Примечания:  
- [Пошагово как создать базу адресов addresse160-Sort.bin или скачать](https://github.com/phrutis/Rotor/issues/1) 
- [Гипотеза - Почему Random лучше перебора](https://github.com/phrutis/Rotor/issues/3)
- Для работы программы нужно преобразовать Legacy адреса (которые начинаются на 1) в бинарные хэши160 RIPEMD160. 
- Для преобразования используйте программу [b58dec](https://github.com/phrutis/Rotor/blob/main/Others/b58dec.exe) ```Команда: b58dec.exe 1.txt 2.bin```
- Важно выполнить сортировку файла 2.bin Иначе Bloom фильтр поиска не будет работать должным образом. 
- Что бы отсортировать 2.bin используйте программу [RMD160-Sort](https://github.com/phrutis/Rotor/blob/main/Others/RMD160-Sort.exe) ```Команда: RMD160-Sort.exe 2.bin addresse160-Sort.bin```
- Минимальное количество хешей160 в addresse160-Sort.bin должно быть не менее 1000! 
- [RTX3900, RTX3080 решение ошибки CL_MEM_OBJECT_ALLOCATION_FAILURE](https://github.com/phrutis/Rotor/issues/5)
- [Зачем нужны файлы START.bat и Next.bat](https://github.com/phrutis/Rotor/issues/2)
## Параметры:
```
Rotor.exe -h
Usage: Rotor [options...]
Options:
    -p, --platform         Platform id [default: 0]
    -d, --device           Device id [default: 0]
    -r, --rows             Grid rows [default: 0(auto)]
    -c, --cols             Grid cols [default: 0(auto)]
    -i, --invsize          Mod inverse batch size [default: 0(auto)]
    -m, --mode             Address mode [default: 0] [0: uncompressed, 1: compressed, 2: both] (Required)
    -u, --unlim            Отключить генерацию нового хэша [по умолчанию: 0] [0: откл., 1: вкл.]  пример: -u 1
    -k, --privkey          Стартовый хэш пример: -k b5d4045c3f466fa91fe2cc6abe79232a1a57cdf104f7a26e716e0a1e2789df78
    -f, --file             RMD160 Address binary file path (Required)
    -h, --help             Shows this page
```

## Пример работы Rotor.exe
```
C:\Users\user>Rotor.exe -m 1 -f 10.bin

ARGUMENTS:
        PLATFORM ID: 0[default: 0]
        DEVICE ID  : 0[default: 0]
        NUM ROWS   : 0[default: 0(auto)]
        NUM COLS   : 0[default: 0(auto)]
        INVSIZE    : 0[default: 0(auto)]
        ADDR_MODE  : 1[0: uncompressed, 1: compressed, 2: both]
        UNLIM ROUND: 0
        PKEY BASE  :
        BIN FILE   : 10.bin

Загрузка адресов   : 100 %
Загруженно адресов : 90693 за 0,149708 сек.

Bloom at 000002075FE48F20
        Version    : 2.1
        Entries    : 181386
        Error      : 0,0000100000
        Bits       : 4346488
        Bits/Elem  : 23,962646
        Bytes      : 543311 (0 MB)
        Hash funcs : 17

Loading program file: gpu.cl


MATRIX:
        Grid size  : 4608x4096
        Total      : 18874368
        Mod inverse: 36864 threads [512 ops/thread]

DEVICE INFO:
        Device              : NVIDIA GeForce RTX 2070
        Vendor              : NVIDIA Corporation (10de)
        Driver              : 471.41
        Profile             : FULL_PROFILE
        Version             : OpenCL 3.0 CUDA
        Max compute units   : 36
        Max workgroup size  : 1024
        Global memory       : 8589934592
        Max allocation      : 2147483648

        Project Rotor v1.01 : https://github.com/phrutis/Rotor
        Donate BitCoin      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9


Iteration 1 at [2021-08-04 00:03:44] from: e75a05bacbec700fc730c33300f8cb04d670e5e21890af307eb0d07857ebb82e
[e75a05bacbec700fc730c33300f8cb04d670e5e21890af307eb0d079562bb82e] [round 227: 0,13s (143,39 Mkey/s)] [total 4,284,481,536 (148,13 Mkey/s)]
Iteration 2 at [2021-08-04 00:04:12] from: 7e095d787dd2f6cef6c1b98bf06d47b1ebbb41385bddb285b4ba6b022293eeb7
[7e095d787dd2f6cef6c1b98bf06d47b1ebbb41385bddb285b4ba6b0320d3eeb7] [round 227: 0,12s (161,75 Mkey/s)] [total 8,568,963,072 (149,81 Mkey/s)]
Iteration 3 at [2021-08-04 00:04:40] from: d6925a4f22342e0d44ddcd36fe06d9dc6852540d54a451f302d08b788d8ecdc4
[d6925a4f22342e0d44ddcd36fe06d9dc6852540d54a451f302d08b78cececdc4] [round 59: 0,12s (161,75 Mkey/s)] [total 9,682,550,784 (150,34 Mkey/s)]

```
# Пример работы Rotor2.exe
```
C:\Users\user>Rotor2.exe -m 1 -f 01.bin

ARGUMENTS:
        PLATFORM ID: 0[default: 0]
        DEVICE ID  : 0[default: 0]
        NUM ROWS   : 0[default: 0(auto)]
        NUM COLS   : 0[default: 0(auto)]
        INVSIZE    : 0[default: 0(auto)]
        ADDR_MODE  : 1[0: uncompressed, 1: compressed, 2: both]
        UNLIM ROUND: 0
        PKEY BASE  :
        BIN FILE   : 01.bin

Загрузка адресов   : 100 %
Загруженно адресов : 1326779 за 1,159541 сек.

Bloom at 0000026FE9D68A70
        Version    : 2.1
        Entries    : 2653558
        Error      : 0,0000100000
        Bits       : 63586270
        Bits/Elem  : 23,962646
        Bytes      : 7948284 (7 MB)
        Hash funcs : 17

Loading program file: gpu.cl


MATRIX:
        Grid size  : 4608x4096
        Total      : 18874368
        Mod inverse: 36864 threads [512 ops/thread]

DEVICE INFO:
        Device              : NVIDIA GeForce RTX 2070
        Vendor              : NVIDIA Corporation (10de)
        Driver              : 471.41
        Profile             : FULL_PROFILE
        Version             : OpenCL 3.0 CUDA
        Max compute units   : 36
        Max workgroup size  : 1024
        Global memory       : 8589934592
        Max allocation      : 2147483648
        Random              : Каждую секунду + 100-150 млн. значений
        Project Rotor v1.02 : https://github.com/phrutis/Rotor
        Donate BitCoin      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

[45d981bde0162b3ca4126d211230de3a962f71058e85cea0249d2db958c151ec] (175,23 Mkey/s) [total: 10,060,038,144]
```
## Изминения:
- Изменино время генерации нового хеша. Выставил генерацию через 0.5-1 сек. (было ~30 секунд или 4,284,481,536) К новому хешу добавляется значения +70-300 млн.
- Для удобства использования убрал отображение "Iteration 1 at [дата, время] from: xxxxxxxxxxxxxxxx" которое переносилось на новую строку и засоряло экран.
- Зафиксирована коретка printf, теперь после обновления нового хеша строка остается на месте.
- При использовании большого файла адресов (25млн. и больше) в режиме both происходят ложноположительные срабатывания найденых адресов. Примерно 20 ложных адресов на 20.000.000.000 хешей. В связи с этим отключил вывод информации о найденом хэше на экран.
- Для удобства сделал вывод в 2 файла Found.txt и BASE.txt 
- В файле Found.txt только адреса, в файле BASE.txt вся информация.
- Сделано это для удобства, копируем адреса из файла Found.txt и вставляем их в окно проверки адресов списком на сайте. К примеру на сайтах: https://www.homebitcoin.com/easybalance/ или https://bitcoindata.science/bitcoin-balance-check.html или http://addresschecker.eu 
- Можете найти свои сайты для проверски списком. Желательно проверять на двух разных сайтах, для точности.
- Файл gpu.cl нужен, без него не работает!
- С базой до 5.000.000 адресов, ложноположительные срабатывания не обнаружены.
# Пример работы Rotor3.exe (FULL RANDOM)
```
C:\Users\user>Rotor3.exe -m 1 -f 10.bin

ARGUMENTS:
        PLATFORM ID: 0[default: 0]
        DEVICE ID  : 0[default: 0]
        NUM ROWS   : 0[default: 0(auto)]
        NUM COLS   : 0[default: 0(auto)]
        INVSIZE    : 0[default: 0(auto)]
        ADDR_MODE  : 1[0: uncompressed, 1: compressed, 2: both]
        UNLIM ROUND: 0
        PKEY BASE  :
        BIN FILE   : 10.bin

Загрузка адресов   : 100 %
Загруженно адресов : 90693 за 0,141924 сек.

Bloom at 0000022E5ADC9210
        Version    : 2.1
        Entries    : 181386
        Error      : 0,0000100000
        Bits       : 4346488
        Bits/Elem  : 23,962646
        Bytes      : 543311 (0 MB)
        Hash funcs : 17

Loading program file: gpu.cl
Compiling CL, can take minutes...

MATRIX:
        Grid size  : 4608x4096
        Total      : 18874368
        Mod inverse: 36864 threads [512 ops/thread]

DEVICE INFO:
        Device              : NVIDIA GeForce RTX 2070
        Vendor              : NVIDIA Corporation (10de)
        Driver              : 471.41
        Profile             : FULL_PROFILE
        Version             : OpenCL 3.0 CUDA
        Max compute units   : 36
        Max workgroup size  : 1024
        Global memory       : 8589934592
        Max allocation      : 2147483648
        Random              : Full
        Project Rotor v1.03 : https://github.com/phrutis/Rotor
        Donate BitCoin      : bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9

[6971a5815b3435e6a86c0cfe1fd0d7cbc396b7a58e3a67af6c3100fee9fee765] (180,23 Mkey/s) [total: 4,190,109,696]
```
## Изминения:
- Полный рандом! Каждый хеш новый. 
- Файл gpu.cl нужен, без него не работает!
## Собрать проект
- Microsoft Visual Studio Community 2019
- OpenCL 1.2
## Donation
- BTC: bc1qh2mvnf5fujg93mwl8pe688yucaw9sflmwsukz9
