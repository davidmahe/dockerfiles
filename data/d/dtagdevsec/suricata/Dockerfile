FROM alpine  
  
# Include dist  
ADD dist/ /root/dist/  
  
# Install packages  
RUN apk -U upgrade && \  
apk add bash \  
ca-certificates \  
file \  
libcap \  
procps \  
wget && \  
apk -U add \--repository http://dl-cdn.alpinelinux.org/alpine/edge/community \  
suricata && \  
  
# Setup user, groups and configs  
addgroup -g 2000 suri && \  
adduser -S -H -u 2000 -D -g 2000 suri && \  
mv /root/dist/suricata.yaml /etc/suricata/suricata.yaml && \  
mv /root/dist/capture-filter.bpf /etc/suricata/capture-filter.bpf && \  
  
# Download the latest EmergingThreats ruleset, replace rulebase and enable all
rules  
cp /root/dist/update.sh /usr/bin/ && \  
chmod 755 /usr/bin/update.sh && \  
update.sh OPEN && \  
  
# Clean up  
rm -rf /root/* && \  
rm -rf /var/cache/apk/*  
  
# Start suricata  
CMD update.sh $OINKCODE && exec suricata -v -F /etc/suricata/capture-
filter.bpf -i $(/sbin/ip address | grep '^2: ' | awk '{ print $2 }' | tr -d
[:punct:])  

