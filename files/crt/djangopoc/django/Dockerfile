FROM centos:centos7

WORKDIR /srv
RUN yum -y install python-virtualenv httpd mod_wsgi postgresql-devel gcc && virtualenv "{{ topdir }}"

WORKDIR /srv/{{ topdir }}
ADD . /srv/{{ topdir }}/{{ topdir }}
RUN source bin/activate && pip install -r "{{ topdir }}/requirements.txt"
RUN sed -i "s|@PATHS@|`find $(pwd) -type d -path '*lib/*/site-packages'`|" {{ topdir }}/{{ topdir }}.conf
RUN cp {{ topdir }}/{{ topdir }}.conf /etc/httpd/conf.d

EXPOSE 80
CMD /usr/sbin/httpd -DFOREGROUND