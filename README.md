# rsysloging
на сервере
nano /etc/rsyslog.conf
расхешить 2 строки imudp
в конце файла
if $fromhost-ip contains '192.168.30.2' then /opt/log/br-srv/log.log
if $fromhost-ip contains '192.168.30.1' then /opt/log/br-rtr/log.log
if $fromhost-ip contains '192.168.100.1' then /opt/log/hq-rtr/log.log
рестартим
nano /etc/logrotate.d/rsyslog
/opt/log/br-srv/log.log
/opt/log/br-rtr/log.log
/opt/log/hq-rtr/log.log
{
weekly
compress
minsize 10M
}

на клиентах
*.warn @hq-srv:514
рестартим
на hq-rtr -> rsyslog host 192.168.100.2 port 514
На br-rtr -> rsyslog host 192.168.100.2 source 192.168.30.1 port 514
