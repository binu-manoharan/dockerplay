FROM ubuntu

#RUN mkdir -p /myfiles && touch /myfiles/nodename.txt
RUN mkdir /test

COPY index.html /test

#CMD echo `uname -n` > /myfiles/nodename.txt && /bin/bash
#CMD echo `uname -n` && /bin/bash
#CMD sed -i "s/HOSTNAME/$(uname -n)/" /test/index.html && /bin/bash
CMD /bin/bash
