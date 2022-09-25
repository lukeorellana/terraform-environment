FROM ubuntu:20.04
ARG TFVERSION=1.3.0
ARG TG_VERSION=0.38.12

RUN apt-get update && apt-get install -y gnupg software-properties-common curl ca-certificates apt-transport-https lsb-release

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    curl \
    openssh-server \
    jq \
    git \
    wget \
    golang \
    unzip \
    pip \
    iputils-ping \
    netcat \
    vim


# Install Azure CLI
RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

# Install Terraform
RUN wget -q "https://releases.hashicorp.com/terraform/$TFVERSION/terraform_${TFVERSION}_linux_amd64.zip" \
    && unzip terraform_${TFVERSION}_linux_amd64.zip \
    && mv terraform /usr/local/bin/  \ 
    && rm terraform_${TFVERSION}_linux_amd64.zip

#Install PWSH
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb \
    && apt-get install ./packages-microsoft-prod.deb \
    && apt-get update \
    #&& add-apt-repository universe \
    && apt-get install -y powershell \
    && pwsh

# Install Terragrunt
RUN curl -LsS "https://github.com/gruntwork-io/terragrunt/releases/download/v${TG_VERSION}/terragrunt_linux_amd64" -o /usr/local/bin/terragrunt && \
  chmod +x /usr/local/bin/terragrunt

#Install Pre-Commit
RUN pip install pre-commit

#Install tflint
RUN curl -L "$(curl -Ls https://api.github.com/repos/terraform-linters/tflint/releases/latest | grep -o -E "https://.+?_linux_amd64.zip")" -o tflint.zip \
    && unzip tflint.zip && rm tflint.zip \
    && mv tflint /usr/local/bin/