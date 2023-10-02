> https://github.com/datavane/datasophon/releases/download/v1.2.0/datasophon-manager-1.2.0.tar.gz
> yum install mysql-server
>  dnf -y install java-1.8.0-openjdk java-1.8.0-openjdk-devel
'''bash
cat > /etc/profile.d/java.sh <<'EOF'
export JAVA_HOME=$(dirname $(dirname $(readlink $(readlink $(which java)))))
export PATH=$PATH:$JAVA_HOME/bin
EOF
'''
> source /etc/profile.d/java.sh
> https://www.server-world.info/en/note?os=CentOS_Stream_9&p=java&f=1

> /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.151-5.b12.el7_4.x86_64/jre/bin/java

>  yum install -y java-1.8.0-openjdk*
> vim /etc/profile

> https://timberkito.com/?p=12
