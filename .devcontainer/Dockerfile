ARG IMG_URL
FROM ${IMG_URL}
RUN mkdir -p /workspace
ENV DEBIAN_FRONTEND=noninteractive
ARG USERNAME
RUN useradd -m ${USERNAME} \
&& apt-get update \
&& apt-get install -y sudo \
&& echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
&& chmod 0440 /etc/sudoers.d/$USERNAME
RUN DEBIAN_FRONTEND=noninteractive apt-get update -y &&  DEBIAN_FRONTEND=noninteractive apt-get install -q -y libpam-ldap libnss-ldap ldap-auth-client ldap-auth-config libnet-ldap-perl iputils-ping zsh telnet
RUN DEBIAN_FRONTEND=noninteractive apt-get install -q -y  sudo \
git \
curl \
vim \
ldap-utils \
libnss-ldap \
libpam-ldap \
nscd \
&& rm -rf /var/lib/apt/lists/*
RUN echo 'base cn=users,dc=nas-admin,dc=nota,dc=ai \n\
uri ldap://nas-admin.nota.ai/ \n\
ldap_version 3 \n\
binddn uid=ldap_client,cn=users,dc=nas-admin,dc=nota,dc=ai \n\
bindpw zI4TjZdIaLE \n\
pam_password md5 \n\
nss_base_passwd cn=users,dc=nas-admin,dc=nota,dc=ai \n\
nss_base_group cn=groups,dc=nas-admin,dc=nota,dc=ai' > /etc/ldap.conf
RUN echo 'zI4TjZdIaLE' > /etc/ldap.secret
RUN echo 'passwd: ldap \n\
group: ldap \n\
shadow: ldap \n\
gshadow: ldap \n\
 \n\
hosts:          files mdns4_minimal [NOTFOUND=return] dns \n\
networks:       files \n\
 \n\
protocols:      db files \n\
services:       db files \n\
ethers:         db files \n\
rpc:            db files \n\
 \n\
netgroup:       nis' > /etc/nsswitch.conf 
RUN     echo "session required pam_mkhomedir.so skel=/etc/skel umask=0022" >> /etc/pam.d/common-session
RUN service nscd start
WORKDIR /workspace