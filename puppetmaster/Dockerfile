# Use phusion/baseimage as base image. To make your builds reproducible, make
# sure you lock down to a specific version, not to `latest`!
# See https://github.com/phusion/baseimage-docker/blob/master/Changelog.md for
# a list of version numbers.
FROM phusion/baseimage:0.9.11

# Use baseimage-docker's init system.
CMD ["/sbin/my_init"]


# ...put your own build instructions here...
RUN apt-get update && apt-get install -y \
  wget
RUN wget https://apt.puppetlabs.com/puppetlabs-release-trusty.deb
RUN dpkg -i puppetlabs-release-trusty.deb
RUN apt-get update && apt-get install -y \
  build-essential \
  ruby1.9.1 \
  ruby1.9.1-dev \
  git \
  puppetmaster-passenger
RUN gem install r10k
RUN rm /etc/puppet/puppet.conf
run rm /etc/apache2/sites-enabled/puppetmaster.conf
ADD r10k.yaml /etc/r10k.yaml
ADD puppet.conf /etc/puppet/puppet.conf
ADD puppetmaster.conf /etc/apache2/sites-enabled/puppetmaster.conf
RUN mkdir -p /var/lib/puppet

EXPOSE 22
EXPOSE 3000
EXPOSE 8080
EXPOSE 8081
EXPOSE 8140

VOLUME /var/lib/puppet

# Clean up APT when done.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
