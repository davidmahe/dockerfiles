## Image name: faucet/packet-fuzzer  
FROM faucet/test-base:latest  
  
ENV PIP="pip -q --no-cache-dir install --upgrade"  
ENV PIP3="pip3 -q --no-cache-dir install --upgrade"  
COPY ./ /faucet-src/  
WORKDIR /faucet-src  
  
RUN \  
apt-get update && \  
apt-get install -y afl cython3 && \  
$PIP -r fuzz-requirements.txt && \  
$PIP3 -r requirements.txt && \  
$PIP3 -r fuzz-requirements.txt && \  
$PIP3 .  
  
VOLUME ["/var/log/faucet/", "/var/log/afl/", "/etc/faucet/",
"/var/run/faucet/"]  
  
EXPOSE 6653 9302  
CMD ["docker/fuzz_packet.sh"]  

