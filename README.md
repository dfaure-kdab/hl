hl : a colorization command
===========================

Purpose
-------
This command uses regcomp() and regexec() to colorize (highlight)
strings from stdin using options on the command line.

Standard system commands can be colorized without having to change their syntax nor having to manually pipe their output to the `hl`command, using the `hl_generic` script.

`hl` can use up to 42 colors :

![hl_colors](https://github.com/mbornet-hl/hl/blob/master/images/hl_colors.png)

Here is a [review](https://connect.ed-diamond.com/Linux-Pratique/LP-093/Colorisez-vos-textes-avec-la-commande-hl) about `hl` in a french magazine (Linux Pratique).

Usage
-----

```
hl: version 1.67
Usage: hl [-h|-H|-V|-[[%.]eiuvdDEL1234][-[rgybmcwRGYBMCWn] regexp ...][--config_name ...] ]
  -h  : help
  -H  : help + configuration names
  -V  : version
  -v  : verbose
  -u  : do not bufferize output on stdout
  -e  : extended regular expressions
  -i  : ignore case
  -E  : print on stderr
  -r  : red
  -g  : green
  -y  : yellow
  -b  : blue
  -m  : magenta
  -c  : cyan
  -w  : white
  -R  : red     (reverse video)
  -G  : green   (reverse video)
  -Y  : yellow  (reverse video)
  -B  : blue    (reverse video)
  -M  : magenta (reverse video)
  -C  : cyan    (reverse video)
  -W  : white   (reverse video)
  -n  : never colorize
  -%c : specifies the beginning of a range colorized in color 'c'
  -.  : specifies the end of the previous range
  -d  : debug
  -D  : display regular expressions
  -L  : lex debug
  -1  : color brightness (half-bright)
  -2  : color brightness (normal : default)
  -3  : color brightness (bright)
  -4  : color brightness (underscore)
  Configurations :
    --acl
    --apt
    --C
    --cal
    --colors
    --colors42
    --color_names
    --df
    --diff
    --dpkg-query
    --err
    --eth
    --ethtool
    --eth_VIP
    --fail2ban
    --fdisk
    --free
    --ha_log
    --heartbeat
    --hl
    --hl_usage
    --hosts
    --ifconfig
    --IP
    --ip
    --iptables
    --ls_doc
    --MAC
    --man
    --namei
    --netstat
    --passwd
    --percent
    --ps_cpu
    --rev_color_names
    --samba
    --sep3
    --services
    --show_disks
    --tcpdump
    --validate_IP
    --virsh_list
    --w
    --xxd
    --za0
    --za_conf
    --alpha
    --beta
    --alphabeta
    --alpha2
    --beta
    --alphabeta
    --alphabeta2
    --col_dupl
    --free_used_swap
    --swap
    --p
    --test
    --hi_red
    --hi_green
    --hi_yellow
    --hi_blue
    --hi_magenta
    --hi_cyan
    --hi_white
    --dim_red
    --dim_green
    --dim_yellow
    --dim_blue
    --dim_magenta
    --dim_cyan
    --dim_white
    --red
    --green
    --yellow
    --blue
    --magenta
    --cyan
    --white
    --file
    --sql
    --quote1
    --quote2
    --html
    --ref_list
    --apt-get
    --cal
    --chkconfig
    --df
    --diff
    --dpkg-query
    --dmidecode
    --ethtool
    --fdisk
    --free
    --ifconfig
    --iostat
    --iptables
    --man
    --mpg123
    --namei
    --netstat
    --objdump
    --ps
    --smartctl
    --strace
    --stty
    --tcpdump
    --w
    --xxd
    --acl
    --C
    --colors
    --colors42
    --color_names
    --err
    --eth
    --eth_VIP
    --fail2ban
    --ha_log
    --heartbeat
    --hl
    --hl_conf
    --hl_usage
    --hosts
    --IP
    --ip
    --jigdo
    --ls_doc
    --MAC
    --on-off
    --passwd
    --passwd_chk
    --percent
    --ps_cpu
    --ps_cpu_time
    --rev_color_names
    --samba
    --sep3
    --services
    --sh
    --show_disks
    --validate_IP
    --virsh_list
    --hi_red
    --hi_green
    --hi_yellow
    --hi_blue
    --hi_magenta
    --hi_cyan
    --hi_white
    --dim_red
    --dim_green
    --dim_yellow
    --dim_blue
    --dim_magenta
    --dim_cyan
    --dim_white
    --red
    --green
    --yellow
    --blue
    --magenta
    --cyan
    --white
```

Examples
--------

```
/sbin/ifconfig -a | hl -ei -m '^(eth|(vir)?br|vnet)[0-9.]*:[0-9]+\>'       \
			 -b '^(eth|(vir)?br|vnet)[0-9.]*\.[0-9]+\>'             \
			 -c '([0-9a-f]{2}:){5}[0-9a-f]{2}'                      \
			 -g '\<UP\>|\<RUNNING\>|([0-9]{1,3}\.){3}[0-9]{1,3}\>'  \
			 -y '^(eth|(vir)?br|vnet)[0-9.:]*\>'

/sbin/ifconfig -a | hl --ifconfig

/sbin/ifconfig -a | hl --IP --MAC --eth

cat firewall_rules | hl -e -c INPUT                    \
				   -y 'FORWARD|POSTROUTING'    \
				   -b '#.*'                    \
				   -W 'OUTPUT'                 \
				   -g '.*ACCEPT.*'             \
				   -r '.*(DROP|REJECT).*'      \
				   -m 'iptables.*-F.*'         \
				   -w '^iptables .*'

cat firewall_rules | hl --iptables

df -h | hl --df
```
![df](https://github.com/mbornet-hl/hl/blob/master/images/df.png)

```
fdisk -l | hl --fdisk

```
![fdisk](https://github.com/mbornet-hl/hl/blob/master/images/fdisk.png)
