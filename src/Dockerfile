FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes

# Install base deps
RUN apt-get update \
&& apt-get install -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg-agent \
    software-properties-common \
    wget

# Install .NET CLI dependencies
RUN wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb --no-check-certificate \
&& dpkg -i packages-microsoft-prod.deb \
&& rm -f packages-microsoft-prod.deb

# Install .NET SDK
RUN apt-get update \
&& apt-get install -y --no-install-recommends \
        dotnet-sdk-8.0

# Install Docker CLI
RUN apt-get update \
&& curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add - \
&& add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
   $(lsb_release -cs) \
   stable" \
&& apt-get update \
&& apt-get install -y docker-ce-cli

# Install PowerShell
RUN apt-get update \
&& apt-get install -y --no-install-recommends \
        powershell

# Install Remaining OS Deps
RUN apt-get update \
&& apt-get install -y --no-install-recommends \
        jq \
        git \
        iputils-ping \
        libcurl4 \
        libunwind8 \
        netcat \
        libssl1.0 \
		    zip \
		    unzip \
        libfreetype6-dev \
&& rm -rf /var/lib/apt/lists/*

# Install Azure CLI
RUN curl -LsS https://aka.ms/InstallAzureCLIDeb | bash \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /azp

COPY ./start.sh .
RUN chmod +x start.sh

CMD ["./start.sh"]