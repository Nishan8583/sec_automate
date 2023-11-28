# Using the debian official image
FROM debian

# Install curl
RUN apt update -y && apt install curl python3 git build-essential nmap wget ffuf smbclient gobuster dirsearch dnsutils ldap-utils -y

# Install rust for rustscan
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs > install.rs && chmod +x install.rs && ./install.rs -y

RUN pwd && ls /home/
# Install rustscan
RUN bash -c 'source "$HOME/.cargo/env" && git clone https://github.com/RustScan/RustScan.git && cd RustScan && cargo build --release && cp ./target/release/rustscan /usr/local/bin'

# Install go
RUN wget https://go.dev/dl/go1.21.4.linux-amd64.tar.gz &&  rm -rf /usr/local/go && tar -C /usr/local -xzf go1.21.4.linux-amd64.tar.gz && export PATH=$PATH:/usr/local/go/bin && go version

# Adding path
RUN echo "PATH=$PATH:/usr/local/go/bin:~/go/bin" >> ~/.bashrc

# Install nuclei
RUN /usr/local/go/bin/go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest

# Install mage
RUN git clone https://github.com/ropnop/windapsearch.git
RUN apt-get install python3-pip -y
RUN apt install python3-ldap -y
RUN cp windapsearch/windapsearch.py /usr/local/bin/

# Install impacket
RUN apt install pipx -y
RUN pipx ensurepath && pipx install impacket

RUN mkdir /priv_check

RUN git clone https://github.com/CiscoCXSecurity/enum4linux.git && cp enum4linux/enum4linux.pl /priv_check/

RUN wget https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh && cp linpeas.sh /priv_check/
