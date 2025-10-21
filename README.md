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

   <img width="180" height="28" alt="image" src="https://github.com/user-attachments/assets/52c54dfd-e384-4a2a-b09e-c2fd15e58f93" />

4. **Подключиться в foxglove**
   
   Для подключения выбрать в левом боковом меню *Open connection* и в разделе *ROS1* `http://ip_add:11311` заменить `ip_add` на ip дрона. см. [Настройка foxglove](#настройка-foxglove)

## Настройка foxglove
**В случае, если подключение уже было совершено и ip адрес не изменился, на стартовой странице Foxglove в разделе *Recently viewed* будет отображается последние подключения с сохраненными параметрами отображения.**
1. Для добавления виджетов в активную область используйте *Add panel*

   <img width="259" height="112" alt="image" src="https://github.com/user-attachments/assets/09c6dfd2-6bd5-48c7-932c-0bb5d4becd8e" />
2. Для отображения траектории в 2D в виджете *Plot* выставляем *X-axis value type*:**Message path** и устанавливаем следующие данные отображения

<img width="321" height="39" alt="image" src="https://github.com/user-attachments/assets/58e50d19-c80a-468f-9b59-53c8baf1e528" /> 

<img width="319" height="302" alt="image" src="https://github.com/user-attachments/assets/8cb31a0a-999a-4292-ae2d-4ead287d4808" /> <img width="510" height="473" alt="image" src="https://github.com/user-attachments/assets/7c51da13-6ea0-484b-ac22-31a9a1d78ae8" />

   Эти данные соответствуют следующему отображению по осям

2. Для отображения траектории в 3D в виждете *3D* выставляем следующие параметры

3. Для отображения выходных данных системы в виджете *Raw messages* можно подписаться на /udp
   
## Перезапуск

1. Для каждого последующего эксперимента необходимо калибровать его относительно начального положения.
2. Запуск автостарта занимает от 40 до 50 секунд.

## Сохранение траектории

Все траектории сохраняются в home/user/*.bag. Каждую траекторию можно отобразить повторно в Foxglove используя *Open file* на стартовой странице.
