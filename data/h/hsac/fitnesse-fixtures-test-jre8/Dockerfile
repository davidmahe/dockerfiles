ARG BASE_VERSION=base-latest  
ARG JRE_VERSION=8-jre-alpine  
  
FROM hsac/fitnesse-fixtures-test-jre8:${BASE_VERSION} as base  
  
FROM openjdk:${JRE_VERSION}  
RUN mkdir -p /fitnesse/wiki/fixtures/nl/hsac/fitnesse  
  
WORKDIR /fitnesse  
  
RUN mkdir target  
VOLUME /fitnesse/target  
  
RUN mkdir wiki/FitNesseRoot  
VOLUME /fitnesse/wiki/FitNesseRoot  
  
COPY runTests.sh .  
COPY htmlReportIndexGenerator.sh .  
  
ENTRYPOINT ["/fitnesse/runTests.sh"]  
CMD []  
  
COPY \--from=base /usr/src/test/wiki wiki/

