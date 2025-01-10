# Jira-License Confluence-License attlassian-License

## tested on all attlassian Products + Plugins + everything

basically you just need the agent file to genereate a license code <br><br>

### sample Docker file

```
FROM atlassian/jira-software:latest
USER root

# Add agent file
COPY atlassian-agent.jar /opt/atlassian/jira/

# Add agent to env
RUN echo 'export CATALINA_OPTS="-javaagent:/opt/atlassian/jira/atlassian-agent.jar ${CATALINA_OPTS}"' >> /opt/atlassian/jira/bin/setenv.sh
```

same thing works for confluence

```
FROM atlassian/confluence
USER root

# Add agent to env
COPY atlassian-agent.jar /opt/atlassian/confluence/

# Set Startup Loading Agent Package
RUN echo 'export CATALINA_OPTS="-javaagent:/opt/atlassian/confluence/atlassian-agent.jar ${CATALINA_OPTS}"' >> /opt/atlassian/confluence/bin/setenv.sh
```

then just build and use <br>

you can use the same file to generate license code like below for any product or plugin you want

```
java -jar atlassian-agent.jar --help

# products
java -jar atlassian-agent.jar -d -m [Email] -n BAT -p [conf or jira] -o http://[serverip-or-domain] -s [serverId]

# plugins
java -jar atlassian-agent.jar -d -m [Email] -n BAT -p [plugin code] -o http://[serverip-or-domain] -s [serverId]
```
