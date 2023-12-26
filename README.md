# Recompile sqlsrv and pdo_sqlsrv for PHP 8.3

- Download the latest version of the driver from [sqlsrv](https://pecl.php.net/package/sqlsrv) and [pdo_sqlsrv](https://pecl.php.net/package/pdo_sqlsrv)

  ```bash
  wget https://pecl.php.net/get/sqlsrv-5.11.1.tgz
  wget https://pecl.php.net/get/pdo_sqlsrv-5.11.1.tgz
  ```

- Extract the files

  ```bash
  tar -xvf sqlsrv-5.11.1.tgz
  tar -xvf pdo_sqlsrv-5.11.1.tgz
  ```

- cd into the extracted directories

  ```bash
  cd sqlsrv-5.11.1
  cd pdo_sqlsrv-5.11.1
  ```

- Run

  ```bash
  phpize
  ```

- Run

  ```bash
  ./configure --with-php-config=/usr/bin/php-config8.3
  ```

  > Note: Make sure php 8.3 is installed. If not, run `sudo apt install php8.3-dev`

- Run

  ```bash
  make
  ```

- Run

  ```bash
  sudo make install
  ```

- Enable the extensions

  ```bash
  sudo su
  printf "; priority=20\nextension=sqlsrv.so\n" > /etc/php/8.3/mods-available/sqlsrv.ini
  printf "; priority=30\nextension=pdo_sqlsrv.so\n" > /etc/php/8.3/mods-available/pdo_sqlsrv.ini
  exit
  ```

  ```bash
  sudo phpenmod -v 8.3 sqlsrv pdo_sqlsrv
  ```

- Enable apache2 mods
  ```bash
  sudo apt install libapache2-mod-php8.3
  ```
  ```bash
    sudo a2dismod php8.1 // disable php8.1
    sudo a2enmod php8.3 // enable php8.3
    a2dismod mpm_event
    a2enmod mpm_prefork
  ```
- Restart apache2
  ```bash
  sudo service apache2 restart
  ```

# Set Default php version

```bash
sudo update-alternatives --config php
sudo update-alternatives --config phar
sudo update-alternatives --config phar.phar
sudo update-alternatives --config phpize
```
