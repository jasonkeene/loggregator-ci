FROM golang:1.9

RUN go version

RUN apt-get update; apt-get install --yes \
    bundler \
    jq \
    rsync \
    unzip \
    psmisc \
    vim

# get v3 protoc from github, it was in beta at the time of writing
RUN cd /tmp \
  && wget https://github.com/google/protobuf/releases/download/v3.0.0-beta-2/protoc-3.0.0-beta-2-linux-x86_64.zip \
  && unzip *.zip \
  && cp ./protoc /usr/local/bin/

RUN go get -d github.com/cloudfoundry/bosh-cli && go build -o $GOPATH/bin/bosh github.com/cloudfoundry/bosh-cli
RUN curl -L "https://cli.run.pivotal.io/stable?release=debian64&source=github" > cf.deb && dpkg -i ./cf.deb

RUN go get github.com/onsi/ginkgo/ginkgo
RUN git config --global user.email "cf-loggregator@pivotal.io" && git config --global user.name "Loggregator CI"

RUN cd /tmp \
  && wget https://github.com/cloudfoundry/bosh-bootloader/releases/download/v6.6.7/bbl-v6.6.7_linux_x86-64 -O /usr/local/bin/bbl \
  && chmod +x /usr/local/bin/bbl

RUN cd /tmp \
    && wget https://releases.hashicorp.com/terraform/0.11.7/terraform_0.11.7_linux_amd64.zip -O terraform.zip \
    && unzip terraform.zip -d /usr/local/bin

RUN cd /tmp \
  && wget https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-sdk-200.0.0-linux-x86_64.tar.gz -O google-cloud-sdk.tar.gz \
  && tar xzvf google-cloud-sdk.tar.gz -C /usr/local/share \
  && /usr/local/share/google-cloud-sdk/install.sh \
  && ln -s /usr/local/share/google-cloud-sdk/bin/gcloud /usr/local/bin/gcloud

RUN wget -O /usr/local/bin/kubectl https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl \
  && chmod +x /usr/local/bin/kubectl

RUN cd /tmp \
  && wget https://github.com/cloudfoundry-incubator/credhub-cli/releases/download/1.7.5/credhub-linux-1.7.5.tgz \
  && tar xzvf credhub*.tgz ./credhub \
  && cp ./credhub /usr/local/bin/
