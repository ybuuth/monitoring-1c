# На внедрении:
## 1.Проверить время сервера UTC. 
Установить его в .\promtail\conf\promtail-local-config.yaml

      -regexp
      template: '{{ $val := .filename | regexFind "[1-9][0-9][0-1][0-9][0-3][0-9][0-2][0-9]" }}20{{ $val | substr 0 2 }}-{{ $val | substr 2 4 }}-{{ $val | substr 4 6 }}T{{ $val | substr 6 8 }}:{{ .time }}+04:00'

где 04:00 заменить на время по UTC например для мск - 03:00
## 2.Настроить пути для сбора логов с технологического журнала. 
Заменить в .\promtail\conf\promtail-local-config.yaml:
      
      labels:
      job: test_logs
      __path__: var/log/bf-log/*log

  Также заменить настройки хранения таких логов в compose.yaml

      volumes:
      # копируем логи
      - D:/work_logs/promtail:/var/log # реальный путь к логам: D:\work_logs\promtail\bf-log\*.log
      - C:/work_logs:/var/log/work_log

  на Ваши пути
## 3.Сбор метрик железа с помощью "WMI exporter"
В процессе. Пока отсутствует. Прометеус будет ругаться что служба WMI exporter недоступна. Не обращать внимание