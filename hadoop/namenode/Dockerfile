# hadoop base 이미지
FROM altera526/hadoop-base:3.3.0

# NameNode Web UI 응답 여부를 통한 healthcheck
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 CMD curl -f http://localhost:9870/ || exit 1

# 설정 파일 복제
ADD hdfs-site.xml $HADOOP_HOME/etc/hadoop/hdfs-site.xml

# FsImage, EditLog 파일 경로를 volume으로 연결
RUN mkdir $HADOOP_HOME/dfs
RUN mkdir $HADOOP_HOME/dfs/name
VOLUME $HADOOP_HOME/dfs/name

# 실행 스크립트 복제
ADD start.sh /start.sh
RUN chmod a+x /start.sh

# NameNode의 HTTP, IPC 포트 노출
# (3.0) 9870 <---> (2.0) 50070
# (3.0) 9820 <---> (2.0) 8020
EXPOSE 9870 9000

# 시작 명령어
CMD ["/start.sh", "/usr/local/hadoop/dfs/name"]
