# prepare for unrar installation
##FROM --platform=linux/amd64 oraclelinux:8-slim as prep

##RUN microdnf install yum

##RUN yum check-update -y || { rc=$?; [ "$rc" -eq 100 ] && exit 0; exit "$rc"; } && \
##yum update -y && \
##yum install wget -y && \
##yum clean all 

##RUN wget https://www.rarlab.com/rar/rarlinux-x64-622.tar.gz
##RUN tar -zxvf rarlinux-x64-622.tar.gz
##RUN cp -rv /rar/rar /bin && \
##cp -rv /rar/unrar /bin 

# base build stage
FROM --platform=linux/amd64 oraclelinux:7-slim

##COPY --from=prep /bin /bin

# ol8 and ol9 slim versions don't come with yum but microdnf only
###RUN microdnf install yum

# Install necessary dependencies (libnsl.x86_64)
RUN yum check-update -y || { rc=$?; [ "$rc" -eq 100 ] && exit 0; exit "$rc"; } && \
yum update -y
RUN yum install which passwd binutils nano tcsh uuidd unzip oracle-database-preinstall-19c -y && \
yum clean all

# Change root password
RUN echo -e "root\nroot" | passwd --stdin root

# start uuidd process, required by SAP Applications (different path for 7-slim)
###RUN chown uuidd /var/run/uuidd && /usr/sbin/uuidd
RUN chown uuidd /var/uuidd && /usr/sbin/uuidd

# Create folder
RUN mkdir /tmp/SAPEWM 

#  Expose ports
EXPOSE 1129
EXPOSE 3200
EXPOSE 3300
EXPOSE 4237
EXPOSE 8000
EXPOSE 8443
EXPOSE 30213
EXPOSE 44300
EXPOSE 50000
EXPOSE 50001