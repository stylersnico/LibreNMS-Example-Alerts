# LibreNMS Example Alerts

Based on the work of zimmertr/LibreNMS-Example-Alerts


## Included alerts 

_This table holds all of my LibreNMS alerts._

| # | Name | Rule | Severity | Extra |
| - | ---- | ---- | -------- | ----- |
| 1 | CPU usage > 95% for 15 minutes. | processors.processor_usage >= 95 | warning | Max: 1 Delay: 60 Interval: 900 |
| 2 | Host has been down for 10 minutes. | macros.device_down = 1 | critical | Max: 1 Delay: 60 Interval: 600 |
| 3 | Host has been rebooted. | devices.uptime < 300 AND macros.device = 1 | warning | Max: 1 Delay: 60 Interval: 300 |
| 4 | Host has not been polled within the last day. | devices.last_polled >= 86400 | critical | Max: 1 Delay: 60 Interval: 300 |
| 5 | Memory usage > 95% for 5 minutes. | mempools.mempool_perc >= 95 | warning | Max: 1 Delay: 60 Interval: 300
| 6 | Network usage > 80% for 5 minutes. | %macros.port_usage_perc >= "80" | ok | Max: 1 Delay: 60 Interval: 600 |
| 7 | Root filesystem has less than 5% free space available. | storage.storage_descr = "/" AND storage.storage_perc >= 95 | critical | Max: 1 Delay: 60 Interval: 300 |
| 8 | 	Service up/down | services.service_status != 0 AND macros.device_up = 1 | warning | Max: 1 Delay: 60 Interval: 300 |
| 9 | Host has entered a Warning state. | %services.service_status = "1" | warning | Max: -1 Delay: 300 Interval: 300 | 
| 10 | Host has entered a Critical state. | %services.service_status = "2" | critical | Max: -1 Delay: 300 Interval: 300 | 


## Telegram HTML Alert Template

_LibreNMS allows you to customize the alert message that is sent to your transport endpoint. The following is my default message. I did not bother with additional templates._

**Alert Title:** `LibreNMS ({{ $alert->hostname }}) - NEW ALERT`    
**Recovery Title:** `LibreNMS ({{ $alert->hostname }}) - END OF ALERT`  
**Alert Body:**  
```
<b><i><u>{{ $alert->title }}</u></i></b>

@if ($alert->state == 0)<b><u>Duration:</u></b> {{ $alert->elapsed }} @else <b><u>Severity:</u></b> {{ $alert->severity }} @endif

<b><u>Rule:</u></b> @if ($alert->name) {{ $alert->name }} @else {{ $alert->rule }} @endif

@if ($alert->faults)<b><u>Faults:</u></b>
@foreach ($alert->faults as $key => $value)
  {{ $key }}: {{ $value['string'] }}
@endforeach
@endif

<b>---------------------------</b>
<b><u>Timestamp:</u></b> {{ $alert->timestamp }}
<b><u>Uptime:</u></b> {{ $alert->uptime_long }}
```

## Alert Example 

_The following is a screenshot of my telegram bot displaying a test alert_

![](https://raw.githubusercontent.com/stylersnico/LibreNMS-Example-Alerts/master/alerting.jpg)
