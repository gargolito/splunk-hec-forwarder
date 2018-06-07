# PROVIDED AS-IS, USE AT YOUR PERIL #

* the script is a copy/paste modification of Ryan Faircloth's rsyslog-omsplunk
* https://bitbucket.org/rfaircloth-splunk/rsyslog-omsplunk
* http://www.rfaircloth.com/

### Why? ###
Short answer: I couldn't get the original script to work for me so, I improvised.

### What's different? ###
The script runs an UDP listener and rsyslog is configured to filter an application's name and send those events to the port the script is listening on. I can't see any reason this wouldn't work for all of syslog.

### Performance note: ###
The application I was logging, was running 6 instances of the same daemon and altogether the log output was around 260 EPS. I found quickly that the buffer size on the script just wasn't enough to handle that many events even when I used smaller batch sizes. I increased it 8x from 1024 and that "fixed it". I don't like it but I intend to continue to make improvements. Do all the performance testing you can before putting this into production.

### Rsyslog hates you ###
It took a while before I could come up with a cleaner output from rsyslog using a template. The config relies on omfwd to output to another syslog server. omfwd is builtin to rsyslog but in case your version doesn't have it, uncomment the line that loads the module. Any app that can send to syslog on udp should work though.

#### NOTE: ####
I didn't have control of the splunk instance I was sending events to and the events where all bunched up into one event when indexed. The fix was to make sure the template in rsyslog had a line break at the end.

### Future Improvements ###
I could use some pointers, feel free to fork and do pull requests, etc...