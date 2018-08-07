.. _deployment_guide:

==============================
Best Practice Deployment guide
==============================

Introduction
============
In our `lab setup <http://tachyonic.org/sphinx/tachlab/development/index.html>`_ we illustrate a best practice deployment
of the Tachyonic Project echo system that results in a highly available, scalable implementation.

This page documents this setup in order to serve as a reference architecture.

Comming Soon
============
Stuff like

.. code:: bash

    mkdir /opt/tachyonic
    cd /opt/tachyonic
    git clone -b development https://github.com/TachyonicProject/luxon.git
    git clone -b development https://github.com/TachyonicProject/psychokinetic.git
    git clone -b development https://github.com/TachyonicProject/photonic.git
    git clone -b development https://github.com/TachyonicProject/infinitystone.git

    cd /opt/tachyonic/luxon
    pip3 install .
    cd /opt/tachyonic/psychokinetic
    pip3 install .
    cd /opt/tachyonic/photonic
    pip3 install .
    cd /opt/tachyonic/infinitystone
    pip3 install .

    cd /var/www
    mkdir infinitystone
    luxon -i infinitystone infinitystone

    luxon -d infinitystone
    chown -R www-data:www-data infinitystone
    chmod 770 infinitystone/sqlite3.db
    luxon -r infinitystone

    mkdir photonic
    luxon -i photonic photonic
    ln -s ../infinitystone/public.pem  photonic/public.pem
    ln -s /opt/tachyonic/photonic/photonic/static /var/www/html/static

    chown -R www-data:www-data infinitystone
    chown -R www-data:www-data photonic
    chown -R www-data:www-data /opt/tachyonic/photonic

    cp 000-default.conf /etc/apache2/sites-available/

    service apache2 start && tail -f /var/log/apache2/error.log

