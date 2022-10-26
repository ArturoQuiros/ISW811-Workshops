<VirtualHost \*:80>

ServerAdmin webmaster@lfts.isw811.xyz
ServerName lfts.isw811.xyz

# Indexes + Directory Root.

DirectoryIndex index.php index.html
DocumentRoot /home/vagrant/sites/lfts.isw811.xyz/public

<Directory /home/vagrant/sites/lfts.isw811.xyz/public>
DirectoryIndex index.php index.html
AllowOverride All
Require all granted
</Directory>

ErrorLog ${APACHE_LOG_DIR}/lfts.isw811.xyz.error.log

# Possible values include: debug, info, notice, warn, error, crit,

# alert, emerg.

LogLevel warn

CustomLog ${APACHE_LOG_DIR}/lfts.isw811.xyz.access.log combined
</VirtualHost>
