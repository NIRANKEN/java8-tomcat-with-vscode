FROM tomcat:8.5-jdk8-corretto
# workspaceをmountするディレクトリの作成
RUN mkdir /opt/project
# 使うツールを入れる
RUN yum -y update && \
  yum -y install maven tar gzip iputils wget

# warをdeployしたときに、libraryとDB接続情報を読めるようにする対応
RUN wget https://corretto.aws/downloads/latest/amazon-corretto-11-x64-linux-jdk.rpm
RUN yum -y localinstall amazon-corretto-11-x64-linux-jdk.rpm

# this is tomcat plugin fixed readableListening Error in https://github.com/NIRANKEN/vscode-tomcat
COPY --chown=644 files/vscode-tomcat-0.11.3.vsix /root/

# install maven 3.6.3
RUN wget https://dlcdn.apache.org/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
RUN tar xvf apache-maven-3.6.3-bin.tar.gz 
RUN cp -r apache-maven-3.6.3 /usr/local/apache-maven
RUN echo "export M2_HOME=/usr/local/apache-maven" >> ~/.bashrc 
RUN echo "export M2=$M2_HOME/bin" >> ~/.bashrc 
RUN echo "PATH=$M2:$PATH" >> ~/.bashrc 
RUN source ~/.bashrc 