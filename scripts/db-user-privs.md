## POSTGRES CREATE DB, USER, PRIVS
    CREATE DATABASE <<db>>;
    
    CREATE USER <<user>> WITH ENCRYPTED PASSWORD '<<pass>>';
    
    GRANT ALL PRIVILEGES ON DATABASE <<user>> TO <<db>>;

## MARIADB CREATE DB, USER, PRIVS
    CREATE DATABASE '<<db>>';
    
    SHOW DATABASES;
    
    CREATE USER '<<user>>'@mariadb IDENTIFIED BY '<<pass>>';
    
    SELECT User FROM mysql.user;
    
    GRANT ALL PRIVILEGES ON '<<db>>'.* TO '<<user>>'@mariadb;
    
    FLUSH PRIVILEGES;
    
    SHOW GRANTS FOR '<<user>>'@mariadb;