FROM node:slim  
  
RUN npm install -g slackin  
  
CMD slackin \  
\--coc "$SLACK_COC" \  
\--channels "$SLACK_CHANNELS" \  
\--port "$PORT" \  
"$SLACK_SUBDOMAIN" \  
"$SLACK_API_TOKEN"  

