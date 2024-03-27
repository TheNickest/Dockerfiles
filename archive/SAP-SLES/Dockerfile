FROM --platform=linux/amd64 registry.suse.com/suse/sle15:15.2 as repo-prep

# Install SAP dependencies
RUN zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Module-SAP-Applications/15-SP2/x86_64/product/ SLE-Module-SAP-Applications_product && \
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Module-SAP-Applications/15-SP2/x86_64/update/ SLE-Module-SAP-Applications_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Module-Basesystem/15-SP2/x86_64/product/ SLE-Module-Basesystem_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Module-Basesystem/15-SP2/x86_64/update/ SLE-Module-Basesystem_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Module-Containers/15-SP2/x86_64/product/ SLE-Module-Containers_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Module-Containers/15-SP2/x86_64/update/ SLE-Module-Containers_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Module-Development-Tools/15-SP2/x86_64/product/ SLE-Module-Development-Tools_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Module-Development-Tools/15-SP2/x86_64/update/ SLE-Module-Development-Tools_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Module-Legacy/15-SP2/x86_64/product/ SLE-Module-Legacy_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Module-Legacy/15-SP2/x86_64/update/ SLE-Module-Legacy_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Module-Packagehub-Subpackages/15-SP2/x86_64/product/ SLE-Module-Packagehub-Subpackages_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Module-Packagehub-Subpackages/15-SP2/x86_64/update/ SLE-Module-Packagehub-Subpackages_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Module-Server-Applications/15-SP2/x86_64/product/ SLE-Module-Server-Applications_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Module-Server-Applications/15-SP2/x86_64/update/ SLE-Module-Server-Applications_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Product-SLES/15-SP2/x86_64/product/ SLE-Product-SLES-15-SP2_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Product-SLES/15-SP2/x86_64/update/ SLE-Product-SLES-15-SP2_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Product-SLES_SAP/15-SP2/x86_64/product/ SLE-Product-SLES_SAP_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Product-SLES_SAP/15-SP2/x86_64/update/ SLE-Product-SLES_SAP_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Module-Public-Cloud/15-SP2/x86_64/product/ SLE-Module-Public-Cloud_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Module-Public-Cloud/15-SP2/x86_64/update/ SLE-Module-Public-Cloud_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Module-Web-Scripting/15-SP2/x86_64/product/ SLE-Module-Web-Scripting_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Module-Web-Scripting/15-SP2/x86_64/update/ SLE-Module-Web-Scripting_update && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Products/SLE-Product-HA/15-SP2/x86_64/product/ SLE-Product-HA_product && \ 
zypper ar https://repo.eu-nl-1.cloud.sap/suse/SUSE/Updates/SLE-Product-HA/15-SP2/x86_64/update/ SLE-Product-HA_update

# new stage, take all repos
FROM --platform=linux/amd64 registry.suse.com/suse/sle15:15.2

COPY --from=repo-prep /etc/zypp /etc/zypp

# refresh and update repos
RUN zypper ref -s && zypper update -y && zypper --gpg-auto-import-keys ref -s

# install dependencies (patterns-sap-nw or patterns-sap-hana)
RUN zypper in --force-resolution -y -n -t pattern devel_basis && \ 
zypper rm --force-resolution -y -n container-suseconnect
RUN zypper in -y bc chrony clamsap cryptctl expect libgtk-2_0-0 libicu60_2 libjpeg62 libpng12-0 libssh2-1 libyui-ncurses11 numactl patterns-sap-hana iputils vim

# Cleanup
RUN zypper clean

# Create folder
RUN mkdir /tmp/SAPEWM 

# Expose ports
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