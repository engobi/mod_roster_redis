mod_roster_redis
================

ejabberd module to use Redis as rosters storage.

This module has been designed with focus on performance. Rosters are stored in a Redis hash, that uses the ``username`` as key and also content ``groups`` list, designed as following: 

```
{
    "rosterusers::username1": [
                                {"user2@server2": "nick2::subscription2::ask2::askmessage2::group2"},
                                {"user3@server3": "nick3::subscription3::ask3::askmessage3::group3,group1"},
                                {"user3@server4": "nick4::subscription4::ask4::askmessage4::group4"} ],
    "rosterusers::username2": [
                                {"user2@server2": "nick2::subscription2::ask2::askmessage2::group2"},
                                {"user5@server5": "nick5::subscription5::ask5::askmessage5::group5"},
                                {"user3@server4": "nick4::subscription4::ask4::askmessage4::group4,group3"} ]
}
```

### Compile

    $ erl -make

### Installation

Copy beams files from ``./ebin`` directory to ejabberd ebin directory (which is usualy: ``/usr/lib/ejabberd/ebin``)
        
    $ sudo ./ebin/*.beam /usr/lib/ejabberd/ebin/.
          
### Configuration

Add following line in your ``ejabberd.cfg`` file to configure mod_roster_redis 

    if your Redis is not in cluster mode

```
{mod_roster_redis,  [{redis_host, "localhost"}, {redis_port, 6379}, {redis_password, none|password}]},
```

    if your Redisis in cluster mode (it could be a good idea to write on master and to read on slave)
         
```
{mod_roster_redis,  [{redis_ro_host, "localhost"}, {redis_ro_port, 6379}, {redis_rw_host, "localhost"}, {redis_rw_port, 6379}, {redis_password, none|password}]},
```

### Dependencies
          
This module is compatible with ejabberd 2.1.x versions.
 
