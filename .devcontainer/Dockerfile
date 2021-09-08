FROM amazonlinux:latest
## SYSTEM SETUP
RUN yum update -y
RUN yum install -y sudo gcc g++ make git zip unzip tar bzip2 wget jq openssl uuid -y
RUN yum install -y python3
## VSCODE USER Setup
RUN adduser vscode
RUN usermod -aG wheel vscode
RUN echo '%vscode ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers
## AWS CLI
RUN wget --quiet "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -O ~/awscliv2.zip \
    && unzip ~/awscliv2.zip \
    && ./aws/install \
    && aws --version \
    && rm aws/install \
    && rm ~/awscliv2.zip
## Parallel 
RUN wget --quiet "https://ftpmirror.gnu.org/parallel/parallel-20200222.tar.bz2" -O ~/parallel-20200222.tar.bz2 \
    && bzip2 -dc ~/parallel-20200222.tar.bz2 | tar xvf - \
    && cd parallel-20200222 \
    && ./configure && make && make install \
    && rm -rf parallel-20200222 \
    && rm ~/parallel-20200222.tar.bz2
#Python Tools
COPY requirements.txt /tmp/pip-tmp/
RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt && rm -rf /tmp/pip-tmp
#### VSCODE USER
USER vscode
RUN python3 -m venv /home/vscode/venv
RUN echo 'source ~/venv/bin/activate && python -m pip install --upgrade pip' >> ~/.bash_profile
