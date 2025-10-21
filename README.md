# Инструкция по работе с системой взаимного позиционирования дронов

## Оглавление

- [Включение](#включение)
- [Настройка foxglove](#настройка-foxglove)
- [Перезапуск](#перезапуск)
- [Сохранение траектории](#сохранение-траектории)

---
## Включение

1. **Подключение к сети wifi**
2. **Подключение SSH к NUC**
   Подключиться к NUC через `ssh user@ip_add` и `ssh aias@ip_add`.
   В случае изменения ip адрессов необходимо внести правки в файл `aias@aias-nuc:~$ nano ws_super/src/maestro/scripts/run.sh` в строки:
   ```
   10   export ROS_MASTER_URI=http://10.16.104.224:11311
   11   export ROS_IP=10.16.104.224
   82   tmux send-keys -t ${SESSION}:7.0 "export ROS_MASTER_URI=http://10.16.104.224:11311 && export ROS_IP=10.16.104.224 && ${INIT_ODOM} && ${RUN_ODOMETRY_READER}" Enter
   85   tmux send-keys -t ${SESSION}:8.0 "export ROS_MASTER_URI=http://10.16.104.224:11311 && export ROS_IP=10.16.104.224 && ${INIT_ODOM} && ${RUN_UDR_TEMP_SENDER}" Enter
   ```
   или в файл `user@flighter:~$ nano mars/ws_super/src/maestro/scripts/run.sh` в строки:   
   ```
   10   export ROS_MASTER_URI=http://10.16.105.57:11311
   11   export ROS_IP=10.16.105.57
   71   tmux send-keys -t ${SESSION}:10.0 "export ROS_MASTER_URI=http://10.16.105.57:11311 && export ROS_IP=10.16.105.57 && ${INIT_ODOM} && ${RUN_ODOMETRY_READER}" Enter
   74   tmux send-keys -t ${SESSION}:11.0 "export ROS_MASTER_URI=http://10.16.105.57:11311 && export ROS_IP=10.16.105.57 && ${INIT_ODOM} && ${RUN_UDR_TEMP_SENDER}" Enter
   ```
3. **Проверить включение всех автостартов**
   Для проверки работы всех автостартов следует использовать команду `tmux attach` и проверить работу во вкладках *init* и *resp*.
   
   <img width="180" height="28" alt="image" src="https://github.com/user-attachments/assets/1b9ba6e5-bab9-4827-bf26-7ebd12cccdac" />

5. **Подключиться в foxglove**
   см. [Настройка foxglove](#настройка-foxglove)

## Настройка foxglove
**В случае, если подключение уже было совершено и ip адрес не изменился, на стартовой странице Foxglove в разделе *Recently viewed* будет отображается последние подключения с сохраненными параметрами отображения.**
1. Для добавления виджетов в активную область используйте *Add panel*

   <img width="337" height="483" alt="image" src="https://github.com/user-attachments/assets/b85311ac-fbdb-4303-9256-effb95b05d46" />
2. Для отображения траектории в 2D в виджете *Plot* выставляем *X-axis value type*:**Message path** и устанавливаем следующие данные отображения
<img width="328" height="311" alt="image" src="https://github.com/user-attachments/assets/4a42f836-4688-4868-8d05-61cce171c2c9" />
<img width="510" height="473" alt="image" src="https://github.com/user-attachments/assets/223188c7-94ba-4da7-919b-898be72237d7" />

   Эти данные соответствуют следующему отображению по осям

3. Для отображения траектории в 3D в виждете *3D* выставляем следующие параметры

4. Для отображения выходных данных системы в виджете *Raw messages* можно подписаться на /udp
   
## Перезапуск

1. Для каждого последующего эксперимента необходимо калибровать его относительно начального положения.
2. Запуск автостарта занимает от 40 до 50 секунд.

## Сохранение траектории

Все траектории сохраняются в home/user/*.bag. Каждую траекторию можно отобразить повторно в Foxglove используя *Open file* на стартовой странице.
