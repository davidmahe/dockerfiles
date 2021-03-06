FROM telegraf:1.2-alpine  
  
ENV AGENT_INTERVAL="10s"  
ENV AGENT_ROUND_INTERVAL=true  
ENV AGENT_METRIC_BATCH_SIZE=1000  
ENV AGENT_METRIC_BUFFER_LIMIT=10000  
ENV AGENT_COLLECTION_JITTER="0s"  
ENV AGENT_FLUSH_INTERVAL="10s"  
ENV AGENT_FLUSH_JITTER="0s"  
ENV AGENT_FLUSH_PRECISION=""  
ENV AGENT_DEBUG=false  
ENV AGENT_QUIET=false  
ENV AGENT_LOGFILE="/dev/stderr"  
# ENV AGENT_HOSTNAME=""  
ENV AGENT_OMIT_HOSTNAME=false  
  
ENV OUTPUTS_INFLUXDB_URLS='["http://influxdb:8086"]'  
ENV OUTPUTS_INFLUXDB_DATABASE="telegraf"  
ENV OUTPUTS_INFLUXDB_RETENTION_POLICY="autogen"  
ENV OUTPUTS_INFLUXDB_WRITE_CONSISTENCY="any"  
ENV OUTPUTS_INFLUXDB_TIMEOUT="5s"  
ENV OUTPUTS_INFLUXDB_USERNAME=""  
ENV OUTPUTS_INFLUXDB_PASSWORD=""  
ENV OUTPUTS_INFLUXDB_USER_AGENT="telegraf"  
ENV OUTPUTS_INFLUXDB_UDP_PAYLOAD=512  
# ENV OUTPUTS_INFLUXDB_SSL_CA="/etc/telegraf/ca.pem"  
# ENV OUTPUTS_INFLUXDB_SSL_CERT="/etc/telegraf/cert.pem"  
# ENV OUTPUTS_INFLUXDB_SSL_KEY="/etc/telegraf/key.pem"  
ENV OUTPUTS_INFLUXDB_INSECURE_SKIP_VERIFY=false  
  
ENV INPUTS_DOCKER_ENDPOINT="unix:///var/run/docker.sock"  
ENV INPUTS_DOCKER_CONTAINER_NAMES='[]'  
ENV INPUTS_DOCKER_TIMEOUT="5s"  
ENV INPUTS_DOCKER_PERDEVICE=true  
ENV INPUTS_DOCKER_TOTAL=false  
  
ENV INPUTS_STATSD_DELETE_GAUGES=true  
ENV INPUTS_STATSD_DELETE_COUNTERS=true  
ENV INPUTS_STATSD_DELETE_SETS=true  
ENV INPUTS_STATSD_DELETE_TIMINGS=true  
ENV INPUTS_STATSD_PERCENTILES='[90]'  
ENV INPUTS_STATSD_METRIC_SEPARATOR="_"  
ENV INPUTS_STATSD_PARSE_DATA_DOG_TAGS=false  
ENV INPUTS_STATSD_TEMPLATES='[]'  
ENV INPUTS_STATSD_ALLOWED_PENDING_MESSAGES=10000  
ENV INPUTS_STATSD_PERCENTILE_LIMIT=1000  
  
ENV INPUTS_REDIS_SERVERS='["tcp://redis:6379"]'  
  
ENV INPUTS_CLOUDWATCH_REGION="us-east-1"  
ENV INPUTS_CLOUDWATCH_PERIOD="5m"  
ENV INPUTS_CLOUDWATCH_DELAY="5m"  
ENV INPUTS_CLOUDWATCH_INTERVAL="5m"  
ENV INPUTS_CLOUDWATCH_CACHE_TTL="1h"  
ENV INPUTS_CLOUDWATCH_NAMESPACE="AWS/ELB"  
ENV INPUTS_CLOUDWATCH_RATELIMIT=10  
  
COPY telegraf.conf /etc/telegraf/  

