FROM alpine  
RUN apk --no-cache add curl  
COPY scripts/opam-github-pr-diff /root/opam-github-pr-diff  
ENTRYPOINT ["/root/opam-github-pr-diff"]  

