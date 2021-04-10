# dwm v6.2
## Instalar
    git clone https://github.com/phpbell/dwm.git && cd dwm && sh make

## Configurações
    nano config.h

## .profile

```bash
# resolve o bug de apps java
export _JAVA_AWT_WM_NONREPARENTING=1 

# bateria, memória, calendário e relógio
while true; do
    bat="$(acpi -b)"
    mem="$(free -h --si | awk '(NR==2){ print $3 }')"
    status="$(echo "$bat, Mem: $mem ~" && date +"%A, %d.%b.%Y %H:%M")"
    xsetroot -name " $(echo $status | xargs) "
    sleep 1s    # atualiza a cada 1 segundo
done &

# bateria, memória, calendário e relógio (versão PHP com CPU)
while true; do
    bat="$(acpi -b)"
    mem="$(free -h --si | awk '(NR==2){ print $3 }')"
    data="$(php /opt/home/www/html/data.php)"
    cpu="$(mpstat | awk '(NR==4){ print $4 }')"
    status="$(echo "$bat, CPU: $cpu%, Mem: $mem ~ $data")"
    xsetroot -name " $(echo $status | xargs) "
    sleep 1s    # atualiza a cada 1 segundo
done &

# alarme
setsid alarm-clock-applet &

# wallpaper
setsid nitrogen --restore &
