### PROVIDED AS IS, USE AT YOUR PERIL ###

* the script is a copy/paste modification of Ryan Faircloth's rsyslog-omsplunk
** https://bitbucket.org/rfaircloth-splunk/rsyslog-omsplunk
** http://www.rfaircloth.com/

Why?
Short answer: I couldn't get the original script to work for me so, I improvised. The primary difference is that the script runs an UDP listener and rsyslog is configured to filter an application's name and send those events to the port the script is listening on.

Performance note:
1. The application I was logging, was running 6 instances of the same daemon and altogether the log output was 260 EPS. I found quickly that the buffer size on the script just wasn't enough to handle that many events even when I used smaller batch sizes. I increased it 8x from 1024. Do all the performance testing you can before putting this into production.

Rsyslog hates you
It took a while before I could come up with a cleaner output from rsyslog using a template. The config relies on omfwd to output to another syslog server. omfwd is builtin to rsyslog but in case your version doesn't have it, uncomment the line that loads the module. Any app that can send to syslog on udp should work though.

NOTE: I didn't have control of the splunk instance I was sending to and the events where all bunched up into one event when indexed. The fix was to make sure the template in rsyslog had a line break at the end.
