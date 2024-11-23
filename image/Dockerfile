# Use the codercom/code-server base image
FROM codercom/code-server:4.93.1

# Set environment variables
ENV T_VERSION=1.9.8
ENV GO_VERSION=1.23.3
ENV PATH="/usr/local/go/bin:$PATH"

# Switch to root user to install dependencies
USER root

RUN apt-get update
RUN apt install unzip \ 
    && apt-get install -y docker.io \
    && apt-get clean

# Install Terraform
RUN curl -fsSL "https://releases.hashicorp.com/terraform/${T_VERSION}/terraform_${T_VERSION}_linux_amd64.zip" -o terraform.zip \
    && unzip terraform.zip \
    && mv terraform /usr/local/bin/ \
    && chmod +x /usr/local/bin/terraform \
    && rm -f terraform.zip

# Install AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip awscliv2.zip \
    && ./aws/install \
    && rm -rf awscliv2.zip aws

# Install Go
RUN curl -fsSL "https://dl.google.com/go/go${GO_VERSION}.linux-amd64.tar.gz" -o go.tar.gz \
    && tar -C /usr/local -xzf go.tar.gz \
    && rm -f go.tar.gz

ENV PATH=/usr/local/go/bin:$PATH
# Switch back to the non-root user for running code-server

# Expose the default code-server port
