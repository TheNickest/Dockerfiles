FROM --platform=linux/amd64 opensuse/leap:15

# Install necessary dependencies (passwd)
RUN zypper ref
RUN zypper -n in which nano tcsh uuidd unzip binutils gcc8
RUN zypper clean

# Change root password
#RUN echo -e "root\nroot" | passwd --stdin root
RUN passwd -q root | echo -e "root\nroot"

# start uuidd process, required by SAP Applications
#RUN chown uuidd /usr/share/bash-completion/completions/uuidd && 
#RUN /usr/sbin/uuidd
RUN systemctl enable uuidd

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

CMD ["/bin/bash"]