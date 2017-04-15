# emqtt

Refer to [original repository here](https://github.com/emqtt/emqttd), this is my forked version to add more functionalities.

## Whats new in this ?

I added the functionality of pushing the incoming PUBLISH messages to the PGSQL database.

## Any dependencies ?

Yeah, [epgsql_poolboy](https://github.com/thechamp/epgsql_poolboy). I have already added this in the Makefile, so it will be compiled automatically when you build this repository.

## How to use it?

1. Clone the EMQ release project
```
git clone https://github.com/emqtt/emq-relx.git
```

2. Open **emq-relx/Makefile** and change emqttd dependency code download url to my repository's url, i.e. change
```
dep_emqttd        = git https://github.com/emqtt/emqttd master
```
to
```
dep_emqttd        = git https://github.com/thechamp/emqttd master
```

3. Make the repository
```
cd emq-relx && make
```

4. Follow the instruction on [epgsql_poolboy](https://github.com/thechamp/epgsql_poolboy) README file to configure PGSQL connection variables.

5. Create a table in pgsql database to save the incoming data. This is the schema
```
create table mqtt_publish (
    client_id char(100),
    ip_port char(25),
    username char(100),
    topic char(100),
    payload text,
    qos char(5),
    retain char(5)
);
```
