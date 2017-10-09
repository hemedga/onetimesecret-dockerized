# Things to configure


## edit onetime.conf

- add sendgrid or SMTP credentials
- modify the :limits: config
- the 'incoming' config, if you want onetimesecret to receive secrets



## edit redis.conf

- use the password you want
- use a TCP socket, if you like



# Actually build this

Just cd to this project directory and run

    docker build -t onetimesecret .


# Inspect and screw around

    run -it onetimesecret:latest /bin/bash


# Actually run this

    docker run -d -p 80:80 onetimesecret



# TODO:

- log to stdout/stderr (redis.conf and...somehow...the ruby app?)
- where/why is port 7143 getting hardcoded on the website? It's in all the nav links.



## Upgrade to newer versions of Ruby
FIX with newer versions of ruby (2.3) + up-to-date gems:

    RUN sed -i "s|require 'gibbler'|require 'gibbler/mixins'|g" /root/onetimesecret/lib/onetime.rb
    RUN rm Gemfile.lock && bundle install --without dev


## redis unix sockets not supported?
NoMethodError: undefined method serverid for #<URI::Generic:0x00000000032a3a98>


## run as a separate 'ots' user?
- use ots' $HOME as the WORKDIR?
- RUN chown ots /etc/onetime /var/log/onetime /var/run/onetime /var/lib/onetime
