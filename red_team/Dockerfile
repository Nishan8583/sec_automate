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
RUN git clone https://github.com/ropnop/go-windapsearch.git && cd go-windapsearch && /usr/local/go/bin/go get github.com/magefile/mage && mage build && ./windapsearch --version

# Install impacket
RUN sudo apt install python3-pip && pip3 install pipx && python3 -m pipx install impacket