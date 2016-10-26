from	ubuntu:14.04
RUN	echo 'deb http://us.archive.ubuntu.com/ubuntu/ trusty universe' >> /etc/apt/sources.list
RUN	apt-get -y update

# Install required packages
RUN	apt-get -y install python-ldap python-cairo python-django python-twisted python-django-tagging python-simplejson python-memcache python-pysqlite2 python-support python-tz python-pip gunicorn supervisor nginx-light
RUN	pip install whisper==0.9.15
RUN	pip install --install-option="--prefix=/var/lib/graphite" --install-option="--install-lib=/var/lib/graphite/lib" carbon==0.9.15
RUN	pip install --install-option="--prefix=/var/lib/graphite" --install-option="--install-lib=/var/lib/graphite/webapp" graphite-web==0.9.15

# ADD system service config
ADD	./nginx/nginx.conf /etc/nginx/nginx.conf
ADD	./supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Graphite setup
ADD	./initial_data.json /var/lib/graphite/webapp/graphite/initial_data.json
ADD	./local_settings.py /var/lib/graphite/webapp/graphite/local_settings.py
ADD	./carbon.conf /var/lib/graphite/conf/carbon.conf
ADD	./storage-schemas.conf /var/lib/graphite/conf/storage-schemas.conf
RUN	mkdir -p /var/lib/graphite/storage/whisper
RUN	touch /var/lib/graphite/storage/graphite.db /var/lib/graphite/storage/index
RUN	chown -R www-data /var/lib/graphite/storage
RUN	chmod 0775 /var/lib/graphite/storage /var/lib/graphite/storage/whisper
RUN	chmod 0664 /var/lib/graphite/storage/graphite.db
RUN	cd /var/lib/graphite/webapp/graphite && python manage.py syncdb --noinput

# Nginx
expose	80
# Carbon
expose	2003
# Carbon UDP
expose	2003/udp
# Carbon pickle
expose	2004
# Carbon cache query
expose	7002
