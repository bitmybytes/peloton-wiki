## Remote Access to Peloton

To configure Peloton for remote access,

1. Add a new rule to `$DB_DIR/pg_hba.conf` to allow remote connection from certain hosts, ex:

   `host all all 192.168.0.0/24 trust`

   The above rule grants access rights to the hosts from `192.168.0.0/24`.

2. Modify one of the connection settings in `postgresql.conf`. 

   `listen_addresses = '*'`
   
   You can find more information in the [Connections and Authentication](http://www.postgresql.org/docs/9.0/static/runtime-config-connection.html) section.

