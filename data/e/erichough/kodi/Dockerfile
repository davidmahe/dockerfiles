# ehough/docker-kodi - Dockerized Kodi with audio and video.  
#  
# https://github.com/ehough/docker-kodi  
# https://hub.docker.com/r/erichough/kodi/  
#  
# Copyright 2018 - Eric Hough (eric@tubepress.com)  
#  
# This program is free software: you can redistribute it and/or modify  
# it under the terms of the GNU General Public License as published by  
# the Free Software Foundation, either version 3 of the License, or  
# (at your option) any later version.  
# This program is distributed in the hope that it will be useful,  
# but WITHOUT ANY WARRANTY; without even the implied warranty of  
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the  
# GNU General Public License for more details.  
# You should have received a copy of the GNU General Public License  
# along with this program. If not, see <https://www.gnu.org/licenses/>.  
  
FROM ubuntu:bionic  
  
# install the team-xbmc ppa  
RUN apt-get update && \  
apt-get install -y --no-install-recommends software-properties-common && \  
add-apt-repository ppa:team-xbmc/ppa && \  
apt-get -y purge ca-certificates openssl software-properties-common && \  
apt-get -y --purge autoremove && \  
rm -rf /var/lib/apt/lists/*  
# install base packages  
RUN packages="kodi kodi-eventclients-xbmc-send" && \  
apt-get update && \  
apt-get install -y --no-install-recommends $packages && \  
apt-get -y --purge autoremove && \  
rm -rf /var/lib/apt/lists/*  
# setup entry point  
COPY entrypoint.sh /usr/local/bin  
ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]  
  
# install optional packages. do this last so we can cache the above layers
between branches  
RUN packages=" \  
kodi-pvr-argustv \  
kodi-pvr-dvblink \  
kodi-pvr-dvbviewer \  
kodi-pvr-hdhomerun \  
kodi-pvr-hts \  
kodi-pvr-iptvsimple \  
kodi-pvr-mythtv \  
kodi-pvr-nextpvr \  
kodi-pvr-njoy \  
kodi-pvr-octonet \  
kodi-pvr-pctv \  
kodi-pvr-vbox \  
kodi-pvr-vdr-vnsi \  
kodi-pvr-vuplus=*~bionic" && \  
apt-get update && \  
apt-get install -y --no-install-recommends $packages && \  
apt-get -y --purge autoremove && \  
rm -rf /var/lib/apt/lists/*  
# notes on the PVR packages:  
#  
# kodi-pvr-vuplus needs its version set to prevent the Debian package from
taking priority  
# kodi-pvr-mediaportal-tvserver can in installed once this issue [1] is fixed.  
# kodi-pvr-wmc can be installed once this PR [2] makes its way into the Team
XBMC PPA. See this issue [3] for details.  
#  
# [1] https://github.com/kodi-pvr/pvr.mediaportal.tvserver/issues/86  
# [2] https://github.com/kodi-pvr/pvr.wmc/pull/61  
# [3] https://github.com/kodi-pvr/pvr.wmc/issues/60  

