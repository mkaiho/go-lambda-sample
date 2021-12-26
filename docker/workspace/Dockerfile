FROM amazonlinux:2

ARG GO_FILE=go1.17.5.linux-amd64.tar.gz
ARG SRC_MODULE=github.com/mkaiho/go-lambda-sample

ENV GOPATH /go
ENV PATH $PATH:/usr/local/go/bin:$GOPATH/bin

RUN yum update -y && yum install -y \
  sudo tar curl gcc make git unzip

RUN useradd "ec2-user" && echo "ec2-user ALL=NOPASSWD: ALL" >> /etc/sudoers

RUN curl -OL https://golang.org/dl/${GO_FILE} \
  && tar -C /usr/local -xzf ${GO_FILE} \
  && rm ${GO_FILE}

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
  && unzip awscliv2.zip \
  && rm awscliv2.zip \
  && ./aws/install \
  && rm -r ./aws \
&& curl -L -o direnv https://github.com/direnv/direnv/releases/download/v2.29.0/direnv.linux-amd64 \
  && chmod +x direnv \
  && mv direnv /usr/local/bin/ \
  && echo 'eval "$(direnv hook bash)"' >> /home/ec2-user/.bashrc

RUN mkdir -p $GOPATH/src/$SRC_MODULE && chmod -R 777 $GOPATH

USER ec2-user
WORKDIR $GOPATH/src/$SRC_MODULE
