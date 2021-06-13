FROM altera526/hadoop-base:3.3.0

# DataNode Web UI 응답 여부를 통해 Healthcheck
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3  CMD curl -f http://localhost:9864/ || exit 1

# volume으로 연결
RUN mkdir $HADOOP_HOME/dfs
RUN mkdir $HADOOP_HOME/dfs/data
VOLUME $HADOOP_HOME/dfs/data

ADD start.sh /start.sh
RUN chmod a+x /start.sh

# WebUI, 데이터전송
# (3.0) 9864 <---> (2.0) 50075
# (3.0) 9866 <---> (2.0) 50010
EXPOSE 9864 9866

CMD ["/start.sh"]