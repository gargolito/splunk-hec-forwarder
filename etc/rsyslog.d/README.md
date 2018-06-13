#how to troubleshoot rsyslog#
1. stop rsyslog daemon
1. export RSYSLOG_DEBUG="DebugOnDemand NoStdOut"
1. export RSYSLOG_DEBUGLOG=/usr/local/share/omsplunk/rsyslog.log
1. rsyslogd -n -d -f /etc/rsyslog.conf
1. from another screen, toggle debug on/off: kill -USR1 (pidof rsyslogd)
1. stop manually started rsyslog: kill $(pidof rsyslogd)
