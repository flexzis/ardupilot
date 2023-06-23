# AVES Autopilot
Используется Open-Source проект [Ardupilot](https://github.com/ArduPilot/ardupilot), модифицированный для возможности запуска на плате собственной разработки Royal Pinguin (в данном проекте hwdef для первой версии платы).

Для этого был создан файл hwdef (находится в libraries/AP_HAL_ChibiOS/hwdef/Pinguin0/), с описанием адресов шин и датчиков платы.


## Инструкция по установке автопилота на плату с ОС Ubuntu
### Инициализация репозитория
```
git clone https://github.com/flexzis/ardupilot.git
cd ardupilot
git submodule update --init --recursive
```

### Шаг 1: Сборка
```
./waf distclean
./waf configure --board Pinguin0
./waf plane
```
После этого должен появится файл arduplane_with_bl.hex в build/Pinguin0/bin.


### 	Шаг 2: Загрузка прошивки на плату 
(предварительно устанавливаем dfu-util: `sudo apt-get install dfu-util`)
```
dfu-util -a 0 --dfuse-address 0x08000000 -D ./build/Pinguin0/bi/arduplane_with_bl.hex
```

Проверить работоспособность можно через любую наземную станцию: MissionPlanner / QGC / MavProxy.
