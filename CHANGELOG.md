aerospike-prometheus-exporter/._Dockerfile                                                          000644  000765  000024  00000000243 14426133132 022246  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/Dockerfile                                                  000644  000765  000024  00000000210 14426133132 023774  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.077340007
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/Dockerfile                                                            000644  000765  000024  00000001443 14426133132 022034  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         FROM golang:1.20-alpine AS builder

ARG VERSION=1.10.0

ADD . $GOPATH/src/github.com/aerospike/aerospike-prometheus-exporter
WORKDIR $GOPATH/src/github.com/aerospike/aerospike-prometheus-exporter
RUN go build -ldflags="-X 'main.version=$VERSION'" -o aerospike-prometheus-exporter . \
	&& cp aerospike-prometheus-exporter /aerospike-prometheus-exporter

FROM alpine:latest

COPY --from=builder /aerospike-prometheus-exporter /usr/bin/aerospike-prometheus-exporter
COPY ape.toml.template /etc/aerospike-prometheus-exporter/ape.toml.template
COPY docker-entrypoint.sh /docker-entrypoint.sh

RUN apk add gettext libintl \
	&& chmod +x /docker-entrypoint.sh

EXPOSE 9145

ENTRYPOINT [ "/docker-entrypoint.sh" ]
CMD ["aerospike-prometheus-exporter", "--config", "/etc/aerospike-prometheus-exporter/ape.toml"]
                                                                                                                                                                                                                             aerospike-prometheus-exporter/._LICENSE                                                             000644  000765  000024  00000000243 14426133132 021261  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/LICENSE                                                     000644  000765  000024  00000000210 14426133132 023007  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.077531673
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/LICENSE                                                               000644  000765  000024  00000025010 14426133132 021043  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                                                          Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS

   Copyright 2020 Aerospike, Inc.

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/._Makefile                                                            000644  000765  000024  00000000243 14426143306 021720  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/Makefile                                                    000644  000765  000024  00000000210 14426143306 023446  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.088061499
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/Makefile                                                              000644  000765  000024  00000004535 14426143306 021513  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         # Variables required for this Makefile
# Include all common variables
include Makefile.vars

# Builds exporter binary
.PHONY: exporter
exporter:
	@echo $(GO_FIPS)
	$(GO_ENV_VARS) GOEXPERIMENT=$(GO_FIPS) go build -ldflags="-X 'main.version=$(VERSION)'" -o aerospike-prometheus-exporter .

.PHONY: fipsparam
fipsparam: 
ifeq ($(APE_SUPPORTED_OS),validfipsos)
	@echo  "Setting FIPS required params"
	$(eval GO_FIPS=$(GO_BORINGCRYPTO))
	$(eval PKG_FILENAME=$(FIPS_PKG_FILENAME))
else
	@echo  "Fips Exporter build is supported only on CentOS 8 or Red Hat 8 versions or have Golang v1.20 and above"
	exit 1
endif

.PHONY: fmt
fmt: ## Run go fmt against code.
	go fmt ./...

.PHONY: lint
lint:
    ## install golangci-lint from https://raw.githubusercontent.com/golangci/golangci-lint , install and include in PATH
    ## Run golangci-lint against code.
	golangci-lint run

.PHONY: test
test: ## Run all the test-cases defined in this folder.
	go test -v ./...	

# Builds RPM, DEB and TAR packages
# Requires FPM package manager
.PHONY: deb
deb: exporter
	$(MAKE) -C $(ROOT_DIR)/pkg/ deb 

.PHONY: fips-deb
fips-deb: fipsparam exporter
	$(MAKE) -C $(ROOT_DIR)/pkg/ fips-deb 

.PHONY: rpm
rpm: exporter
	$(MAKE) -C $(ROOT_DIR)/pkg/ rpm 

.PHONY: fips-rpm
fips-rpm: fipsparam exporter
	$(MAKE) -C $(ROOT_DIR)/pkg/ fips-rpm

.PHONY: tar
tar: exporter
	$(MAKE) -C $(ROOT_DIR)/pkg/ tar 

.PHONY: fips-tar
fips-tar: fipsparam exporter
	$(MAKE) -C $(ROOT_DIR)/pkg/ fips-tar 

# Clean up
.PHONY: clean
clean:
	rm -rf aerospike-prometheus-exporter
	$(MAKE) -C $(ROOT_DIR)/pkg/ $@

# Builds exporter docker image
# Requires docker
.PHONY: docker
docker:
	docker build --build-arg VERSION=$(VERSION) . -t aerospike/aerospike-prometheus-exporter:latest

# NOTE: this builds and pushes the image to aerospike/aerospike-prometheus-exporter docker hub repository
# Use this target only for release
.PHONY: release-docker-multi-arch
release-docker-multi-arch:
	docker buildx build --build-arg VERSION=$(VERSION) --platform $(DOCKER_MULTI_ARCH_PLATFORMS) --push . -t aerospike/aerospike-prometheus-exporter:latest -t aerospike/aerospike-prometheus-exporter:$(VERSION)

.PHONY: package-linux-arm64
package-linux-arm64:
	$(MAKE) deb rpm tar GOOS=linux GOARCH=arm64 DEB_PKG_ARCH=arm64 ARCH=aarch64

.PHONY: package-linux-amd64
package-linux-amd64:
	$(MAKE) deb rpm tar GOOS=linux GOARCH=amd64 DEB_PKG_ARCH=amd64 ARCH=x86_64
                                                                                                                                                                   aerospike-prometheus-exporter/._Makefile.vars                                                       000644  000765  000024  00000000243 14426133132 022666  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/Makefile.vars                                               000644  000765  000024  00000000210 14426133132 024414  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.077824839
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/Makefile.vars                                                         000644  000765  000024  00000002547 14426133132 022462  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         # Variables required for this Makefile
ROOT_DIR = $(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))
VERSION = $(shell git describe --tags | cut -c 2-)
GO_ENV_VARS =

PKG_FILENAME = aerospike-prometheus-exporter
FIPS_PKG_FILENAME = aerospike-prometheus-exporter-federal
CENTOS_8 = $(shell cat /etc/*-release | grep "PRETTY_NAME" | sed 's/PRETTY_NAME=//g' | grep -i "CentOS" | grep -i "Linux 8")
RHEL_8 = $(shell cat /etc/*-release | grep "PRETTY_NAME" | sed 's/PRETTY_NAME=//g' | grep -i "Red Hat" | grep -i "Linux 8")

# FIPS required evaluations
GO_VERSION = $(shell go version)
GO_FIPS =

APE_SUPPORTED_OS = invalid-os

ifeq ( , $(findstring go1.20,$(GO_VERSION) go_not_20 ))
        GO_BORINGCRYPTO=
        # check if OS is CentOS 8 or RHEL 8
        ifeq ($(CENTOS_8),)
	         ifneq ($(RHEL_8),)
			      APE_SUPPORTED_OS = validfipsos
		      else
			      APE_SUPPORTED_OS = not-validfipsos
		      endif
	      else
		         APE_SUPPORTED_OS = validfipsos
         endif
        # end OS check

else
        # If Go version is >=1.20 we auto-support FIPS build
        APE_SUPPORTED_OS = validfipsos
        GO_BORINGCRYPTO=boringcrypto
endif

# end FIPS required evaluations

# Variables related to go build

ifdef GOOS
GO_ENV_VARS = GOOS=$(GOOS)
endif

ifdef GOARCH
GO_ENV_VARS += GOARCH=$(GOARCH)
endif

DOCKER_MULTI_ARCH_PLATFORMS = linux/amd64,linux/arm64
                                                                                                                                                         aerospike-prometheus-exporter/._README.md                                                           000644  000765  000024  00000000243 14426133132 021533  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/README.md                                                   000644  000765  000024  00000000210 14426133132 023261  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.077998922
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/README.md                                                             000644  000765  000024  00000032703 14426133132 021324  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         # Aerospike Prometheus Exporter

This repo contains Aerospike's monitoring agent for Prometheus. The exporter is part of the [Aerospike Monitoring Stack](https://www.aerospike.com/docs/tools/monitorstack/index.html).

The Aerospike Prometheus Exporter is now **generally available** (GA).
If you're an enterprise customer feel free to reach out to support with any questions.
We appreciate feedback from community members on the [issues](https://github.com/aerospike/aerospike-prometheus-exporter/issues).

## Build Instructions

### Aerospike Prometheus Exporter Binary

#### Pre Requisites

- Install Go v1.17+

#### Steps

1. Clone or fetch this repository
    ```bash
    git clone https://github.com/aerospike/aerospike-prometheus-exporter.git
    cd aerospike-prometheus-exporter/

    # or

    # go get github.com/aerospike/aerospike-prometheus-exporter
    # cd $GOPATH/src/github.com/aerospike/aerospike-prometheus-exporter
    ```
2. Build the exporter binary,
    ```bash
    go build -o aerospike-prometheus-exporter .
    ```
    or,

    ```bash
    make
    ```

3. Run the exporter
     ```bash
     ./aerospike-prometheus-exporter --config <full-path-of-the-config-file>
     ```

### Aerospike Prometheus Exporter Docker Image

- Build the docker image
  ```bash
  docker build . -t aerospike/aerospike-prometheus-exporter:latest
  ```
  or,

  ```bash
  make docker
  ```
- Run the exporter as a container
  ```bash
  docker run -itd --name exporter1 -e AS_HOST=172.17.0.2 -e AS_PORT=3000 -e METRIC_LABELS="type='development',source='aerospike'" aerospike/aerospike-prometheus-exporter:latest
  ```

### `RPM`, `DEB` and `tar` Package

####  Pre Requisites

- FPM Package manager
    - https://fpm.readthedocs.io/en/latest/installing.html
    - For instance, on Debian-derived systems (Debian, Ubuntu, etc),
        ```bash
        apt install ruby ruby-dev rubygems build-essential -y
        ```
        ```bash
        gem install --no-document fpm
        ```

####  Pre Requisites for a FIPS build

To generate a FIPS compatible exporter you need Golang 1.20 or above or have a FIPS enabled OS and OpenSSL.

Aerospike Exporter internally using boringcrypto library for FIPS complaince crypto operations

#### Steps

Build the exporter go binary and package it into `rpm`, `deb` or `tar`.

- Build `deb` package,
    ```bash
    make deb
    ```

- Build `rpm` package,
    ```bash
    make rpm
    ```

- Build linux tarball,
    ```bash
    make tar
    ```

- Build FIPS compliant `deb` package,
    ```bash
    make fips-deb
    ```

- Build FIPS compliant `rpm` package,
    ```bash
    make fips-rpm
    ```

- Build FIPS compliant linux tarball,
    ```bash
    make fips-tar
    ```

Packages will be generated under `./pkg/target/` directory.

#### Support for multiple architectures

Build the exporter packages for `linux/arm64` and `linux/amd64`.

For `arm64`,
```bash
make package-linux-arm64
```

For `amd64`,
```bash
make package-linux-amd64
```

For docker, build and push (for release only) exporter docker image with multiarch support
```bash
make release-docker-multi-arch
```

#### Install Exporter Using `DEB` and `RPM` Packages

- Install `deb` package
    ```bash
    dpkg -i ./pkg/target/aerospike-prometheus-exporter-*.deb
    ```

- Install `rpm` package
    ```bash
    rpm -Uvh ./pkg/target/aerospike-prometheus-exporter-*.rpm
    ```

- Install FIPS compatible `rpm` package
    ```bash
    rpm -Uvh ./pkg/target/aerospike-prometheus-exporter-federal-*.rpm
    ```

- Run the exporter
    ```bash
    systemctl start aerospike-prometheus-exporter.service
    ```

## Aerospike Prometheus Exporter Configuration

- Aerospike Prometheus Exporter requires a configuration file to run. Check [default configuration file](ape.toml).
    ```bash
    mkdir -p /etc/aerospike-prometheus-exporter
    curl https://raw.githubusercontent.com/aerospike/aerospike-prometheus-exporter/master/ape.toml -o /etc/aerospike-prometheus-exporter/ape.toml
    ```

- Edit `/etc/aerospike-prometheus-exporter/ape.toml` to add `db_host` (default `localhost`) and `db_port` (default `3000`) to point to an Aerospike server IP and port.
    ```toml
    [Aerospike]

    db_host="localhost"
    db_port=3000
    ```

- Configure timeout (in seconds) for info commands to Aerospike node (optional). Default value is `5` seconds.
    ```toml
    [Aerospike]
    # timeout for sending commands to the server node in seconds
    timeout=5
    ```

- Update Aerospike security and TLS configurations (optional),
    ```toml
    [Aerospike]

    # TLS certificates.
    # Supports below formats,
    # 2. Certificate file path                                      - "file:<file-path>"
    # 3. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
    # 4. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
    # Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

    # root certificate file
    root_ca=""

    # certificate file
    cert_file=""

    # key file
    key_file=""

    # Passphrase for encrypted key_file. Supports below formats,
    # 1. Passphrase directly                                                      - "<passphrase>"
    # 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
    # 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
    # 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
    # 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
    key_file_passphrase=""

    # node TLS name for authentication
    node_tls_name=""

    # Aerospike cluster security credentials.
    # Supports below formats,
    # 1. Credential directly                                                      - "<credential>"
    # 2. Credential via file                                                      - "file:<file-that-contains-credential>"
    # 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
    # 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
    # 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
    # Applicable to 'user' and 'password' configurations.

    # database user
    user=""

    # database password
    password=""

    # authentication mode: internal (for server), external (LDAP, etc.)
    auth_mode=""
    ```

- Update exporter's bind address and port (default: `0.0.0.0:9145`), and add labels.
    ```toml
    [Agent]

    bind=":9145"
    labels={zone="asia-south1-a", platform="google compute engine"}
    ```

- Use allowlist and blocklist to filter out required metrics (optional). The allowlist and blocklist supports standard wildcards (globbing patterns which include - `? (question mark)`, `* (asterisk)`, `[ ] (square brackets)`, `{ } (curly brackets)`, `[!]` and `\ (backslash)`) for bulk metrics filtering. For example,
    ```toml
    [Aerospike]

    # Metrics Allowlist - If specified, only these metrics will be scraped. An empty list will exclude all metrics.
    # Commenting out the below allowlist configs will disable metrics filtering (i.e. all metrics will be scraped).

    # Namespace metrics allowlist
    namespace_metrics_allowlist=[
    "client_read_[a-z]*",
    "stop_writes",
    "storage-engine.file.defrag_q",
    "client_write_success",
    "memory_*_bytes",
    "objects",
    "*_available_pct"
    ]

    # Set metrics allowlist
    set_metrics_allowlist=[
    "objects",
    "tombstones"
    ]

    # Node metrics allowlist
    node_metrics_allowlist=[
    "uptime",
    "cluster_size",
    "batch_index_*",
    "xdr_ship_*"
    ]

    # XDR metrics allowlist (only for Aerospike versions 5.0 and above)
    xdr_metrics_allowlist=[
    "success",
    "latency_ms",
    "throughput",
    "lap_us"
    ]

    # Job (scans/queries) metrics allowlist
    job_metrics_allowlist = [
    "rps",
    "active-threads",
    "job-progress",
    "run-time",
    "recs-throttled",
    "recs-succeeded",
    "recs-failed",
    "net-io-bytes"
    ]

    # Secondary index metrics allowlist
    sindex_metrics_allowlist = [
    "entries",
    "ibtr_memory_used",
    "nbtr_memory_used",
    "query_basic_complete",
    "query_basic_error",
    "query_basic_abort",
    "query_basic_avg_rec_count"
    ]

    # Metrics Blocklist - If specified, these metrics will be NOT be scraped.

    # Namespace metrics blocklist
    namespace_metrics_blocklist=[
    "memory_used_sindex_bytes",
    "client_read_success"
    ]

    # Set metrics blocklist
    # set_metrics_blocklist=[]

    # Node metrics blocklist
    node_metrics_blocklist=[
    "batch_index_*_buffers"
    ]

    # XDR metrics blocklist (only for Aerospike versions 5.0 and above)
    # xdr_metrics_blocklist=[]

    # Job (scans/queries) metrics blocklist
    # job_metrics_blocklist = []

    # Secondary index metrics blocklist
    # sindex_metrics_blocklist = []
    ```

- To enable basic HTTP authentication and/or enable HTTPS between the Prometheus server and the exporter, use the below configurations keys,
    ```toml
    [Agent]
    # Exporter HTTPS (TLS) configuration
    # HTTPS between Prometheus and Exporter

    # TLS certificates.
    # Supports below formats,
    # 1. Certificate file path                                      - "file:<file-path>"
    # 2. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
    # 3. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
    # Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

    # Server certificate
    cert_file = ""

    # Private key associated with server certificate
    key_file = ""

    # Root CA to validate client certificates (for mutual TLS)
    root_ca = ""

    # Passphrase for encrypted key_file. Supports below formats,
    # 1. Passphrase directly                                                      - "<passphrase>"
    # 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
    # 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
    # 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
    # 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
    key_file_passphrase = ""

    # Basic HTTP authentication for '/metrics'.
    # Supports below formats,
    # 1. Credential directly                                                      - "<credential>"
    # 2. Credential via file                                                      - "file:<file-that-contains-credential>"
    # 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
    # 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
    # 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
    basic_auth_username=""
    basic_auth_password=""
    ```

- Use users' allowlist and blocklist configuration to filter out the users for which the statistics are to be fetched. The user statistics are available in Aerospike 5.6+. To fetch user statistics, the authenticated user must have `user-admin` privilege.
    ```toml
    [Aerospike]

    # Users Statistics (user statistics are available in Aerospike 5.6+)
    # Users Allowlist and Blocklist to control for which users their statistics should be collected.
    # Note globbing patterns are not supported for this configuration.

    user_metrics_users_allowlist=[
    "admin",
    "superuser",
    "aerospikeUser1",
    "aerospikeUser2"
    ]

    user_metrics_users_blocklist=[
    "admin",
    "superuser"
    ]
    ```

- Exporter logs to console by default. To enable file logging, use `log_file` configuration to specify a file path. Use `log_level` configuration to specify a logging level (optional). Default logging level is `info`.
    ```toml
    [Agent]
    # Exporter logging configuration
    # Log file path (optional, logs to console by default)
    # Level can be info|warning,warn|error,err|debug|trace ('info' by default)
    log_file = ""
    log_level = ""
    ```

- Use `latency_buckets_count` to specify number of histogram buckets to be exported for latency metrics (optional). Bucket thresholds range from 2<sup>0</sup> to 2<sup>16</sup> (`17` buckets). All threshold buckets are exported by default (`latency_buckets_count=0`).

    Example, `latency_buckets_count=5` will export first five buckets i.e. `<=1ms`, `<=2ms`, `<=4ms`, `<=8ms` and `<=16ms`.
    ```toml
    [Aerospike]
    # Number of histogram buckets to export for latency metrics. Bucket thresholds range from 2^0 to 2^16 (17 buckets).
    # e.g. latency_buckets_count=5 will export first five buckets i.e. <=1ms, <=2ms, <=4ms, <=8ms and <=16ms.
    # Default: 0 (export all threshold buckets).
    latency_buckets_count=0
    ```
                                                             aerospike-prometheus-exporter/._ape.toml                                                            000644  000765  000024  00000000243 14426143306 021722  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/ape.toml                                                    000644  000765  000024  00000000210 14426143306 023450  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.088318021
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/ape.toml                                                              000644  000765  000024  00000015145 14426143306 021514  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         [Agent]
# Exporter HTTPS (TLS) configuration
# HTTPS between Prometheus and Exporter

# TLS certificates.
# Supports below formats,
# 1. Certificate file path                                      - "file:<file-path>"
# 2. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
# 3. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
# Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

# Server certificate
cert_file = ""

# Private key associated with server certificate
key_file = ""

# Root CA to validate client certificates (for mutual TLS)
root_ca = ""

# Passphrase for encrypted key_file. Supports below formats,
# 1. Passphrase directly                                                      - "<passphrase>"
# 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
# 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
# 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
# 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
key_file_passphrase = ""

# labels to add to the prometheus metrics for e.g. labels={zone="asia-south1-a", platform="google compute engine"}
labels = {}

bind = ":9145"

# metrics server timeout in seconds
timeout = 10

# Exporter logging configuration
# Log file path (optional, logs to console by default)
# Level can be info|warning,warn|error,err|debug|trace ('info' by default)
log_file = ""
log_level = ""

# Basic HTTP authentication for '/metrics'.
# Supports below formats,
# 1. Credential directly                                                      - "<credential>"
# 2. Credential via file                                                      - "file:<file-that-contains-credential>"
# 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
# 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
# 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
basic_auth_username = ""
basic_auth_password = ""

[Aerospike]
db_host = "localhost"
db_port = 3000

# TLS certificates.
# Supports below formats,
# 1. Certificate file path                                      - "file:<file-path>"
# 2. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
# 3. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
# Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

# root certificate file
root_ca = ""

# certificate file
cert_file = ""

# key file
key_file = ""

# Passphrase for encrypted key_file. Supports below formats,
# 1. Passphrase directly                                                      - "<passphrase>"
# 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
# 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
# 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
# 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
key_file_passphrase = ""

# node TLS name for authentication
node_tls_name = ""

# Aerospike cluster security credentials.
# Supports below formats,
# 1. Credential directly                                                      - "<credential>"
# 2. Credential via file                                                      - "file:<file-that-contains-credential>"
# 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
# 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
# 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
# Applicable to 'user' and 'password' configurations.

# database user
user = ""

# database password
password = ""

# authentication mode: internal (for server), external (LDAP, etc.)
auth_mode = ""

# timeout for sending commands to the server node in seconds
timeout = 5

# Number of histogram buckets to export for latency metrics. Bucket thresholds range from 2^0 to 2^16 (17 buckets).
# e.g. latency_buckets_count=5 will export first five buckets i.e. <=1ms, <=2ms, <=4ms, <=8ms and <=16ms.
# Default: 0 (export all threshold buckets).
latency_buckets_count = 0

# Order of context - namespace, set, latencies, node-stats, xdr, user, jobs, sindex

# Metrics Allowlist - If specified, only these metrics will be scraped. An empty list will exclude all metrics.
# Commenting out the below allowlist configs will disable metrics filtering (i.e. all metrics will be scraped).

# Metrics Blocklist - If specified, these metrics will be NOT be scraped. An empty list will include all metrics.
# Commenting out the below blocklist configs will disable metrics filtering (i.e. no metrics will be blocked/filtered).

# globbing pattern (wildcard) are allowd for allowlist and blocklist
# for example "batch_index_*_buffers"

# Namespace metrics allowlist, to control which Namespace metrics should be collected.
# namespace_metrics_allowlist = []
# namespace_metrics_blocklist = []

# set_metrics_allowlist = []
# set_metrics_blocklist = []

# Latencies histogram allowlist, to control which Histogram-name metrics should be collected. 
# Note: globbing patterns (wildcard) are not supported for this latency metric configuration. 
# latencies_metrics_allowlist = []
# latencies_metrics_blocklist = []

# node_metrics_allowlist = []
# node_metrics_blocklist = []

# Support only from Aerospike versions 5.0 and above
# xdr_metrics_allowlist = []
# xdr_metrics_blocklist = []

# User statistics are available in Aerospike 5.6+
# Note globbing patterns (wildcard) are not supported for this User configuration.
# user_metrics_users_allowlist = []
# user_metrics_users_blocklist = []

# job_metrics_allowlist = []
# job_metrics_blocklist = []

# sindex_metrics_allowlist = []
# sindex_metrics_blocklist = []

                                                                                                                                                                                                                                                                                                                                                                                                                           aerospike-prometheus-exporter/._ape.toml.template                                                   000644  000765  000024  00000000243 14426133132 023530  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/ape.toml.template                                           000644  000765  000024  00000000210 14426133132 025256  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.078306295
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/ape.toml.template                                                     000644  000765  000024  00000016240 14426133132 023317  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         [Agent]
# Exporter HTTPS (TLS) configuration
# HTTPS between Prometheus and Exporter

# TLS certificates.
# Supports below formats,
# 1. Certificate file path                                      - "file:<file-path>"
# 2. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
# 3. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
# Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

# Server certificate
cert_file = "${AGENT_CERT_FILE}"

# Private key associated with server certificate
key_file = "${AGENT_KEY_FILE}"

# Root CA to validate client certificates (for mutual TLS)
root_ca = "${AGENT_ROOT_CA}"

# Passphrase for encrypted key_file. Supports below formats,
# 1. Passphrase directly                                                      - "<passphrase>"
# 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
# 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
# 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
# 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
key_file_passphrase = "${AGENT_KEY_FILE_PASSPHRASE}"

# labels to add to the prometheus metrics for e.g. labels={zone="asia-south1-a", platform="google compute engine"}
labels = {${METRIC_LABELS}}

bind = "${AGENT_BIND_HOST}:${AGENT_BIND_PORT}"

# metrics server timeout in seconds
timeout = ${AGENT_TIMEOUT}

# Exporter logging configuration
# Log file path (optional, logs to console by default)
# Level can be info|warning,warn|error,err|debug|trace ('info' by default)
log_file = "${AGENT_LOG_FILE}"
log_level = "${AGENT_LOG_LEVEL}"

# Basic HTTP authentication for '/metrics'.
# Supports below formats,
# 1. Credential directly                                                      - "<credential>"
# 2. Credential via file                                                      - "file:<file-that-contains-credential>"
# 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
# 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
# 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
basic_auth_username = "${BASIC_AUTH_USERNAME}"
basic_auth_password = "${BASIC_AUTH_PASSWORD}"

[Aerospike]
db_host = "${AS_HOST}"
db_port = ${AS_PORT}

# TLS certificates.
# Supports below formats,
# 1. Certificate file path                                      - "file:<file-path>"
# 2. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
# 3. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
# Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

# root certificate file
root_ca = "${AS_ROOT_CA}"

# certificate file
cert_file = "${AS_CERT_FILE}"

# key file
key_file = "${AS_KEY_FILE}"

# Passphrase for encrypted key_file. Supports below formats,
# 1. Passphrase directly                                                      - "<passphrase>"
# 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
# 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
# 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
# 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
key_file_passphrase = "${AS_KEY_FILE_PASSPHRASE}"

# node TLS name for authentication
node_tls_name = "${AS_NODE_TLS_NAME}"

# Aerospike cluster security credentials.
# Supports below formats,
# 1. Credential directly                                                      - "<credential>"
# 2. Credential via file                                                      - "file:<file-that-contains-credential>"
# 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
# 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
# 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
# Applicable to 'user' and 'password' configurations.

# database user
user = "${AS_AUTH_USER}"

# database password
password = "${AS_AUTH_PASSWORD}"

# authentication mode: internal (for server), external (LDAP, etc.)
auth_mode = "${AS_AUTH_MODE}"

# timeout for sending commands to the server node in seconds
timeout = ${TICKER_TIMEOUT}

# Number of histogram buckets to export for latency metrics. Bucket thresholds range from 2^0 to 2^16 (17 buckets).
# e.g. latency_buckets_count = 5 will export first five buckets i.e. <=1ms, <=2ms, <=4ms, <=8ms and <=16ms.
# Default: 0 (export all threshold buckets).
latency_buckets_count = ${LATENCY_BUCKETS_COUNT}

# Metrics Allowlist - If specified, only these metrics will be scraped. An empty list will exclude all metrics.
# Commenting out the below allowlist configs will disable metrics filtering (i.e. all metrics will be scraped).

# Namespace metrics allowlist
# namespace_metrics_allowlist = [${NAMESPACE_METRICS_ALLOWLIST}]

# Set metrics allowlist
# set_metrics_allowlist = [${SET_METRICS_ALLOWLIST}]

# Node metrics allowlist
# node_metrics_allowlist = [${NODE_METRICS_ALLOWLIST}]

# XDR metrics allowlist (only for Aerospike versions 5.0 and above)
# xdr_metrics_allowlist = [${XDR_METRICS_ALLOWLIST}]

# Job (scans/queries) metrics allowlist
# job_metrics_allowlist = [${JOB_METRICS_ALLOWLIST}]

# Secondary index metrics allowlist
# sindex_metrics_allowlist = [${SINDEX_METRICS_ALLOWLIST}]

# Metrics Blocklist - If specified, these metrics will be NOT be scraped.

# Namespace metrics blocklist
# namespace_metrics_blocklist = [${NAMESPACE_METRICS_BLOCKLIST}]

# Set metrics blocklist
# set_metrics_blocklist = [${SET_METRICS_BLOCKLIST}]

# Node metrics blocklist
# node_metrics_blocklist = [${NODE_METRICS_BLOCKLIST}]

# XDR metrics blocklist (only for Aerospike versions 5.0 and above)
# xdr_metrics_blocklist = [${XDR_METRICS_BLOCKLIST}]

# Job (scans/queries) metrics blocklist
# job_metrics_blocklist = [${JOB_METRICS_BLOCKLIST}]

# Secondary index metrics blocklist
# sindex_metrics_blocklist = [${SINDEX_METRICS_BLOCKLIST}]

# Users Statistics (user statistics are available in Aerospike 5.6+)
# Users Allowlist and Blocklist to control for which users their statistics should be collected.
# Note globbing patterns are not supported for this configuration.

# user_metrics_users_allowlist = [${USER_METRICS_USERS_ALLOWLIST}]
# user_metrics_users_blocklist = [${USER_METRICS_USERS_BLOCKLIST}]
                                                                                                                                                                                                                                                                                                                                                                aerospike-prometheus-exporter/._common.go                                                           000644  000765  000024  00000000243 14426446034 022103  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/common.go                                                   000644  000765  000024  00000000210 14426446034 023631  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683639324.931060699
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/common.go                                                             000644  000765  000024  00000022714 14426446034 021675  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"bytes"
	"crypto/subtle"
	"crypto/tls"
	"crypto/x509"
	"encoding/base64"
	"encoding/pem"
	"fmt"
	"net/http"
	"os"
	"regexp"
	"strconv"
	"strings"
	"unicode/utf8"

	"github.com/gobwas/glob"
	"github.com/prometheus/client_golang/prometheus"

	goversion "github.com/hashicorp/go-version"
)

func makeMetric(namespace, name string, t metricType, constLabels map[string]string, labels ...string) promMetric {
	promDesc := prometheus.NewDesc(
		namespace+"_"+normalizeMetric(name),
		normalizeDesc(name),
		labels,
		constLabels,
	)

	switch t {
	case mtCounter:
		return promMetric{
			origDesc:  name,
			desc:      promDesc,
			valueType: prometheus.CounterValue,
		}
	case mtGauge:
		return promMetric{
			origDesc:  name,
			desc:      promDesc,
			valueType: prometheus.GaugeValue,
		}
	}

	panic("Should not reach here...")
}

var descReplacerFunc = strings.NewReplacer("_", " ", "-", " ", ".", " ")

func normalizeDesc(s string) string {
	return descReplacerFunc.Replace(s)
}

var metricReplacerFunc = strings.NewReplacer(".", "_", "-", "_", " ", "_")

func normalizeMetric(s string) string {
	return metricReplacerFunc.Replace(s)
}

func parseStats(s, sep string) map[string]string {
	stats := make(map[string]string, strings.Count(s, sep)+1)
	s2 := strings.Split(s, sep)
	for _, s := range s2 {
		list := strings.SplitN(s, "=", 2)
		switch len(list) {
		case 0, 1:
		case 2:
			stats[list[0]] = list[1]
		default:
			stats[list[0]] = strings.Join(list[1:], "=")
		}
	}

	return stats
}

func tryConvert(s string) (float64, error) {
	if f, err := strconv.ParseFloat(s, 64); err == nil {
		return f, nil
	}

	if b, err := strconv.ParseBool(s); err == nil {
		if b {
			return 1, nil
		}
		return 0, nil
	}

	return 0, fmt.Errorf("invalid value `%s`. Only Float or Boolean are accepted", s)
}

// Check HTTP Basic Authentication.
// Validate username, password from the http request against the configured values.
func validateBasicAuth(r *http.Request, username string, password string) bool {
	user, pass, ok := r.BasicAuth()

	if !ok || subtle.ConstantTimeCompare([]byte(user), []byte(username)) != 1 || subtle.ConstantTimeCompare([]byte(pass), []byte(password)) != 1 {
		return false
	}

	return true
}

// Regex for indentifying globbing patterns (or standard wildcards) in the metrics allowlist and blocklist.
var globbingPattern = regexp.MustCompile(`\[|\]|\*|\?|\{|\}|\\|!`)

// Filter metrics
// Runs the raw metrics through allowlist first and the resulting metrics through blocklist
func getFilteredMetrics(rawMetrics map[string]metricType, allowlist []string, allowlistEnabled bool, blocklist []string) map[string]metricType {
	filteredMetrics := filterAllowedMetrics(rawMetrics, allowlist, allowlistEnabled)
	filterBlockedMetrics(filteredMetrics, blocklist)

	return filteredMetrics
}

// Filter metrics based on configured allowlist.
func filterAllowedMetrics(rawMetrics map[string]metricType, allowlist []string, allowlistEnabled bool) map[string]metricType {
	if !allowlistEnabled {
		return rawMetrics
	}

	filteredMetrics := make(map[string]metricType)

	for _, stat := range allowlist {
		if globbingPattern.MatchString(stat) {
			ge := glob.MustCompile(stat)

			for k, v := range rawMetrics {
				if ge.Match(k) {
					filteredMetrics[k] = v
				}
			}
		} else {
			if val, ok := rawMetrics[stat]; ok {
				filteredMetrics[stat] = val
			}
		}
	}

	return filteredMetrics
}

// Filter metrics based on configured blocklist.
func filterBlockedMetrics(filteredMetrics map[string]metricType, blocklist []string) {
	if len(blocklist) == 0 {
		return
	}

	for _, stat := range blocklist {
		if globbingPattern.MatchString(stat) {
			ge := glob.MustCompile(stat)

			for k := range filteredMetrics {
				if ge.Match(k) {
					delete(filteredMetrics, k)
				}
			}
		} else {
			delete(filteredMetrics, stat)
		}
	}
}

// Get secret
// secretConfig can be one of the following,
// 1. "<secret>" (secret directly)
// 2. "file:<file-that-contains-secret>" (file containing secret)
// 3. "env:<environment-variable-that-contains-secret>" (environment variable containing secret)
// 4. "env-b64:<environment-variable-that-contains-base64-encoded-secret>" (environment variable containing base64 encoded secret)
// 5. "b64:<base64-encoded-secret>" (base64 encoded secret)
func getSecret(secretConfig string) ([]byte, error) {
	secretSource := strings.SplitN(secretConfig, ":", 2)

	if len(secretSource) == 2 {
		switch secretSource[0] {
		case "file":
			return readFromFile(secretSource[1])

		case "env":
			secret, ok := os.LookupEnv(secretSource[1])
			if !ok {
				return nil, fmt.Errorf("environment variable %s not set", secretSource[1])
			}

			return []byte(secret), nil

		case "env-b64":
			return getValueFromBase64EnvVar(secretSource[1])

		case "b64":
			return getValueFromBase64(secretSource[1])

		default:
			return nil, fmt.Errorf("invalid source: %s", secretSource[0])
		}
	}

	return []byte(secretConfig), nil
}

// Get certificate
// certConfig can be one of the following,
// 1. "<file-path>" (certificate file path directly)
// 2. "file:<file-path>" (certificate file path)
// 3. "env-b64:<environment-variable-that-contains-base64-encoded-certificate>" (environment variable containing base64 encoded certificate)
// 4. "b64:<base64-encoded-certificate>" (base64 encoded certificate)
func getCertificate(certConfig string) ([]byte, error) {
	certificateSource := strings.SplitN(certConfig, ":", 2)

	if len(certificateSource) == 2 {
		switch certificateSource[0] {
		case "file":
			return readFromFile(certificateSource[1])

		case "env-b64":
			return getValueFromBase64EnvVar(certificateSource[1])

		case "b64":
			return getValueFromBase64(certificateSource[1])

		default:
			return nil, fmt.Errorf("invalid source %s", certificateSource[0])
		}
	}

	// Assume certConfig is a file path (backward compatible)
	return readFromFile(certConfig)
}

// Read content from file
func readFromFile(filePath string) ([]byte, error) {
	dataBytes, err := os.ReadFile(filePath)
	if err != nil {
		return nil, fmt.Errorf("failed to read from file `%s`: `%v`", filePath, err)
	}

	data := bytes.TrimSuffix(dataBytes, []byte("\n"))

	return data, nil
}

// Get decoded base64 value from environment variable
func getValueFromBase64EnvVar(envVar string) ([]byte, error) {
	b64Value, ok := os.LookupEnv(envVar)
	if !ok {
		return nil, fmt.Errorf("environment variable %s not set", envVar)
	}

	return getValueFromBase64(b64Value)
}

// Get decoded base64 value
func getValueFromBase64(b64Value string) ([]byte, error) {
	value, err := base64.StdEncoding.DecodeString(b64Value)
	if err != nil {
		return nil, fmt.Errorf("failed to decode base64 value: %v", err)
	}

	return value, nil
}

// loadCACert returns CA set of certificates (cert pool)
// reads CA certificate based on the certConfig and adds it to the pool
func loadCACert(certConfig string) (*x509.CertPool, error) {
	certificates, err := x509.SystemCertPool()
	if certificates == nil || err != nil {
		certificates = x509.NewCertPool()
	}

	if len(certConfig) > 0 {
		caCert, err := getCertificate(certConfig)
		if err != nil {
			return nil, err
		}

		certificates.AppendCertsFromPEM(caCert)
	}

	return certificates, nil
}

// loadServerCertAndKey reads server certificate and associated key file based on certConfig and keyConfig
// returns parsed server certificate
// if the private key is encrypted, it will be decrypted using key file passphrase
func loadServerCertAndKey(certConfig, keyConfig, keyPassConfig string) ([]tls.Certificate, error) {
	var certificates []tls.Certificate

	// Read cert file
	certFileBytes, err := getCertificate(certConfig)
	if err != nil {
		return nil, err
	}

	// Read key file
	keyFileBytes, err := getCertificate(keyConfig)
	if err != nil {
		return nil, err
	}

	// Decode PEM data
	keyBlock, _ := pem.Decode(keyFileBytes)

	if keyBlock == nil {
		return nil, fmt.Errorf("failed to decode PEM data for key")
	}

	// Check and Decrypt the the Key Block using passphrase
	if x509.IsEncryptedPEMBlock(keyBlock) { // nolint:staticcheck
		keyFilePassphraseBytes, err := getSecret(keyPassConfig)
		if err != nil {
			return nil, fmt.Errorf("failed to get key passphrase: `%s`", err)
		}

		decryptedDERBytes, err := x509.DecryptPEMBlock(keyBlock, keyFilePassphraseBytes) // nolint:staticcheck
		if err != nil {
			return nil, fmt.Errorf("failed to decrypt PEM Block: `%s`", err)
		}

		keyBlock.Bytes = decryptedDERBytes
		keyBlock.Headers = nil
	}

	// Encode PEM data
	keyPEM := pem.EncodeToMemory(keyBlock)

	if keyPEM == nil {
		return nil, fmt.Errorf("failed to encode PEM data for key")
	}

	cert, err := tls.X509KeyPair(certFileBytes, keyPEM)
	if err != nil {
		return nil, fmt.Errorf("failed to add certificate and key to the pool: `%s`", err)
	}

	certificates = append(certificates, cert)

	return certificates, nil
}

func sanitizeUTF8(lv string) string {
	if utf8.ValidString(lv) {
		return lv
	}
	fixUtf := func(r rune) rune {
		if r == utf8.RuneError {
			return 65533
		}
		return r
	}

	return strings.Map(fixUtf, lv)
}

func buildVersionGreaterThanOrEqual(rawMetrics map[string]string, ref string) (bool, error) {
	if len(rawMetrics["build"]) == 0 {
		return false, fmt.Errorf("couldn't get build version")
	}

	ver := rawMetrics["build"]
	version, err := goversion.NewVersion(ver)
	if err != nil {
		return false, fmt.Errorf("error parsing build version %s: %v", ver, err)
	}

	refVersion, err := goversion.NewVersion(ref)
	if err != nil {
		return false, fmt.Errorf("error parsing reference version %s: %v", ref, err)
	}

	if version.GreaterThanOrEqual(refVersion) {
		return true, nil
	}

	return false, nil
}
                                                    aerospike-prometheus-exporter/._config.go                                                           000644  000765  000024  00000000243 14426446031 022055  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/config.go                                                   000644  000765  000024  00000000207 14426446031 023611  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         29 mtime=1683639321.39181565
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                         aerospike-prometheus-exporter/config.go                                                             000644  000765  000024  00000023203 14426446031 021641  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"os"
	"strings"

	"github.com/BurntSushi/toml"

	aslog "github.com/aerospike/aerospike-client-go/v6/logger"
	log "github.com/sirupsen/logrus"
)

// Config represents the aerospike-prometheus-exporter configuration
type Config struct {
	AeroProm struct {
		CertFile          string `toml:"cert_file"`
		KeyFile           string `toml:"key_file"`
		RootCA            string `toml:"root_ca"`
		KeyFilePassphrase string `toml:"key_file_passphrase"`

		MetricLabels map[string]string `toml:"labels"`

		Bind    string `toml:"bind"`
		Timeout uint8  `toml:"timeout"`

		LogFile  string `toml:"log_file"`
		LogLevel string `toml:"log_level"`

		BasicAuthUsername string `toml:"basic_auth_username"`
		BasicAuthPassword string `toml:"basic_auth_password"`
	} `toml:"Agent"`

	Aerospike struct {
		Host string `toml:"db_host"`
		Port uint16 `toml:"db_port"`

		CertFile          string `toml:"cert_file"`
		KeyFile           string `toml:"key_file"`
		KeyFilePassphrase string `toml:"key_file_passphrase"`
		NodeTLSName       string `toml:"node_tls_name"`
		RootCA            string `toml:"root_ca"`

		AuthMode string `toml:"auth_mode"`
		User     string `toml:"user"`
		Password string `toml:"password"`

		Timeout uint8 `toml:"timeout"`

		LatencyBucketsCount uint8 `toml:"latency_buckets_count"`

		// Order of context ( from observer.go) - namespace, set, latencies, node-stats, xdr, user, jobs, sindex
		// Namespace metrics allow/block
		NamespaceMetricsAllowlist []string `toml:"namespace_metrics_allowlist"`
		NamespaceMetricsBlocklist []string `toml:"namespace_metrics_blocklist"`

		NamespaceMetricsAllowlistEnabled bool

		// Set metrics allow/block
		SetMetricsAllowlist []string `toml:"set_metrics_allowlist"`
		SetMetricsBlocklist []string `toml:"set_metrics_blocklist"`

		SetMetricsAllowlistEnabled bool

		// Latencies metrics allow/block
		LatenciesMetricsAllowlist []string `toml:"latencies_metrics_allowlist"`
		LatenciesMetricsBlocklist []string `toml:"latencies_metrics_blocklist"`

		LatenciesMetricsAllowlistEnabled bool

		// knob to disable latencies metrics collection (for internal use only, will be deprecated)
		DisableLatenciesMetrics bool `toml:"disable_latencies_metrics"`

		// Node metrics allow/block
		NodeMetricsAllowlist []string `toml:"node_metrics_allowlist"`
		NodeMetricsBlocklist []string `toml:"node_metrics_blocklist"`

		NodeMetricsAllowlistEnabled bool

		// Xdr metrics allow/block
		XdrMetricsAllowlist []string `toml:"xdr_metrics_allowlist"`
		XdrMetricsBlocklist []string `toml:"xdr_metrics_blocklist"`

		XdrMetricsAllowlistEnabled bool

		// User metrics allow/block
		UserMetricsUsersAllowlist []string `toml:"user_metrics_users_allowlist"`
		UserMetricsUsersBlocklist []string `toml:"user_metrics_users_blocklist"`

		UserMetricsUsersAllowlistEnabled bool

		// Job metrics allow/block
		JobMetricsAllowlist []string `toml:"job_metrics_allowlist"`
		JobMetricsBlocklist []string `toml:"job_metrics_blocklist"`

		JobMetricsAllowlistEnabled bool

		// knob to disable job metrics collection (for internal use only, will be deprecated)
		DisableJobMetrics bool `toml:"disable_job_metrics"`

		// Sindex metrics allow/block
		SindexMetricsAllowlist []string `toml:"sindex_metrics_allowlist"`
		SindexMetricsBlocklist []string `toml:"sindex_metrics_blocklist"`

		SindexMetricsAllowlistEnabled bool

		// knob to disable sindex metrics collection (for internal use only, will be deprecated)
		DisableSindexMetrics bool `toml:"disable_sindex_metrics"`

		// Tolerate older whitelist and blacklist configurations for a while
		NamespaceMetricsWhitelist []string `toml:"namespace_metrics_whitelist"`
		SetMetricsWhitelist       []string `toml:"set_metrics_whitelist"`
		NodeMetricsWhitelist      []string `toml:"node_metrics_whitelist"`
		XdrMetricsWhitelist       []string `toml:"xdr_metrics_whitelist"`

		NamespaceMetricsBlacklist []string `toml:"namespace_metrics_blacklist"`
		SetMetricsBlacklist       []string `toml:"set_metrics_blacklist"`
		NodeMetricsBlacklist      []string `toml:"node_metrics_blacklist"`
		XdrMetricsBlacklist       []string `toml:"xdr_metrics_blacklist"`
	} `toml:"Aerospike"`

	LogFile *os.File
}

// Validate and update exporter configuration
func (c *Config) validateAndUpdate() {
	if c.AeroProm.Bind == "" {
		c.AeroProm.Bind = ":9145"
	}

	if c.AeroProm.Timeout == 0 {
		c.AeroProm.Timeout = 5
	}

	if c.Aerospike.AuthMode == "" {
		c.Aerospike.AuthMode = "internal"
	}

	if c.Aerospike.Timeout == 0 {
		c.Aerospike.Timeout = 5
	}
}

// Initialize exporter configuration
func initConfig(configFile string, config *Config) {
	// to print everything out regarding reading the config in app init
	log.SetLevel(log.DebugLevel)

	log.Infof("Loading configuration file %s", configFile)
	blob, err := os.ReadFile(configFile)
	if err != nil {
		log.Fatalln(err)
	}

	md, err := toml.Decode(string(blob), &config)
	if err != nil {
		log.Fatalln(err)
	}

	initAllowlistAndBlocklistConfigs(config, md)

	config.LogFile = setLogFile(config.AeroProm.LogFile)

	aslog.Logger.SetLogger(log.StandardLogger())
	setLogLevel(config.AeroProm.LogLevel)
}

// Set log file path
func setLogFile(filepath string) *os.File {
	if len(strings.TrimSpace(filepath)) > 0 {
		out, err := os.OpenFile(filepath, os.O_RDWR|os.O_CREATE|os.O_APPEND, 0666)
		if err != nil {
			log.Fatalf("Error opening file: %v", err)
		}
		log.SetOutput(out)
		return out
	}

	return nil
}

// Set logging level
func setLogLevel(level string) {
	level = strings.ToLower(level)

	switch level {
	case "info":
		log.SetLevel(log.InfoLevel)
		aslog.Logger.SetLevel(aslog.INFO)
	case "warning", "warn":
		log.SetLevel(log.WarnLevel)
		aslog.Logger.SetLevel(aslog.WARNING)
	case "error", "err":
		log.SetLevel(log.ErrorLevel)
		aslog.Logger.SetLevel(aslog.ERR)
	case "debug":
		log.SetLevel(log.DebugLevel)
		aslog.Logger.SetLevel(aslog.DEBUG)
	case "trace":
		log.SetLevel(log.TraceLevel)
		aslog.Logger.SetLevel(aslog.DEBUG)
	default:
		log.SetLevel(log.InfoLevel)
		aslog.Logger.SetLevel(aslog.INFO)
	}
}

// Initialize Allowlist and Blocklist configurations
func initAllowlistAndBlocklistConfigs(config *Config, md toml.MetaData) {
	// Initialize AllowlistEnabled config
	config.Aerospike.NamespaceMetricsAllowlistEnabled = md.IsDefined("Aerospike", "namespace_metrics_allowlist")
	config.Aerospike.SetMetricsAllowlistEnabled = md.IsDefined("Aerospike", "set_metrics_allowlist")
	config.Aerospike.NodeMetricsAllowlistEnabled = md.IsDefined("Aerospike", "node_metrics_allowlist")
	config.Aerospike.XdrMetricsAllowlistEnabled = md.IsDefined("Aerospike", "xdr_metrics_allowlist")
	config.Aerospike.UserMetricsUsersAllowlistEnabled = md.IsDefined("Aerospike", "user_metrics_users_allowlist")
	config.Aerospike.JobMetricsAllowlistEnabled = md.IsDefined("Aerospike", "job_metrics_allowlist")
	config.Aerospike.SindexMetricsAllowlistEnabled = md.IsDefined("Aerospike", "sindex_metrics_allowlist")
	config.Aerospike.LatenciesMetricsAllowlistEnabled = md.IsDefined("Aerospike", "latencies_metrics_allowlist")

	// Tolerate older whitelist and blacklist configurations for a while.
	// If whitelist and blacklist configs are defined copy them into allowlist and blocklist.
	// Error out if both configurations are used at the same time.
	if md.IsDefined("Aerospike", "namespace_metrics_whitelist") {
		if config.Aerospike.NamespaceMetricsAllowlistEnabled {
			log.Fatalf("namespace_metrics_whitelist and namespace_metrics_allowlist are mutually exclusive!")
		}

		config.Aerospike.NamespaceMetricsAllowlistEnabled = true
		config.Aerospike.NamespaceMetricsAllowlist = config.Aerospike.NamespaceMetricsWhitelist
	}

	if md.IsDefined("Aerospike", "set_metrics_whitelist") {
		if config.Aerospike.SetMetricsAllowlistEnabled {
			log.Fatalf("set_metrics_whitelist and set_metrics_allowlist are mutually exclusive!")
		}

		config.Aerospike.SetMetricsAllowlistEnabled = true
		config.Aerospike.SetMetricsAllowlist = config.Aerospike.SetMetricsWhitelist
	}

	if md.IsDefined("Aerospike", "node_metrics_whitelist") {
		if config.Aerospike.NodeMetricsAllowlistEnabled {
			log.Fatalf("node_metrics_whitelist and node_metrics_allowlist are mutually exclusive!")
		}

		config.Aerospike.NodeMetricsAllowlistEnabled = true
		config.Aerospike.NodeMetricsAllowlist = config.Aerospike.NodeMetricsWhitelist
	}

	if md.IsDefined("Aerospike", "xdr_metrics_whitelist") {
		if config.Aerospike.XdrMetricsAllowlistEnabled {
			log.Fatalf("xdr_metrics_whitelist and xdr_metrics_allowlist are mutually exclusive!")
		}

		config.Aerospike.XdrMetricsAllowlistEnabled = true
		config.Aerospike.XdrMetricsAllowlist = config.Aerospike.XdrMetricsWhitelist
	}

	if md.IsDefined("Aerospike", "namespace_metrics_blacklist") {
		if len(config.Aerospike.NamespaceMetricsBlocklist) > 0 {
			log.Fatalf("namespace_metrics_blacklist and namespace_metrics_blocklist are mutually exclusive!")
		}

		config.Aerospike.NamespaceMetricsBlocklist = config.Aerospike.NamespaceMetricsBlacklist
	}

	if md.IsDefined("Aerospike", "set_metrics_blacklist") {
		if len(config.Aerospike.SetMetricsBlocklist) > 0 {
			log.Fatalf("set_metrics_blacklist and set_metrics_blocklist are mutually exclusive!")
		}

		config.Aerospike.SetMetricsBlocklist = config.Aerospike.SetMetricsBlacklist
	}

	if md.IsDefined("Aerospike", "node_metrics_blacklist") {
		if len(config.Aerospike.NodeMetricsBlocklist) > 0 {
			log.Fatalf("node_metrics_blacklist and node_metrics_blocklist are mutually exclusive!")
		}

		config.Aerospike.NodeMetricsBlocklist = config.Aerospike.NodeMetricsBlacklist
	}

	if md.IsDefined("Aerospike", "xdr_metrics_blacklist") {
		if len(config.Aerospike.XdrMetricsBlocklist) > 0 {
			log.Fatalf("xdr_metrics_blacklist and xdr_metrics_blocklist are mutually exclusive!")
		}

		config.Aerospike.XdrMetricsBlocklist = config.Aerospike.XdrMetricsBlacklist
	}
}
                                                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/._docker-entrypoint.sh                                                000644  000765  000024  00000000243 14426133132 024270  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/docker-entrypoint.sh                                        000644  000765  000024  00000000210 14426133132 026016  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.078782752
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/docker-entrypoint.sh                                                  000644  000765  000024  00000005010 14426133132 024050  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         #!/bin/sh
set -e

export AGENT_CERT_FILE=${AGENT_CERT_FILE:-""}
export AGENT_KEY_FILE=${AGENT_KEY_FILE:-""}
export AGENT_ROOT_CA=${AGENT_ROOT_CA:-""}
export AGENT_KEY_FILE_PASSPHRASE=${AGENT_KEY_FILE_PASSPHRASE:-""}
export METRIC_LABELS=${METRIC_LABELS:-""}
export AGENT_BIND_HOST=${AGENT_BIND_HOST:-""}
export AGENT_BIND_PORT=${AGENT_BIND_PORT:-9145}
export AGENT_TIMEOUT=${AGENT_TIMEOUT:-10}
export AGENT_LOG_FILE=${AGENT_LOG_FILE:-""}
export AGENT_LOG_LEVEL=${AGENT_LOG_LEVEL:-""}
export BASIC_AUTH_USERNAME=${BASIC_AUTH_USERNAME:-""}
export BASIC_AUTH_PASSWORD=${BASIC_AUTH_PASSWORD:-""}
export AS_HOST=${AS_HOST:-""}
export AS_PORT=${AS_PORT:-3000}
export AS_CERT_FILE=${AS_CERT_FILE:-""}
export AS_KEY_FILE=${AS_KEY_FILE:-""}
export AS_KEY_FILE_PASSPHRASE=${AS_KEY_FILE_PASSPHRASE:-""}
export AS_NODE_TLS_NAME=${AS_NODE_TLS_NAME:-""}
export AS_ROOT_CA=${AS_ROOT_CA:-""}
export AS_AUTH_MODE=${AS_AUTH_MODE:-""}
export AS_AUTH_USER=${AS_AUTH_USER:-""}
export AS_AUTH_PASSWORD=${AS_AUTH_PASSWORD:-""}
export TICKER_TIMEOUT=${TICKER_TIMEOUT:-5}
export LATENCY_BUCKETS_COUNT=${LATENCY_BUCKETS_COUNT:-0}
export NAMESPACE_METRICS_ALLOWLIST=${NAMESPACE_METRICS_ALLOWLIST:-""}
export SET_METRICS_ALLOWLIST=${SET_METRICS_ALLOWLIST:-""}
export NODE_METRICS_ALLOWLIST=${NODE_METRICS_ALLOWLIST:-""}
export XDR_METRICS_ALLOWLIST=${XDR_METRICS_ALLOWLIST:-""}
export NAMESPACE_METRICS_BLOCKLIST=${NAMESPACE_METRICS_BLOCKLIST:-""}
export SET_METRICS_BLOCKLIST=${SET_METRICS_BLOCKLIST:-""}
export NODE_METRICS_BLOCKLIST=${NODE_METRICS_BLOCKLIST:-""}
export XDR_METRICS_BLOCKLIST=${XDR_METRICS_BLOCKLIST:-""}
export USER_METRICS_USERS_ALLOWLIST=${USER_METRICS_USERS_ALLOWLIST:-""}
export USER_METRICS_USERS_BLOCKLIST=${USER_METRICS_USERS_BLOCKLIST:-""}
export JOB_METRICS_ALLOWLIST=${JOB_METRICS_ALLOWLIST:-""}
export JOB_METRICS_BLOCKLIST=${JOB_METRICS_BLOCKLIST:-""}
export SINDEX_METRICS_ALLOWLIST=${SINDEX_METRICS_ALLOWLIST:-""}
export SINDEX_METRICS_BLOCKLIST=${SINDEX_METRICS_BLOCKLIST:-""}

if [ -f /etc/aerospike-prometheus-exporter/ape.toml.template ]; then
        env | while IFS= read -r line; do
                name=${line%%=*}
                value=${line#*=}
                if [ -n "$value" ]; then
                        sed -i --regex "s/# (.*\{$name\}.*)/\1/" /etc/aerospike-prometheus-exporter/ape.toml.template
                fi
        done
        envsubst < /etc/aerospike-prometheus-exporter/ape.toml.template > /etc/aerospike-prometheus-exporter/ape.toml
fi

if [ "${1:0:1}" = '-' ]; then
        set -- aerospike-prometheus-exporter "$@"
fi

exec "$@"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/._go.mod                                                              000644  000765  000024  00000000243 14426143306 021366  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/go.mod                                                      000644  000765  000024  00000000207 14426143306 023122  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         29 mtime=1683539654.08975662
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                         aerospike-prometheus-exporter/go.mod                                                                000644  000765  000024  00000002050 14426143306 021147  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         module github.com/aerospike/aerospike-prometheus-exporter

go 1.20

require (
	github.com/BurntSushi/toml v1.2.1
	github.com/aerospike/aerospike-client-go/v6 v6.10.0
	github.com/gobwas/glob v0.2.3
	github.com/hashicorp/go-version v1.6.0
	github.com/prometheus/client_golang v1.14.0
	github.com/prometheus/client_model v0.3.0
	github.com/sirupsen/logrus v1.9.0
	github.com/stretchr/testify v1.8.0
)

require (
	github.com/beorn7/perks v1.0.1 // indirect
	github.com/cespare/xxhash/v2 v2.2.0 // indirect
	github.com/davecgh/go-spew v1.1.1 // indirect
	github.com/golang/protobuf v1.5.2 // indirect
	github.com/kr/pretty v0.3.1 // indirect
	github.com/matttproud/golang_protobuf_extensions v1.0.4 // indirect
	github.com/pmezard/go-difflib v1.0.0 // indirect
	github.com/prometheus/common v0.39.0 // indirect
	github.com/prometheus/procfs v0.9.0 // indirect
	github.com/yuin/gopher-lua v1.1.0 // indirect
	golang.org/x/sync v0.1.0 // indirect
	golang.org/x/sys v0.5.0 // indirect
	google.golang.org/protobuf v1.28.1 // indirect
	gopkg.in/yaml.v3 v3.0.1 // indirect
)
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/._go.sum                                                              000644  000765  000024  00000000243 14426143306 021413  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/go.sum                                                      000644  000765  000024  00000000210 14426143306 023141  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.089950522
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/go.sum                                                                000644  000765  000024  00000036242 14426143306 021206  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         github.com/BurntSushi/toml v1.2.1 h1:9F2/+DoOYIOksmaJFPw1tGFy1eDnIJXg+UHjuD8lTak=
github.com/BurntSushi/toml v1.2.1/go.mod h1:CxXYINrC8qIiEnFrOxCa7Jy5BFHlXnUU2pbicEuybxQ=
github.com/aerospike/aerospike-client-go/v6 v6.10.0 h1:dqnYUuMJwnUNsylaOOzs7oEnBkoxApwfdUT2KE6UknA=
github.com/aerospike/aerospike-client-go/v6 v6.10.0/go.mod h1:Do5/flmgSo2X32YLGAYd6o5e/U2gOSpgEhrIGyOS3UI=
github.com/beorn7/perks v1.0.1 h1:VlbKKnNfV8bJzeqoa4cOKqO6bYr3WgKZxO8Z16+hsOM=
github.com/beorn7/perks v1.0.1/go.mod h1:G2ZrVWU2WbWT9wwq4/hrbKbnv/1ERSJQ0ibhJ6rlkpw=
github.com/cespare/xxhash/v2 v2.2.0 h1:DC2CZ1Ep5Y4k3ZQ899DldepgrayRUGE6BBZ/cd9Cj44=
github.com/cespare/xxhash/v2 v2.2.0/go.mod h1:VGX0DQ3Q6kWi7AoAeZDth3/j3BFtOZR5XLFGgcrjCOs=
github.com/chzyer/logex v1.1.10/go.mod h1:+Ywpsq7O8HXn0nuIou7OrIPyXbp3wmkHB+jjWRnGsAI=
github.com/chzyer/readline v0.0.0-20180603132655-2972be24d48e/go.mod h1:nSuG5e5PlCu98SY8svDHJxuZscDgtXS6KTTbou5AhLI=
github.com/chzyer/test v0.0.0-20180213035817-a1ea475d72b1/go.mod h1:Q3SI9o4m/ZMnBNeIyt5eFwwo7qiLfzFZmjNmxjkiQlU=
github.com/creack/pty v1.1.9/go.mod h1:oKZEueFk5CKHvIhNR5MUki03XCEU+Q6VDXinZuGJ33E=
github.com/davecgh/go-spew v1.1.0/go.mod h1:J7Y8YcW2NihsgmVo/mv3lAwl/skON4iLHjSsI+c5H38=
github.com/davecgh/go-spew v1.1.1 h1:vj9j/u1bqnvCEfJOwUhtlOARqs3+rkHYY13jYWTU97c=
github.com/davecgh/go-spew v1.1.1/go.mod h1:J7Y8YcW2NihsgmVo/mv3lAwl/skON4iLHjSsI+c5H38=
github.com/fsnotify/fsnotify v1.4.7/go.mod h1:jwhsz4b93w/PPRr/qN1Yymfu8t87LnFCMoQvtojpjFo=
github.com/fsnotify/fsnotify v1.4.9 h1:hsms1Qyu0jgnwNXIxa+/V/PDsU6CfLf6CNO8H7IWoS4=
github.com/fsnotify/fsnotify v1.4.9/go.mod h1:znqG4EE+3YCdAaPaxE2ZRY/06pZUdp0tY4IgpuI1SZQ=
github.com/go-task/slim-sprig v0.0.0-20210107165309-348f09dbbbc0/go.mod h1:fyg7847qk6SyHyPtNmDHnmrv/HOrqktSC+C9fM+CJOE=
github.com/gobwas/glob v0.2.3 h1:A4xDbljILXROh+kObIiy5kIaPYD8e96x1tgBhUI5J+Y=
github.com/gobwas/glob v0.2.3/go.mod h1:d3Ez4x06l9bZtSvzIay5+Yzi0fmZzPgnTbPcKjJAkT8=
github.com/golang/protobuf v1.2.0/go.mod h1:6lQm79b+lXiMfvg/cZm0SGofjICqVBUtrP5yJMmIC1U=
github.com/golang/protobuf v1.3.5/go.mod h1:6O5/vntMXwX2lRkT1hjjk0nAC1IDOTvTlVgjlRvqsdk=
github.com/golang/protobuf v1.4.0-rc.1/go.mod h1:ceaxUfeHdC40wWswd/P6IGgMaK3YpKi5j83Wpe3EHw8=
github.com/golang/protobuf v1.4.0-rc.1.0.20200221234624-67d41d38c208/go.mod h1:xKAWHe0F5eneWXFV3EuXVDTCmh+JuBKY0li0aMyXATA=
github.com/golang/protobuf v1.4.0-rc.2/go.mod h1:LlEzMj4AhA7rCAGe4KMBDvJI+AwstrUpVNzEA03Pprs=
github.com/golang/protobuf v1.4.0-rc.4.0.20200313231945-b860323f09d0/go.mod h1:WU3c8KckQ9AFe+yFwt9sWVRKCVIyN9cPHBJSNnbL67w=
github.com/golang/protobuf v1.4.0/go.mod h1:jodUvKwWbYaEsadDk5Fwe5c77LiNKVO9IDvqG2KuDX0=
github.com/golang/protobuf v1.4.2/go.mod h1:oDoupMAO8OvCJWAcko0GGGIgR6R6ocIYbsSw735rRwI=
github.com/golang/protobuf v1.5.0/go.mod h1:FsONVRAS9T7sI+LIUmWTfcYkHO4aIWwzhcaSAoJOfIk=
github.com/golang/protobuf v1.5.2 h1:ROPKBNFfQgOUMifHyP+KYbvpjbdoFNs+aK7DXlji0Tw=
github.com/golang/protobuf v1.5.2/go.mod h1:XVQd3VNwM+JqD3oG2Ue2ip4fOMUkwXdXDdiuN0vRsmY=
github.com/google/go-cmp v0.3.0/go.mod h1:8QqcDgzrUqlUb/G2PQTWiueGozuR1884gddMywk6iLU=
github.com/google/go-cmp v0.3.1/go.mod h1:8QqcDgzrUqlUb/G2PQTWiueGozuR1884gddMywk6iLU=
github.com/google/go-cmp v0.4.0/go.mod h1:v8dTdLbMG2kIc/vJvl+f65V22dbkXbowE6jgT/gNBxE=
github.com/google/go-cmp v0.5.5/go.mod h1:v8dTdLbMG2kIc/vJvl+f65V22dbkXbowE6jgT/gNBxE=
github.com/google/go-cmp v0.5.9 h1:O2Tfq5qg4qc4AmwVlvv0oLiVAGB7enBSJ2x2DqQFi38=
github.com/hashicorp/go-version v1.6.0 h1:feTTfFNnjP967rlCxM/I9g701jU+RN74YKx2mOkIeek=
github.com/hashicorp/go-version v1.6.0/go.mod h1:fltr4n8CU8Ke44wwGCBoEymUuxUHl09ZGVZPK5anwXA=
github.com/hpcloud/tail v1.0.0/go.mod h1:ab1qPbhIpdTxEkNHXyeSf5vhxWSCs/tWer42PpOxQnU=
github.com/k0kubun/pp v3.0.1+incompatible/go.mod h1:GWse8YhT0p8pT4ir3ZgBbfZild3tgzSScAn6HmfYukg=
github.com/k0kubun/pp/v3 v3.1.0/go.mod h1:vIrP5CF0n78pKHm2Ku6GVerpZBJvscg48WepUYEk2gw=
github.com/kr/pretty v0.3.1 h1:flRD4NNwYAUpkphVc1HcthR4KEIFJ65n8Mw5qdRn3LE=
github.com/kr/pretty v0.3.1/go.mod h1:hoEshYVHaxMs3cyo3Yncou5ZscifuDolrwPKZanG3xk=
github.com/kr/text v0.2.0 h1:5Nx0Ya0ZqY2ygV366QzturHI13Jq95ApcVaJBhpS+AY=
github.com/kr/text v0.2.0/go.mod h1:eLer722TekiGuMkidMxC/pM04lWEeraHUUmBw8l2grE=
github.com/mattn/go-colorable v0.1.12/go.mod h1:u5H1YNBxpqRaxsYJYSkiCWKzEfiAb1Gb520KVy5xxl4=
github.com/mattn/go-isatty v0.0.14/go.mod h1:7GGIvUiUoEMVVmxf/4nioHXj79iQHKdU27kJ6hsGG94=
github.com/matttproud/golang_protobuf_extensions v1.0.4 h1:mmDVorXM7PCGKw94cs5zkfA9PSy5pEvNWRP0ET0TIVo=
github.com/matttproud/golang_protobuf_extensions v1.0.4/go.mod h1:BSXmuO+STAnVfrANrmjBb36TMTDstsz7MSK+HVaYKv4=
github.com/nxadm/tail v1.4.4/go.mod h1:kenIhsEOeOJmVchQTgglprH7qJGnHDVpk1VPCcaMI8A=
github.com/nxadm/tail v1.4.8 h1:nPr65rt6Y5JFSKQO7qToXr7pePgD6Gwiw05lkbyAQTE=
github.com/nxadm/tail v1.4.8/go.mod h1:+ncqLTQzXmGhMZNUePPaPqPvBxHAIsmXswZKocGu+AU=
github.com/onsi/ginkgo v1.6.0/go.mod h1:lLunBs/Ym6LB5Z9jYTR76FiuTmxDTDusOGeTQH+WWjE=
github.com/onsi/ginkgo v1.12.1/go.mod h1:zj2OWP4+oCPe1qIXoGWkgMRwljMUYCdkwsT2108oapk=
github.com/onsi/ginkgo v1.16.4 h1:29JGrr5oVBm5ulCWet69zQkzWipVXIol6ygQUe/EzNc=
github.com/onsi/ginkgo v1.16.4/go.mod h1:dX+/inL/fNMqNlz0e9LfyB9TswhZpCVdJM/Z6Vvnwo0=
github.com/onsi/gomega v1.7.1/go.mod h1:XdKZgCCFLUoM/7CFJVPcG8C1xQ1AJ0vpAezJrB7JYyY=
github.com/onsi/gomega v1.10.1/go.mod h1:iN09h71vgCQne3DLsj+A5owkum+a2tYe+TOCB1ybHNo=
github.com/onsi/gomega v1.15.0 h1:WjP/FQ/sk43MRmnEcT+MlDw2TFvkrXlprrPST/IudjU=
github.com/onsi/gomega v1.15.0/go.mod h1:cIuvLEne0aoVhAgh/O6ac0Op8WWw9H6eYCriF+tEHG0=
github.com/pkg/diff v0.0.0-20210226163009-20ebb0f2a09e/go.mod h1:pJLUxLENpZxwdsKMEsNbx1VGcRFpLqf3715MtcvvzbA=
github.com/pmezard/go-difflib v1.0.0 h1:4DBwDE0NGyQoBHbLQYPwSUPoCMWR5BEzIk/f1lZbAQM=
github.com/pmezard/go-difflib v1.0.0/go.mod h1:iKH77koFhYxTK1pcRnkKkqfTogsbg7gZNVY4sRDYZ/4=
github.com/prometheus/client_golang v1.14.0 h1:nJdhIvne2eSX/XRAFV9PcvFFRbrjbcTUj0VP62TMhnw=
github.com/prometheus/client_golang v1.14.0/go.mod h1:8vpkKitgIVNcqrRBWh1C4TIUQgYNtG/XQE4E/Zae36Y=
github.com/prometheus/client_model v0.3.0 h1:UBgGFHqYdG/TPFD1B1ogZywDqEkwp3fBMvqdiQ7Xew4=
github.com/prometheus/client_model v0.3.0/go.mod h1:LDGWKZIo7rky3hgvBe+caln+Dr3dPggB5dvjtD7w9+w=
github.com/prometheus/common v0.39.0 h1:oOyhkDq05hPZKItWVBkJ6g6AtGxi+fy7F4JvUV8uhsI=
github.com/prometheus/common v0.39.0/go.mod h1:6XBZ7lYdLCbkAVhwRsWTZn+IN5AB9F/NXd5w0BbEX0Y=
github.com/prometheus/procfs v0.9.0 h1:wzCHvIvM5SxWqYvwgVL7yJY8Lz3PKn49KQtpgMYJfhI=
github.com/prometheus/procfs v0.9.0/go.mod h1:+pB4zwohETzFnmlpe6yd2lSc+0/46IYZRB/chUwxUZY=
github.com/rogpeppe/go-internal v1.9.0 h1:73kH8U+JUqXU8lRuOHeVHaa/SZPifC7BkcraZVejAe8=
github.com/rogpeppe/go-internal v1.9.0/go.mod h1:WtVeX8xhTBvf0smdhujwtBcq4Qrzq/fJaraNFVN+nFs=
github.com/sirupsen/logrus v1.9.0 h1:trlNQbNUG3OdDrDil03MCb1H2o9nJ1x4/5LYw7byDE0=
github.com/sirupsen/logrus v1.9.0/go.mod h1:naHLuLoDiP4jHNo9R0sCBMtWGeIprob74mVsIT4qYEQ=
github.com/stretchr/objx v0.1.0/go.mod h1:HFkY916IF+rwdDfMAkV7OtwuqBVzrE8GR6GFx+wExME=
github.com/stretchr/objx v0.4.0/go.mod h1:YvHI0jy2hoMjB+UWwv71VJQ9isScKT/TqJzVSSt89Yw=
github.com/stretchr/testify v1.5.1/go.mod h1:5W2xD1RspED5o8YsWQXVCued0rvSQ+mT+I5cxcmMvtA=
github.com/stretchr/testify v1.7.0/go.mod h1:6Fq8oRcR53rry900zMqJjRRixrwX3KX962/h/Wwjteg=
github.com/stretchr/testify v1.7.1/go.mod h1:6Fq8oRcR53rry900zMqJjRRixrwX3KX962/h/Wwjteg=
github.com/stretchr/testify v1.8.0 h1:pSgiaMZlXftHpm5L7V1+rVB+AZJydKsMxsQBIJw4PKk=
github.com/stretchr/testify v1.8.0/go.mod h1:yNjHg4UonilssWZ8iaSj1OCr/vHnekPRkoO+kdMU+MU=
github.com/yuin/goldmark v1.2.1/go.mod h1:3hX8gzYuyVAZsxl0MRgGTJEmQBFcNTphYh9decYSb74=
github.com/yuin/goldmark v1.3.5/go.mod h1:mwnBkeHKe2W/ZEtQ+71ViKU8L12m81fl3OWwC1Zlc8k=
github.com/yuin/gopher-lua v0.0.0-20200816102855-ee81675732da/go.mod h1:E1AXubJBdNmFERAOucpDIxNzeGfLzg0mYh+UfMWdChA=
github.com/yuin/gopher-lua v1.1.0 h1:BojcDhfyDWgU2f2TOzYK/g5p2gxMrku8oupLDqlnSqE=
github.com/yuin/gopher-lua v1.1.0/go.mod h1:GBR0iDaNXjAgGg9zfCvksxSRnQx76gclCIb7kdAd1Pw=
golang.org/x/crypto v0.0.0-20190308221718-c2843e01d9a2/go.mod h1:djNgcEr1/C05ACkg1iLfiJU5Ep61QUkGW8qpdssI0+w=
golang.org/x/crypto v0.0.0-20191011191535-87dc89f01550/go.mod h1:yigFU9vqHzYiE8UmvKecakEJjdnWj3jj499lnFckfCI=
golang.org/x/crypto v0.0.0-20200622213623-75b288015ac9/go.mod h1:LzIPMQfyMNhhGPhUkYOs5KpL4U8rLKemX1yGLhDgUto=
golang.org/x/mod v0.3.0/go.mod h1:s0Qsj1ACt9ePp/hMypM3fl4fZqREWJwdYDEqhRiZZUA=
golang.org/x/mod v0.4.2/go.mod h1:s0Qsj1ACt9ePp/hMypM3fl4fZqREWJwdYDEqhRiZZUA=
golang.org/x/net v0.0.0-20180906233101-161cd47e91fd/go.mod h1:mL1N/T3taQHkDXs73rZJwtUhF3w3ftmwwsq0BUmARs4=
golang.org/x/net v0.0.0-20190404232315-eb5bcb51f2a3/go.mod h1:t9HGtf8HONx5eT2rtn7q6eTqICYqUVnKs3thJo3Qplg=
golang.org/x/net v0.0.0-20190620200207-3b0461eec859/go.mod h1:z5CRVTTTmAJ677TzLLGU+0bjPO0LkuOLi4/5GtJWs/s=
golang.org/x/net v0.0.0-20200520004742-59133d7f0dd7/go.mod h1:qpuaurCH72eLCgpAm/N6yyVIVM9cpaDIP3A8BGJEC5A=
golang.org/x/net v0.0.0-20201021035429-f5854403a974/go.mod h1:sp8m0HH+o8qH0wwXwYZr8TS3Oi6o0r6Gce1SSxlDquU=
golang.org/x/net v0.0.0-20210405180319-a5a99cb37ef4/go.mod h1:p54w0d4576C0XHj96bSt6lcn1PtDYWL6XObtHCRCNQM=
golang.org/x/net v0.0.0-20210428140749-89ef3d95e781/go.mod h1:OJAsFXCWl8Ukc7SiCT/9KSuxbyM7479/AVlXFRxuMCk=
golang.org/x/net v0.0.0-20210805182204-aaa1db679c0d/go.mod h1:9nx3DQGgdP8bBQD5qxJ1jj9UTztislL4KSBs9R2vV5Y=
golang.org/x/net v0.4.0 h1:Q5QPcMlvfxFTAPV0+07Xz/MpK9NTXu2VDUuy0FeMfaU=
golang.org/x/sync v0.0.0-20180314180146-1d60e4601c6f/go.mod h1:RxMgew5VJxzue5/jJTE5uejpjVlOe/izrB70Jof72aM=
golang.org/x/sync v0.0.0-20181221193216-37e7f081c4d4/go.mod h1:RxMgew5VJxzue5/jJTE5uejpjVlOe/izrB70Jof72aM=
golang.org/x/sync v0.0.0-20190423024810-112230192c58/go.mod h1:RxMgew5VJxzue5/jJTE5uejpjVlOe/izrB70Jof72aM=
golang.org/x/sync v0.0.0-20201020160332-67f06af15bc9/go.mod h1:RxMgew5VJxzue5/jJTE5uejpjVlOe/izrB70Jof72aM=
golang.org/x/sync v0.0.0-20210220032951-036812b2e83c/go.mod h1:RxMgew5VJxzue5/jJTE5uejpjVlOe/izrB70Jof72aM=
golang.org/x/sync v0.1.0 h1:wsuoTGHzEhffawBOhz5CYhcrV4IdKZbEyZjBMuTp12o=
golang.org/x/sync v0.1.0/go.mod h1:RxMgew5VJxzue5/jJTE5uejpjVlOe/izrB70Jof72aM=
golang.org/x/sys v0.0.0-20180909124046-d0be0721c37e/go.mod h1:STP8DvDyc/dI5b8T5hshtkjS+E42TnysNCUPdjciGhY=
golang.org/x/sys v0.0.0-20190204203706-41f3e6584952/go.mod h1:STP8DvDyc/dI5b8T5hshtkjS+E42TnysNCUPdjciGhY=
golang.org/x/sys v0.0.0-20190215142949-d0b11bdaac8a/go.mod h1:STP8DvDyc/dI5b8T5hshtkjS+E42TnysNCUPdjciGhY=
golang.org/x/sys v0.0.0-20190412213103-97732733099d/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20190904154756-749cb33beabd/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20191005200804-aed5e4c7ecf9/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20191120155948-bd437916bb0e/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20200323222414-85ca7c5b95cd/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20200930185726-fdedc70b468f/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20201119102817-f84b799fce68/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20210112080510-489259a85091/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20210330210617-4fbd30eecc44/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20210423082822-04245dca01da/go.mod h1:h1NjWce9XRLGQEsW7wpKNCjG9DtNlClVuFLEZdDNbEs=
golang.org/x/sys v0.0.0-20210510120138-977fb7262007/go.mod h1:oPkhp1MJrh7nUepCBck5+mAzfO9JrbApNNgaTdGDITg=
golang.org/x/sys v0.0.0-20210630005230-0f9fa26af87c/go.mod h1:oPkhp1MJrh7nUepCBck5+mAzfO9JrbApNNgaTdGDITg=
golang.org/x/sys v0.0.0-20210927094055-39ccf1dd6fa6/go.mod h1:oPkhp1MJrh7nUepCBck5+mAzfO9JrbApNNgaTdGDITg=
golang.org/x/sys v0.0.0-20220715151400-c0bba94af5f8/go.mod h1:oPkhp1MJrh7nUepCBck5+mAzfO9JrbApNNgaTdGDITg=
golang.org/x/sys v0.5.0 h1:MUK/U/4lj1t1oPg0HfuXDN/Z1wv31ZJ/YcPiGccS4DU=
golang.org/x/sys v0.5.0/go.mod h1:oPkhp1MJrh7nUepCBck5+mAzfO9JrbApNNgaTdGDITg=
golang.org/x/term v0.0.0-20201126162022-7de9c90e9dd1/go.mod h1:bj7SfCRtBDWHUb9snDiAeCFNEtKQo2Wmx5Cou7ajbmo=
golang.org/x/text v0.3.0/go.mod h1:NqM8EUOU14njkJ3fqMW+pc6Ldnwhi/IjpwHt7yyuwOQ=
golang.org/x/text v0.3.3/go.mod h1:5Zoc/QRtKVWzQhOtBMvqHzDpF6irO9z98xDceosuGiQ=
golang.org/x/text v0.3.6/go.mod h1:5Zoc/QRtKVWzQhOtBMvqHzDpF6irO9z98xDceosuGiQ=
golang.org/x/text v0.3.7/go.mod h1:u+2+/6zg+i71rQMx5EYifcz6MCKuco9NR6JIITiCfzQ=
golang.org/x/text v0.5.0 h1:OLmvp0KP+FVG99Ct/qFiL/Fhk4zp4QQnZ7b2U+5piUM=
golang.org/x/tools v0.0.0-20180917221912-90fa682c2a6e/go.mod h1:n7NCudcB/nEzxVGmLbDWY5pfWTLqBcC2KZ6jyYvM4mQ=
golang.org/x/tools v0.0.0-20191119224855-298f0cb1881e/go.mod h1:b+2E5dAYhXwXZwtnZ6UAqBI28+e2cm9otk0dWdXHAEo=
golang.org/x/tools v0.0.0-20201224043029-2b0845dc783e/go.mod h1:emZCQorbCU4vsT4fOWvOPXz4eW1wZW4PmDk9uLelYpA=
golang.org/x/tools v0.1.5/go.mod h1:o0xws9oXOQQZyjljx8fwUC0k7L1pTE6eaCbjGeHmOkk=
golang.org/x/xerrors v0.0.0-20190717185122-a985d3407aa7/go.mod h1:I/5z698sn9Ka8TeJc9MKroUUfqBBauWjQqLJ2OPfmY0=
golang.org/x/xerrors v0.0.0-20191011141410-1b5146add898/go.mod h1:I/5z698sn9Ka8TeJc9MKroUUfqBBauWjQqLJ2OPfmY0=
golang.org/x/xerrors v0.0.0-20191204190536-9bdfabe68543/go.mod h1:I/5z698sn9Ka8TeJc9MKroUUfqBBauWjQqLJ2OPfmY0=
golang.org/x/xerrors v0.0.0-20200804184101-5ec99f83aff1/go.mod h1:I/5z698sn9Ka8TeJc9MKroUUfqBBauWjQqLJ2OPfmY0=
google.golang.org/protobuf v0.0.0-20200109180630-ec00e32a8dfd/go.mod h1:DFci5gLYBciE7Vtevhsrf46CRTquxDuWsQurQQe4oz8=
google.golang.org/protobuf v0.0.0-20200221191635-4d8936d0db64/go.mod h1:kwYJMbMJ01Woi6D6+Kah6886xMZcty6N08ah7+eCXa0=
google.golang.org/protobuf v0.0.0-20200228230310-ab0ca4ff8a60/go.mod h1:cfTl7dwQJ+fmap5saPgwCLgHXTUD7jkjRqWcaiX5VyM=
google.golang.org/protobuf v1.20.1-0.20200309200217-e05f789c0967/go.mod h1:A+miEFZTKqfCUM6K7xSMQL9OKL/b6hQv+e19PK+JZNE=
google.golang.org/protobuf v1.21.0/go.mod h1:47Nbq4nVaFHyn7ilMalzfO3qCViNmqZ2kzikPIcrTAo=
google.golang.org/protobuf v1.23.0/go.mod h1:EGpADcykh3NcUnDUJcl1+ZksZNG86OlYog2l/sGQquU=
google.golang.org/protobuf v1.26.0-rc.1/go.mod h1:jlhhOSvTdKEhbULTjvd4ARK9grFBp09yW+WbY/TyQbw=
google.golang.org/protobuf v1.26.0/go.mod h1:9q0QmTI4eRPtz6boOQmLYwt+qCgq0jsYwAQnmE0givc=
google.golang.org/protobuf v1.28.1 h1:d0NfwRgPtno5B1Wa6L2DAG+KivqkdutMf1UhdNx175w=
google.golang.org/protobuf v1.28.1/go.mod h1:HV8QOd/L58Z+nl8r43ehVNZIU/HEI6OcFqwMG9pJV4I=
gopkg.in/check.v1 v0.0.0-20161208181325-20d25e280405/go.mod h1:Co6ibVJAznAaIkqp8huTwlJQCZ016jof/cbN4VW5Yz0=
gopkg.in/check.v1 v1.0.0-20201130134442-10cb98267c6c h1:Hei/4ADfdWqJk1ZMxUNpqntNwaWcugrBjAiHlqqRiVk=
gopkg.in/fsnotify.v1 v1.4.7/go.mod h1:Tz8NjZHkW78fSQdbUxIjBTcgA1z1m8ZHf0WmKUhAMys=
gopkg.in/tomb.v1 v1.0.0-20141024135613-dd632973f1e7 h1:uRGJdciOHaEIrze2W8Q3AKkepLTh2hOroT7a+7czfdQ=
gopkg.in/tomb.v1 v1.0.0-20141024135613-dd632973f1e7/go.mod h1:dt/ZhP58zS4L8KSrWDmTeBkI65Dw0HsyUHuEVlX15mw=
gopkg.in/yaml.v2 v2.2.2/go.mod h1:hI93XBmqTisBFMUTm0b8Fm+jr3Dg1NNxqwp+5A1VGuI=
gopkg.in/yaml.v2 v2.2.4/go.mod h1:hI93XBmqTisBFMUTm0b8Fm+jr3Dg1NNxqwp+5A1VGuI=
gopkg.in/yaml.v2 v2.3.0/go.mod h1:hI93XBmqTisBFMUTm0b8Fm+jr3Dg1NNxqwp+5A1VGuI=
gopkg.in/yaml.v2 v2.4.0 h1:D8xgwECY7CYvx+Y2n4sBz93Jn9JRvxdiyyo8CTfuKaY=
gopkg.in/yaml.v2 v2.4.0/go.mod h1:RDklbk79AGWmwhnvt/jBztapEOGDOx6ZbXqjP6csGnQ=
gopkg.in/yaml.v3 v3.0.0-20200313102051-9f266ea9e77c/go.mod h1:K4uyk7z7BCEPqu6E+C64Yfv1cQ7kz7rIZviUmN+EgEM=
gopkg.in/yaml.v3 v3.0.1 h1:fxVm/GzAzEWqLHuvctI91KS9hhNmmWOoWu0XTYJS7CA=
gopkg.in/yaml.v3 v3.0.1/go.mod h1:K4uyk7z7BCEPqu6E+C64Yfv1cQ7kz7rIZviUmN+EgEM=
                                                                                                                                                                                                                                                                                                                                                              aerospike-prometheus-exporter/._helper_test.go                                                      000644  000765  000024  00000000243 14426143306 023125  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/helper_test.go                                              000644  000765  000024  00000000210 14426143306 024653  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.090088303
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/helper_test.go                                                        000644  000765  000024  00000003551 14426143306 022715  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"fmt"
	"strconv"
	"strings"
)

var DEFAULT_APE_TOML = "tests/default_ape.toml"
var NS_ALLOWLIST_APE_TOML = "tests/ns_allow_block_list_ape.toml"

// var g_ns_metric_allow_list = []string{"aerospike_namespace_master_objects", "aerospike_namespace_memory_used_bytes"}

func extractNamespaceFromLabel(label string) string {
	// [name:"cluster_name" value:""  name:"ns" value:"bar"  name:"service" value:"" ]
	nsFromLabel := label
	nsFromLabel = nsFromLabel[(strings.Index(nsFromLabel, "ns"))+11:]
	nsFromLabel = nsFromLabel[0:(strings.Index(nsFromLabel, "\""))]

	return nsFromLabel
}

func extractMetricNameFromDesc(desc string) string {
	// Desc{fqName: "aerospike_namespac_memory_free_pct", help: "memory free pct", constLabels: {}, variableLabels: [cluster_name service ns]}
	// fmt.Println("description given: ===> ", desc)
	metricNameFromDesc := desc[0 : (strings.Index(desc, ","))-1]
	metricNameFromDesc = metricNameFromDesc[(strings.Index(metricNameFromDesc, ":"))+3:]

	return strings.Trim(metricNameFromDesc, " ")
}

func makeKeyname(a string, b string, combineBoth bool) string {
	if combineBoth {
		return a + "/" + b
	}
	return a
}

func splitAndRetrieveStats(s, sep string) map[string]string {
	stats := make(map[string]string, strings.Count(s, sep)+1)
	s2 := strings.Split(s, sep)
	for _, s := range s2 {
		list := strings.SplitN(s, "=", 2)
		switch len(list) {
		case 0, 1:
		case 2:
			stats[list[0]] = list[1]
		default:
			stats[list[0]] = strings.Join(list[1:], "=")
		}
	}

	return stats
}

func convertValue(s string) (float64, error) {
	if f, err := strconv.ParseFloat(s, 64); err == nil {
		return f, nil
	}

	if b, err := strconv.ParseBool(s); err == nil {
		if b {
			return 1, nil
		}
		return 0, nil
	}

	// fmt.Println("input string is ", s, " **** returning 0")
	return 0, fmt.Errorf("invalid value `%s`. Only Float or Boolean are accepted", s)
}
                                                                                                                                                       aerospike-prometheus-exporter/._info_parser.go                                                      000644  000765  000024  00000000243 14426133132 023112  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/info_parser.go                                              000644  000765  000024  00000000210 14426133132 024640  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.079434458
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/info_parser.go                                                        000644  000765  000024  00000002614 14426133132 022701  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"bufio"
	"fmt"
	"strings"
)

// InfoParser provides a reader for Aerospike cluster's response for any of the metric
type InfoParser struct {
	*bufio.Reader
}

// NewInfoParser provides an instance of the InfoParser
func NewInfoParser(s string) *InfoParser {
	return &InfoParser{bufio.NewReader(strings.NewReader(s))}
}

// PeekAndExpect checks if the expected value is present without advancing the reader
func (ip *InfoParser) PeekAndExpect(s string) error {
	bytes, err := ip.Peek(len(s))
	if err != nil {
		return err
	}

	v := string(bytes)
	if v != s {
		return fmt.Errorf("InfoParser: Wrong value. Peek expected %s, but found %s", s, v)
	}

	return nil
}

// Expect validates the expected value against the one returned by the InfoParser
// This advances the reader by length of the input string.
func (ip *InfoParser) Expect(s string) error {
	bytes := make([]byte, len(s))

	v, err := ip.Read(bytes)
	if err != nil {
		return err
	}

	if string(bytes) != s {
		return fmt.Errorf("InfoParser: Wrong value. Expected %s, found %d", s, v)
	}

	return nil
}

// ReadUntil reads bytes from the InfoParser by handeling some edge-cases
func (ip *InfoParser) ReadUntil(delim byte) (string, error) {
	v, err := ip.ReadBytes(delim)

	switch len(v) {
	case 0:
		return string(v), err
	case 1:
		if v[0] == delim {
			return "", err
		}
		return string(v), err
	}

	return string(v[:len(v)-1]), err
}
                                                                                                                    aerospike-prometheus-exporter/._latency_parser.go                                                   000644  000765  000024  00000000243 14426133132 023616  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/latency_parser.go                                           000644  000765  000024  00000000210 14426133132 025344  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.079579458
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/latency_parser.go                                                     000644  000765  000024  00000013740 14426133132 023407  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"io"
	"strconv"
	"strings"

	log "github.com/sirupsen/logrus"
)

// Parse "latency:" info output.
//
// Format (with and without latency data)
// {test}-read:10:17:37-GMT,ops/sec,>1ms,>8ms,>64ms;10:17:47,29648.2,3.44,0.08,0.00;
// error-no-data-yet-or-back-too-small;
// or,
// {test}-write:;
func parseLatencyInfoLegacy(s string, latencyBucketsCount int) map[string]StatsMap {
	ip := NewInfoParser(s)
	res := map[string]StatsMap{}

	for {
		namespaceName, operation, err := readNamespaceAndOperation(ip)

		if err != nil {
			break
		}

		if namespaceName == "" && operation == "" {
			continue
		}

		// Might be an empty output if there's no latency data (in 5.1), so continue to next section
		if err := ip.PeekAndExpect(";"); err == nil {
			if err := ip.Expect(";"); err != nil {
				break
			}
			continue
		}

		// Ignore timestamp
		_, err = ip.ReadUntil(',')
		if err != nil {
			break
		}

		// Read bucket labels including ops/sec
		bucketLabelsStr, err := ip.ReadUntil(';')
		if err != nil {
			break
		}
		bLabels := strings.Split(bucketLabelsStr, ",")

		// Ignore timestamp
		_, err = ip.ReadUntil(',')
		if err != nil {
			break
		}

		// Read bucket values
		bucketValuesStr, err := ip.ReadUntil(';')
		if err != nil && err != io.EOF {
			break
		}
		bucketValues := strings.Split(bucketValuesStr, ",")

		// Set bucket labels and bucket values.
		// Convert percentage to exact ops count and compute 'less than or equal to' bucket values for Prometheus histograms.
		// Consider only non-zero buckets and the first zero bucket (since we are converting to 'less than or equal to' buckets)
		bucketValuesFloat := make([]float64, 1)
		bucketLabels := make([]string, 1)

		bucketLabels[0] = "+Inf"
		bucketValuesFloat[0], err = strconv.ParseFloat(bucketValues[0], 64)
		if err != nil {
			log.Error(err)
			break
		}

		for i := 1; i < len(bucketValues); i++ {
			val, err := strconv.ParseFloat(bucketValues[i], 64)
			if err != nil {
				log.Error(err)
				break
			}

			v := bucketValuesFloat[0] - ((val * bucketValuesFloat[0]) / 100)

			bucketLabels = append(bucketLabels, strings.Trim(bLabels[i], "><=ms"))
			bucketValuesFloat = append(bucketValuesFloat, v)

			if latencyBucketsCount > 0 && i >= latencyBucketsCount {
				// latency buckets count limit reached
				break
			}
		}

		// Sanity check
		if len(bucketLabels) != len(bucketValuesFloat) {
			log.Errorf("Error parsing latency values for node: `%s`. Bucket mismatch: buckets: `%v`, values: `%v`", fullHost, bucketLabels, bucketValuesFloat)
			break
		}

		stats := StatsMap{
			"bucketLabels": bucketLabels,
			"bucketValues": bucketValuesFloat,
			"timeUnit":     "ms",
		}

		if res[namespaceName] == nil {
			res[namespaceName] = StatsMap{
				operation: stats,
			}
		} else {
			res[namespaceName][operation] = stats
		}
	}

	return res
}

func readNamespaceAndOperation(ip *InfoParser) (string, string, error) {
	if err := ip.PeekAndExpect("batch-index"); err == nil {
		operation, err := ip.ReadUntil(':')
		return "", operation, err
	}

	if err := ip.Expect("{"); err != nil {
		if _, err := ip.ReadUntil(';'); err != nil {
			return "", "", err
		}
		return "", "", nil
	}

	// Get namespace name
	namespaceName, err := ip.ReadUntil('}')
	if err != nil {
		return "", "", err
	}

	if err := ip.Expect("-"); err != nil {
		return "", "", err
	}

	// Get operation (read, write etc.)
	operation, err := ip.ReadUntil(':')
	if err != nil {
		return "", "", err
	}
	return namespaceName, operation, err
}

// Parse "latencies:" info output
//
// Format (with and without latency data)
// {test}-write:msec,4234.9,28.75,7.40,1.63,0.26,0.03,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00;
// {test}-read:;
func parseLatencyInfo(s string, latencyBucketsCount int) map[string]StatsMap {
	ip := NewInfoParser(s)
	res := map[string]StatsMap{}

	for {
		namespaceName, operation, err := readNamespaceAndOperation(ip)

		if err != nil {
			break
		}

		if namespaceName == "" && operation == "" {
			continue
		}

		// Might be an empty output due to no latency data available, so continue to next section
		if err := ip.PeekAndExpect(";"); err == nil {
			if err := ip.Expect(";"); err != nil {
				break
			}
			continue
		}

		// Get time unit - msec or usec
		timeUnit, err := ip.ReadUntil(',')
		if err != nil {
			break
		}

		// Simplify time unit for use in metric name
		timeUnit = strings.TrimSuffix(timeUnit, "ec")

		// Read bucket values
		bucketValuesStr, err := ip.ReadUntil(';')
		if err != nil && err != io.EOF {
			break
		}
		bucketValues := strings.Split(bucketValuesStr, ",")

		// Set bucket labels and bucket values.
		// Convert percentage to exact ops count and compute 'less than or equal to' bucket values for Prometheus histograms.
		// Consider only non-zero buckets and the first zero bucket (since we are converting to 'less than or equal to' buckets)
		bucketValuesFloat := make([]float64, 1)
		bucketLabels := make([]string, 1)

		bucketLabels[0] = "+Inf"
		bucketValuesFloat[0], err = strconv.ParseFloat(bucketValues[0], 64)
		if err != nil {
			log.Error(err)
			break
		}

		for i := 1; i < len(bucketValues); i++ {
			val, err := strconv.ParseFloat(bucketValues[i], 64)
			if err != nil {
				log.Error(err)
				break
			}

			v := bucketValuesFloat[0] - ((val * bucketValuesFloat[0]) / 100)

			bucketLabels = append(bucketLabels, strconv.Itoa(1<<(i-1)))
			bucketValuesFloat = append(bucketValuesFloat, v)

			if latencyBucketsCount > 0 && i >= latencyBucketsCount {
				// latency buckets count limit reached
				break
			}
		}

		// Sanity check
		if len(bucketLabels) != len(bucketValuesFloat) {
			log.Errorf("Error parsing latency values for node: `%s`. Bucket mismatch: buckets: `%v`, values: `%v`", fullHost, bucketLabels, bucketValuesFloat)
			break
		}

		stats := StatsMap{
			"bucketLabels": bucketLabels,
			"bucketValues": bucketValuesFloat,
			"timeUnit":     timeUnit,
		}

		if res[namespaceName] == nil {
			res[namespaceName] = StatsMap{
				operation: stats,
			}
		} else {
			res[namespaceName][operation] = stats
		}
	}

	return res
}
                                aerospike-prometheus-exporter/._main.go                                                             000644  000765  000024  00000000243 14426143306 021533  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/main.go                                                     000644  000765  000024  00000000210 14426143306 023261  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.090303745
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/main.go                                                               000644  000765  000024  00000010773 14426143306 021327  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"crypto/tls"
	"flag"
	"fmt"
	"net"
	"net/http"
	"os"
	"strconv"
	"time"

	"github.com/prometheus/client_golang/prometheus"
	"github.com/prometheus/client_golang/prometheus/promhttp"

	aero "github.com/aerospike/aerospike-client-go/v6"
	log "github.com/sirupsen/logrus"
)

var (
	configFile  = flag.String("config", "/etc/aerospike-prometheus-exporter/ape.toml", "Config File")
	showUsage   = flag.Bool("u", false, "Show usage information")
	showVersion = flag.Bool("version", false, "Print version")

	fullHost string
	config   *Config

	version = "v1.9.0"
)

func main() {
	flag.Parse()
	if *showUsage {
		flag.Usage()
		os.Exit(0)
	}

	if *showVersion {
		fmt.Println(version)
		os.Exit(0)
	}

	log.Infof("Welcome to Aerospike Prometheus Exporter %s", version)

	config = new(Config)
	initConfig(*configFile, config)
	config.validateAndUpdate()

	fullHost = net.JoinHostPort(config.Aerospike.Host, strconv.Itoa(int(config.Aerospike.Port)))

	host := aero.NewHost(config.Aerospike.Host, int(config.Aerospike.Port))
	host.TLSName = config.Aerospike.NodeTLSName

	observer, err := newObserver(host, config.Aerospike.User, config.Aerospike.Password)
	if err != nil {
		log.Fatalln(err)
	}

	promReg := prometheus.NewRegistry()
	promReg.MustRegister(observer)

	mux := http.NewServeMux()

	// Get http basic auth username
	httpBasicAuthUsernameBytes, err := getSecret(config.AeroProm.BasicAuthUsername)
	if err != nil {
		log.Fatal(err)
	}
	httpBasicAuthUsername := string(httpBasicAuthUsernameBytes)

	// Get http basic auth password
	httpBasicAuthPasswordBytes, err := getSecret(config.AeroProm.BasicAuthPassword)
	if err != nil {
		log.Fatal(err)
	}
	httpBasicAuthPassword := string(httpBasicAuthPasswordBytes)

	// Handle "/metrics" url
	mux.HandleFunc("/metrics", func(w http.ResponseWriter, r *http.Request) {
		if httpBasicAuthUsername != "" {
			if validateBasicAuth(r, httpBasicAuthUsername, httpBasicAuthPassword) {
				promhttp.HandlerFor(promReg, promhttp.HandlerOpts{}).ServeHTTP(w, r)
				return
			}
			log.Warnf("Request from %s - Unauthorized", r.RemoteAddr)

			w.Header().Set("WWW-Authenticate", `Basic realm="AEROSPIKE-PROMETHEUS-EXPORTER-REALM"`)
			w.WriteHeader(401)
			_, err := w.Write([]byte("401 Unauthorized\n"))
			if err != nil {
				log.Warnf("failed to write http response data for /metrics: %s", err.Error())
			}
		} else {
			promhttp.HandlerFor(promReg, promhttp.HandlerOpts{}).ServeHTTP(w, r)
		}
	})

	// Handle "/health" url
	mux.HandleFunc("/health", func(w http.ResponseWriter, r *http.Request) {
		_, err := w.Write([]byte(`OK`))
		if err != nil {
			log.Warnf("failed to write http response for /health: %s", err.Error())
		}
	})

	// Handle "/" root url
	mux.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		_, err := w.Write([]byte(`<html>
			<head><title>Aerospike Prometheus Exporter</title></head>
			<body>
			<h1>Aerospike Prometheus Exporter</h1>
			<p>Go to <a href='` + "/metrics" + `'>Metrics</a></p>
			</body>
			</html>
		`))
		if err != nil {
			log.Warnf("failed to write http response for root /: %s", err.Error())
		}
	})

	srv := &http.Server{
		ReadTimeout:  time.Duration(config.AeroProm.Timeout) * time.Second,
		WriteTimeout: time.Duration(config.AeroProm.Timeout) * time.Second,
		Addr:         config.AeroProm.Bind,
		Handler:      mux,
		TLSNextProto: make(map[string]func(*http.Server, *tls.Conn, http.Handler)),
	}

	log.Infof("Listening for Prometheus on: %s", config.AeroProm.Bind)

	if len(config.AeroProm.CertFile) > 0 && len(config.AeroProm.KeyFile) > 0 {
		log.Info("Enabling HTTPS ...")
		srv.TLSConfig = initExporterTLS()
		log.Fatalln(srv.ListenAndServeTLS("", ""))
	}

	log.Fatalln(srv.ListenAndServe())
}

// initExporterTLS initializes and returns TLS config to be used to serve metrics over HTTPS
func initExporterTLS() *tls.Config {
	serverPool, err := loadServerCertAndKey(config.AeroProm.CertFile, config.AeroProm.KeyFile, config.AeroProm.KeyFilePassphrase)
	if err != nil {
		log.Fatal(err)
	}

	tlsConfig := &tls.Config{
		Certificates:             serverPool,
		MinVersion:               tls.VersionTLS12,
		CurvePreferences:         []tls.CurveID{tls.CurveP521, tls.CurveP384, tls.CurveP256},
		PreferServerCipherSuites: true,
		InsecureSkipVerify:       false,
	}

	// if root CA provided, client validation is enabled (mutual TLS)
	if len(config.AeroProm.RootCA) > 0 {
		caPool, err := loadCACert(config.AeroProm.RootCA)
		if err != nil {
			log.Fatal(err)
		}

		tlsConfig.ClientCAs = caPool
		tlsConfig.ClientAuth = tls.RequireAndVerifyClientCert
	}

	return tlsConfig
}
     aerospike-prometheus-exporter/._mock_data_generator_test.go                                         000644  000765  000024  00000000243 14426143306 025636  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/mock_data_generator_test.go                                 000644  000765  000024  00000000210 14426143306 027364  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.090578891
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/mock_data_generator_test.go                                           000644  000765  000024  00000105122 14426143306 025423  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"fmt"
	"strings"
)

/*
Dummy Raw Metrics, copied from local Aerospike Server
returns static test data copied from running an Aerospike Server with test namespaces, sets, sindex, jobs, latencies etc.,
we need to update this data for each release to reflect the new metrics, contexts etc.,
this data is passed to the watcher and expected output is also generated
once we have output from watcher-implementations ( like watcher_namespaces.go, watcher_node_stats.go)

	this output is compated with the expected results generated by Test-Cases
*/
func getRawMetrics() map[string]string {

	rawMetrics := make(map[string]string)

	// ORIGINAL TEST DATA == DONT DELETE
	rawMetrics["namespace/test"] = "ns_cluster_size=1;effective_replication_factor=1;objects=38914;tombstones=0;xdr_tombstones=0;xdr_bin_cemeteries=0;master_objects=38914;master_tombstones=0;prole_objects=0;prole_tombstones=0;non_replica_objects=0;non_replica_tombstones=0;unreplicated_records=0;dead_partitions=0;unavailable_partitions=0;clock_skew_stop_writes=false;stop_writes=false;hwm_breached=false;current_time=420112506;non_expirable_objects=0;expired_objects=0;evicted_objects=0;evict_ttl=0;evict_void_time=0;smd_evict_void_time=0;nsup_cycle_duration=0;nsup_cycle_deleted_pct=0.00;truncate_lut=0;truncating=false;sindex_gc_cleaned=0;memory_used_bytes=21830135;memory_used_data_bytes=2562423;memory_used_index_bytes=2490496;memory_used_set_index_bytes=0;memory_used_sindex_bytes=16777216;memory_free_pct=99;xmem_id=1;available_bin_names=65529;record_proto_uncompressed_pct=0.000;record_proto_compression_ratio=1.000;query_proto_uncompressed_pct=0.000;query_proto_compression_ratio=1.000;pending_quiesce=false;effective_is_quiesced=false;nodes_quiesced=0;effective_prefer_uniform_balance=true;migrate_tx_partitions_imbalance=0;migrate_tx_instances=0;migrate_rx_instances=0;migrate_tx_partitions_active=0;migrate_rx_partitions_active=0;migrate_tx_partitions_initial=0;migrate_tx_partitions_remaining=0;migrate_tx_partitions_lead_remaining=0;migrate_rx_partitions_initial=0;migrate_rx_partitions_remaining=0;migrate_records_skipped=0;migrate_records_transmitted=0;migrate_record_retransmits=0;migrate_record_receives=0;migrate_signals_active=0;migrate_signals_remaining=0;appeals_tx_active=0;appeals_rx_active=0;appeals_tx_remaining=0;appeals_records_exonerated=0;client_tsvc_error=0;client_tsvc_timeout=0;client_proxy_complete=0;client_proxy_error=0;client_proxy_timeout=0;client_read_success=126;client_read_error=0;client_read_timeout=0;client_read_not_found=27;client_read_filtered_out=0;client_write_success=64414;client_write_error=0;client_write_timeout=0;client_write_filtered_out=0;xdr_client_write_success=0;xdr_client_write_error=0;xdr_client_write_timeout=0;client_delete_success=20;client_delete_error=0;client_delete_timeout=0;client_delete_not_found=0;client_delete_filtered_out=0;xdr_client_delete_success=0;xdr_client_delete_error=0;xdr_client_delete_timeout=0;xdr_client_delete_not_found=0;client_udf_complete=0;client_udf_error=0;client_udf_timeout=0;client_udf_filtered_out=0;client_lang_read_success=0;client_lang_write_success=0;client_lang_delete_success=0;client_lang_error=0;from_proxy_tsvc_error=0;from_proxy_tsvc_timeout=0;from_proxy_read_success=0;from_proxy_read_error=0;from_proxy_read_timeout=0;from_proxy_read_not_found=0;from_proxy_read_filtered_out=0;from_proxy_write_success=0;from_proxy_write_error=0;from_proxy_write_timeout=0;from_proxy_write_filtered_out=0;xdr_from_proxy_write_success=0;xdr_from_proxy_write_error=0;xdr_from_proxy_write_timeout=0;from_proxy_delete_success=0;from_proxy_delete_error=0;from_proxy_delete_timeout=0;from_proxy_delete_not_found=0;from_proxy_delete_filtered_out=0;xdr_from_proxy_delete_success=0;xdr_from_proxy_delete_error=0;xdr_from_proxy_delete_timeout=0;xdr_from_proxy_delete_not_found=0;from_proxy_udf_complete=0;from_proxy_udf_error=0;from_proxy_udf_timeout=0;from_proxy_udf_filtered_out=0;from_proxy_lang_read_success=0;from_proxy_lang_write_success=0;from_proxy_lang_delete_success=0;from_proxy_lang_error=0;batch_sub_tsvc_error=0;batch_sub_tsvc_timeout=0;batch_sub_proxy_complete=0;batch_sub_proxy_error=0;batch_sub_proxy_timeout=0;batch_sub_read_success=0;batch_sub_read_error=0;batch_sub_read_timeout=0;batch_sub_read_not_found=0;batch_sub_read_filtered_out=0;batch_sub_write_success=0;batch_sub_write_error=0;batch_sub_write_timeout=0;batch_sub_write_filtered_out=0;batch_sub_delete_success=0;batch_sub_delete_error=0;batch_sub_delete_timeout=0;batch_sub_delete_not_found=0;batch_sub_delete_filtered_out=0;batch_sub_udf_complete=0;batch_sub_udf_error=0;batch_sub_udf_timeout=0;batch_sub_udf_filtered_out=0;batch_sub_lang_read_success=0;batch_sub_lang_write_success=0;batch_sub_lang_delete_success=0;batch_sub_lang_error=0;from_proxy_batch_sub_tsvc_error=0;from_proxy_batch_sub_tsvc_timeout=0;from_proxy_batch_sub_read_success=0;from_proxy_batch_sub_read_error=0;from_proxy_batch_sub_read_timeout=0;from_proxy_batch_sub_read_not_found=0;from_proxy_batch_sub_read_filtered_out=0;from_proxy_batch_sub_write_success=0;from_proxy_batch_sub_write_error=0;from_proxy_batch_sub_write_timeout=0;from_proxy_batch_sub_write_filtered_out=0;from_proxy_batch_sub_delete_success=0;from_proxy_batch_sub_delete_error=0;from_proxy_batch_sub_delete_timeout=0;from_proxy_batch_sub_delete_not_found=0;from_proxy_batch_sub_delete_filtered_out=0;from_proxy_batch_sub_udf_complete=0;from_proxy_batch_sub_udf_error=0;from_proxy_batch_sub_udf_timeout=0;from_proxy_batch_sub_udf_filtered_out=0;from_proxy_batch_sub_lang_read_success=0;from_proxy_batch_sub_lang_write_success=0;from_proxy_batch_sub_lang_delete_success=0;from_proxy_batch_sub_lang_error=0;udf_sub_tsvc_error=0;udf_sub_tsvc_timeout=0;udf_sub_udf_complete=0;udf_sub_udf_error=0;udf_sub_udf_timeout=0;udf_sub_udf_filtered_out=0;udf_sub_lang_read_success=0;udf_sub_lang_write_success=0;udf_sub_lang_delete_success=0;udf_sub_lang_error=0;ops_sub_tsvc_error=0;ops_sub_tsvc_timeout=0;ops_sub_write_success=0;ops_sub_write_error=0;ops_sub_write_timeout=0;ops_sub_write_filtered_out=0;dup_res_ask=0;dup_res_respond_read=0;dup_res_respond_no_read=0;retransmit_all_read_dup_res=0;retransmit_all_write_dup_res=0;retransmit_all_write_repl_write=0;retransmit_all_delete_dup_res=0;retransmit_all_delete_repl_write=0;retransmit_all_udf_dup_res=0;retransmit_all_udf_repl_write=0;retransmit_all_batch_sub_dup_res=0;retransmit_udf_sub_dup_res=0;retransmit_udf_sub_repl_write=0;retransmit_ops_sub_dup_res=0;retransmit_ops_sub_repl_write=0;pi_query_short_basic_complete=0;pi_query_short_basic_error=0;pi_query_short_basic_timeout=0;pi_query_long_basic_complete=1;pi_query_long_basic_error=14;pi_query_long_basic_abort=0;pi_query_aggr_complete=0;pi_query_aggr_error=0;pi_query_aggr_abort=0;pi_query_udf_bg_complete=0;pi_query_udf_bg_error=0;pi_query_udf_bg_abort=0;pi_query_ops_bg_complete=0;pi_query_ops_bg_error=0;pi_query_ops_bg_abort=0;si_query_short_basic_complete=0;si_query_short_basic_error=0;si_query_short_basic_timeout=0;si_query_long_basic_complete=0;si_query_long_basic_error=0;si_query_long_basic_abort=0;si_query_aggr_complete=0;si_query_aggr_error=0;si_query_aggr_abort=0;si_query_udf_bg_complete=0;si_query_udf_bg_error=0;si_query_udf_bg_abort=0;si_query_ops_bg_complete=0;si_query_ops_bg_error=0;si_query_ops_bg_abort=0;geo_region_query_reqs=0;geo_region_query_cells=0;geo_region_query_points=0;geo_region_query_falsepos=0;re_repl_tsvc_error=0;re_repl_tsvc_timeout=0;re_repl_success=0;re_repl_error=0;re_repl_timeout=0;fail_xdr_forbidden=0;fail_key_busy=0;fail_generation=0;fail_record_too_big=0;fail_client_lost_conflict=0;fail_xdr_lost_conflict=0;deleted_last_bin=0;allow-ttl-without-nsup=false;background-query-max-rps=10000;conflict-resolution-policy=generation;conflict-resolve-writes=false;data-in-index=false;default-ttl=0;disable-cold-start-eviction=false;disable-write-dup-res=false;disallow-expunge=false;disallow-null-setname=false;enable-benchmarks-batch-sub=false;enable-benchmarks-ops-sub=false;enable-benchmarks-read=false;enable-benchmarks-udf=false;enable-benchmarks-udf-sub=false;enable-benchmarks-write=false;enable-hist-proxy=false;evict-hist-buckets=10000;evict-tenths-pct=5;force-long-queries=false;high-water-disk-pct=0;high-water-memory-pct=0;ignore-migrate-fill-delay=false;index-stage-size=1073741824;inline-short-queries=false;max-record-size=0;memory-size=4294967296;migrate-order=5;migrate-retransmit-ms=5000;migrate-sleep=1;nsup-hist-period=3600;nsup-period=0;nsup-threads=1;partition-tree-sprigs=256;prefer-uniform-balance=true;rack-id=0;read-consistency-level-override=off;reject-non-xdr-writes=false;reject-xdr-writes=false;replication-factor=2;sindex-stage-size=1073741824;single-bin=false;single-query-threads=4;stop-writes-pct=90;stop-writes-sys-memory-pct=90;strong-consistency=false;strong-consistency-allow-expunge=false;tomb-raider-eligible-age=86400;tomb-raider-period=86400;transaction-pending-limit=20;truncate-threads=4;write-commit-level-override=off;xdr-bin-tombstone-ttl=86400;xdr-tomb-raider-period=120;xdr-tomb-raider-threads=1;geo2dsphere-within.strict=true;geo2dsphere-within.min-level=1;geo2dsphere-within.max-level=20;geo2dsphere-within.max-cells=12;geo2dsphere-within.level-mod=1;geo2dsphere-within.earth-radius-meters=6371000;index-type=shmem;sindex-type=shmem;storage-engine=memory"
	rawMetrics["namespace/bar"] = "ns_cluster_size=1;effective_replication_factor=1;objects=13403218;tombstones=0;xdr_tombstones=0;xdr_bin_cemeteries=0;master_objects=13403218;master_tombstones=0;prole_objects=0;prole_tombstones=0;non_replica_objects=0;non_replica_tombstones=0;unreplicated_records=0;dead_partitions=0;unavailable_partitions=0;clock_skew_stop_writes=false;stop_writes=false;hwm_breached=false;current_time=420112506;non_expirable_objects=0;expired_objects=0;evicted_objects=0;evict_ttl=0;evict_void_time=0;smd_evict_void_time=0;nsup_cycle_duration=0;nsup_cycle_deleted_pct=0.00;truncate_lut=0;truncating=false;sindex_gc_cleaned=0;memory_used_bytes=1751784700;memory_used_data_bytes=893978748;memory_used_index_bytes=857805952;memory_used_set_index_bytes=0;memory_used_sindex_bytes=0;memory_free_pct=59;xmem_id=2;available_bin_names=65532;device_total_bytes=17179869184;device_used_bytes=1621031664;device_free_pct=90;device_available_pct=86;storage-engine.file[0].used_bytes=1621031664;storage-engine.file[0].free_wblocks=14198;storage-engine.file[0].write_q=0;storage-engine.file[0].writes=0;storage-engine.file[0].defrag_q=0;storage-engine.file[0].defrag_reads=2;storage-engine.file[0].defrag_writes=0;storage-engine.file[0].shadow_write_q=0;storage-engine.file[0].age=-1;record_proto_uncompressed_pct=0.000;record_proto_compression_ratio=1.000;query_proto_uncompressed_pct=0.000;query_proto_compression_ratio=1.000;pending_quiesce=false;effective_is_quiesced=false;nodes_quiesced=0;effective_prefer_uniform_balance=true;migrate_tx_partitions_imbalance=0;migrate_tx_instances=0;migrate_rx_instances=0;migrate_tx_partitions_active=0;migrate_rx_partitions_active=0;migrate_tx_partitions_initial=0;migrate_tx_partitions_remaining=0;migrate_tx_partitions_lead_remaining=0;migrate_rx_partitions_initial=0;migrate_rx_partitions_remaining=0;migrate_records_skipped=0;migrate_records_transmitted=0;migrate_record_retransmits=0;migrate_record_receives=0;migrate_signals_active=0;migrate_signals_remaining=0;appeals_tx_active=0;appeals_rx_active=0;appeals_tx_remaining=0;appeals_records_exonerated=0;client_tsvc_error=0;client_tsvc_timeout=0;client_proxy_complete=0;client_proxy_error=0;client_proxy_timeout=0;client_read_success=0;client_read_error=0;client_read_timeout=0;client_read_not_found=0;client_read_filtered_out=0;client_write_success=13;client_write_error=0;client_write_timeout=0;client_write_filtered_out=0;xdr_client_write_success=0;xdr_client_write_error=0;xdr_client_write_timeout=0;client_delete_success=0;client_delete_error=0;client_delete_timeout=0;client_delete_not_found=0;client_delete_filtered_out=0;xdr_client_delete_success=0;xdr_client_delete_error=0;xdr_client_delete_timeout=0;xdr_client_delete_not_found=0;client_udf_complete=0;client_udf_error=0;client_udf_timeout=0;client_udf_filtered_out=0;client_lang_read_success=0;client_lang_write_success=0;client_lang_delete_success=0;client_lang_error=0;from_proxy_tsvc_error=0;from_proxy_tsvc_timeout=0;from_proxy_read_success=0;from_proxy_read_error=0;from_proxy_read_timeout=0;from_proxy_read_not_found=0;from_proxy_read_filtered_out=0;from_proxy_write_success=0;from_proxy_write_error=0;from_proxy_write_timeout=0;from_proxy_write_filtered_out=0;xdr_from_proxy_write_success=0;xdr_from_proxy_write_error=0;xdr_from_proxy_write_timeout=0;from_proxy_delete_success=0;from_proxy_delete_error=0;from_proxy_delete_timeout=0;from_proxy_delete_not_found=0;from_proxy_delete_filtered_out=0;xdr_from_proxy_delete_success=0;xdr_from_proxy_delete_error=0;xdr_from_proxy_delete_timeout=0;xdr_from_proxy_delete_not_found=0;from_proxy_udf_complete=0;from_proxy_udf_error=0;from_proxy_udf_timeout=0;from_proxy_udf_filtered_out=0;from_proxy_lang_read_success=0;from_proxy_lang_write_success=0;from_proxy_lang_delete_success=0;from_proxy_lang_error=0;batch_sub_tsvc_error=0;batch_sub_tsvc_timeout=0;batch_sub_proxy_complete=0;batch_sub_proxy_error=0;batch_sub_proxy_timeout=0;batch_sub_read_success=0;batch_sub_read_error=0;batch_sub_read_timeout=0;batch_sub_read_not_found=0;batch_sub_read_filtered_out=0;batch_sub_write_success=0;batch_sub_write_error=0;batch_sub_write_timeout=0;batch_sub_write_filtered_out=0;batch_sub_delete_success=0;batch_sub_delete_error=0;batch_sub_delete_timeout=0;batch_sub_delete_not_found=0;batch_sub_delete_filtered_out=0;batch_sub_udf_complete=0;batch_sub_udf_error=0;batch_sub_udf_timeout=0;batch_sub_udf_filtered_out=0;batch_sub_lang_read_success=0;batch_sub_lang_write_success=0;batch_sub_lang_delete_success=0;batch_sub_lang_error=0;from_proxy_batch_sub_tsvc_error=0;from_proxy_batch_sub_tsvc_timeout=0;from_proxy_batch_sub_read_success=0;from_proxy_batch_sub_read_error=0;from_proxy_batch_sub_read_timeout=0;from_proxy_batch_sub_read_not_found=0;from_proxy_batch_sub_read_filtered_out=0;from_proxy_batch_sub_write_success=0;from_proxy_batch_sub_write_error=0;from_proxy_batch_sub_write_timeout=0;from_proxy_batch_sub_write_filtered_out=0;from_proxy_batch_sub_delete_success=0;from_proxy_batch_sub_delete_error=0;from_proxy_batch_sub_delete_timeout=0;from_proxy_batch_sub_delete_not_found=0;from_proxy_batch_sub_delete_filtered_out=0;from_proxy_batch_sub_udf_complete=0;from_proxy_batch_sub_udf_error=0;from_proxy_batch_sub_udf_timeout=0;from_proxy_batch_sub_udf_filtered_out=0;from_proxy_batch_sub_lang_read_success=0;from_proxy_batch_sub_lang_write_success=0;from_proxy_batch_sub_lang_delete_success=0;from_proxy_batch_sub_lang_error=0;udf_sub_tsvc_error=0;udf_sub_tsvc_timeout=0;udf_sub_udf_complete=0;udf_sub_udf_error=0;udf_sub_udf_timeout=0;udf_sub_udf_filtered_out=0;udf_sub_lang_read_success=0;udf_sub_lang_write_success=0;udf_sub_lang_delete_success=0;udf_sub_lang_error=0;ops_sub_tsvc_error=0;ops_sub_tsvc_timeout=0;ops_sub_write_success=0;ops_sub_write_error=0;ops_sub_write_timeout=0;ops_sub_write_filtered_out=0;dup_res_ask=0;dup_res_respond_read=0;dup_res_respond_no_read=0;retransmit_all_read_dup_res=0;retransmit_all_write_dup_res=0;retransmit_all_write_repl_write=0;retransmit_all_delete_dup_res=0;retransmit_all_delete_repl_write=0;retransmit_all_udf_dup_res=0;retransmit_all_udf_repl_write=0;retransmit_all_batch_sub_dup_res=0;retransmit_udf_sub_dup_res=0;retransmit_udf_sub_repl_write=0;retransmit_ops_sub_dup_res=0;retransmit_ops_sub_repl_write=0;pi_query_short_basic_complete=0;pi_query_short_basic_error=0;pi_query_short_basic_timeout=0;pi_query_long_basic_complete=0;pi_query_long_basic_error=0;pi_query_long_basic_abort=0;pi_query_aggr_complete=0;pi_query_aggr_error=0;pi_query_aggr_abort=0;pi_query_udf_bg_complete=0;pi_query_udf_bg_error=0;pi_query_udf_bg_abort=0;pi_query_ops_bg_complete=0;pi_query_ops_bg_error=0;pi_query_ops_bg_abort=0;si_query_short_basic_complete=0;si_query_short_basic_error=0;si_query_short_basic_timeout=0;si_query_long_basic_complete=0;si_query_long_basic_error=0;si_query_long_basic_abort=0;si_query_aggr_complete=0;si_query_aggr_error=0;si_query_aggr_abort=0;si_query_udf_bg_complete=0;si_query_udf_bg_error=0;si_query_udf_bg_abort=0;si_query_ops_bg_complete=0;si_query_ops_bg_error=0;si_query_ops_bg_abort=0;geo_region_query_reqs=0;geo_region_query_cells=0;geo_region_query_points=0;geo_region_query_falsepos=0;re_repl_tsvc_error=0;re_repl_tsvc_timeout=0;re_repl_success=0;re_repl_error=0;re_repl_timeout=0;fail_xdr_forbidden=0;fail_key_busy=0;fail_generation=0;fail_record_too_big=0;fail_client_lost_conflict=0;fail_xdr_lost_conflict=0;deleted_last_bin=0;allow-ttl-without-nsup=false;background-query-max-rps=10000;conflict-resolution-policy=generation;conflict-resolve-writes=false;data-in-index=false;default-ttl=0;disable-cold-start-eviction=false;disable-write-dup-res=false;disallow-expunge=false;disallow-null-setname=false;enable-benchmarks-batch-sub=false;enable-benchmarks-ops-sub=false;enable-benchmarks-read=false;enable-benchmarks-udf=false;enable-benchmarks-udf-sub=false;enable-benchmarks-write=false;enable-hist-proxy=false;evict-hist-buckets=10000;evict-tenths-pct=5;force-long-queries=false;high-water-disk-pct=0;high-water-memory-pct=0;ignore-migrate-fill-delay=false;index-stage-size=1073741824;inline-short-queries=false;max-record-size=0;memory-size=4294967296;migrate-order=5;migrate-retransmit-ms=5000;migrate-sleep=1;nsup-hist-period=3600;nsup-period=0;nsup-threads=1;partition-tree-sprigs=256;prefer-uniform-balance=true;rack-id=0;read-consistency-level-override=off;reject-non-xdr-writes=false;reject-xdr-writes=false;replication-factor=2;sindex-stage-size=1073741824;single-bin=false;single-query-threads=4;stop-writes-pct=90;stop-writes-sys-memory-pct=90;strong-consistency=false;strong-consistency-allow-expunge=false;tomb-raider-eligible-age=86400;tomb-raider-period=86400;transaction-pending-limit=20;truncate-threads=4;write-commit-level-override=off;xdr-bin-tombstone-ttl=86400;xdr-tomb-raider-period=120;xdr-tomb-raider-threads=1;geo2dsphere-within.strict=true;geo2dsphere-within.min-level=1;geo2dsphere-within.max-level=20;geo2dsphere-within.max-cells=12;geo2dsphere-within.level-mod=1;geo2dsphere-within.earth-radius-meters=6371000;index-type=shmem;sindex-type=shmem;storage-engine=device;storage-engine.file[0]=/opt/aerospike/data/bar.dat;storage-engine.cache-replica-writes=false;storage-engine.cold-start-empty=false;storage-engine.commit-to-device=false;storage-engine.commit-min-size=0;storage-engine.compression=none;storage-engine.compression-acceleration=0;storage-engine.compression-level=0;storage-engine.data-in-memory=true;storage-engine.defrag-lwm-pct=50;storage-engine.defrag-queue-min=0;storage-engine.defrag-sleep=1000;storage-engine.defrag-startup-minimum=0;storage-engine.direct-files=false;storage-engine.disable-odsync=false;storage-engine.enable-benchmarks-storage=false;storage-engine.encryption-key-file=null;storage-engine.encryption-old-key-file=null;storage-engine.filesize=17179869184;storage-engine.flush-max-ms=1000;storage-engine.max-used-pct=70;storage-engine.max-write-cache=67108864;storage-engine.min-avail-pct=5;storage-engine.post-write-queue=0;storage-engine.read-page-cache=false;storage-engine.scheduler-mode=null;storage-engine.serialize-tomb-raider=false;storage-engine.sindex-startup-device-scan=false;storage-engine.tomb-raider-sleep=1000;storage-engine.write-block-size=1048576"
	rawMetrics["sets"] = "ns=test:set=test_set2:objects=12973:tombstones=0:memory_data_bytes=845591:device_data_bytes=0:truncate_lut=0:sindexes=1:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=test:set=test_east_region:objects=12971:tombstones=0:memory_data_bytes=858449:device_data_bytes=0:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=test:set=test_vendors:objects=12970:tombstones=0:memory_data_bytes=858383:device_data_bytes=0:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=test:set=aerospike:objects=0:tombstones=0:memory_data_bytes=0:device_data_bytes=0:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=test:set=ownset:objects=0:tombstones=0:memory_data_bytes=0:device_data_bytes=0:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=bar:set=set2:objects=3684785:tombstones=0:memory_data_bytes=247974882:device_data_bytes=412695920:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=bar:set=vendors:objects=3495040:tombstones=0:memory_data_bytes=234530114:device_data_bytes=411741440:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=bar:set=south_region:objects=998985:tombstones=0:memory_data_bytes=65825013:device_data_bytes=127870080:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=bar:set=north_region:objects=998987:tombstones=0:memory_data_bytes=65825146:device_data_bytes=127870336:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=bar:set=east_region:objects=3226447:tombstones=0:memory_data_bytes=213999303:device_data_bytes=412985216:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0;ns=bar:set=west_region:objects=998974:tombstones=0:memory_data_bytes=65824290:device_data_bytes=127868672:truncate_lut=0:sindexes=0:index_populating=false:truncating=false:disable-eviction=false:enable-index=false:stop-writes-count=0:stop-writes-size=0"
	rawMetrics["latencies"] = "batch-index:;{test}-read:msec,0.0,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00;{test}-write:msec,0.0,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00;{test}-udf:;{test}-pi-query:;{test}-si-query:;{bar}-read:;{bar}-write:msec,0.0,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00,0.00;{bar}-udf:;{bar}-pi-query:;{bar}-si-query:"
	rawMetrics["sindex/test/test_sindex1"] = "entries=12972;used_bytes=16777216;entries_per_bval=12972;entries_per_rec=1;load_pct=100;load_time=0;stat_gc_recs=0"
	rawMetrics["query-show"] = "trid=12860712447849720134:ns=test:set=test_set2:n-pids-requested=4096:n-keyds-requested=0:rps=0:active-threads=0:status=done(ok):job-progress=100.00:run-time=91:time-since-done=76964462:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=12971:recs-failed=0:from=172.17.0.6+40714:job-type=basic:net-io-bytes=2116680:net-io-time=45:socket-timeout=30000;trid=10212667924988677130:ns=test:set=test_vendors:n-pids-requested=4090:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96971708:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2192:recs-failed=0:from=172.17.0.2+53556:job-type=basic:net-io-bytes=232535:net-io-time=0:socket-timeout=30000;trid=9038054471030658800:ns=test:set=test_vendors:n-pids-requested=4091:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96971747:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2193:recs-failed=0:from=172.17.0.2+53548:job-type=basic:net-io-bytes=228561:net-io-time=0:socket-timeout=30000;trid=18297828132092499463:ns=test:set=test_vendors:n-pids-requested=4092:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96971786:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2193:recs-failed=0:from=172.17.0.2+53532:job-type=basic:net-io-bytes=226885:net-io-time=0:socket-timeout=30000;trid=16496035235509212077:ns=test:set=test_vendors:n-pids-requested=4093:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96971825:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2194:recs-failed=0:from=172.17.0.2+53518:job-type=basic:net-io-bytes=228308:net-io-time=0:socket-timeout=30000;trid=5499606219233706254:ns=test:set=test_vendors:n-pids-requested=4094:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96971864:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2194:recs-failed=0:from=172.17.0.2+53510:job-type=basic:net-io-bytes=231002:net-io-time=0:socket-timeout=30000;trid=4355246641643620061:ns=test:set=test_vendors:n-pids-requested=4095:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96971904:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2196:recs-failed=0:from=172.17.0.2+53502:job-type=basic:net-io-bytes=229269:net-io-time=0:socket-timeout=30000;trid=10994964236021603577:ns=test:set=test_vendors:n-pids-requested=4096:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96971943:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2197:recs-failed=0:from=172.17.0.2+53500:job-type=basic:net-io-bytes=231177:net-io-time=0:socket-timeout=30000;trid=13990051320060701253:ns=test:set=test_vendors:n-pids-requested=4090:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96983686:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2192:recs-failed=0:from=172.17.0.2+35732:job-type=basic:net-io-bytes=218025:net-io-time=0:socket-timeout=30000;trid=13506735252273329484:ns=test:set=test_vendors:n-pids-requested=4091:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=37:time-since-done=96983725:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2192:recs-failed=0:from=172.17.0.2+35720:job-type=basic:net-io-bytes=226786:net-io-time=0:socket-timeout=30000;trid=7603703035483518258:ns=test:set=test_vendors:n-pids-requested=4092:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96983766:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2192:recs-failed=0:from=172.17.0.2+35710:job-type=basic:net-io-bytes=228998:net-io-time=0:socket-timeout=30000;trid=13591277360630725735:ns=test:set=test_vendors:n-pids-requested=4093:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96983805:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2193:recs-failed=0:from=172.17.0.2+35702:job-type=basic:net-io-bytes=227783:net-io-time=0:socket-timeout=30000;trid=8120506070021718461:ns=test:set=test_vendors:n-pids-requested=4094:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96983845:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2194:recs-failed=0:from=172.17.0.2+35690:job-type=basic:net-io-bytes=340535:net-io-time=0:socket-timeout=30000;trid=1896955730142066978:ns=test:set=test_vendors:n-pids-requested=4095:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=36:time-since-done=96983884:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2196:recs-failed=0:from=172.17.0.2+35676:job-type=basic:net-io-bytes=341889:net-io-time=0:socket-timeout=30000;trid=2711297642618297495:ns=test:set=test_vendors:n-pids-requested=4096:n-keyds-requested=0:rps=0:active-threads=0:status=done(abandoned-response-error):job-progress=100.00:run-time=43:time-since-done=96983922:recs-throttled=0:recs-filtered-meta=0:recs-filtered-bins=0:recs-succeeded=2197:recs-failed=0:from=172.17.0.2+35674:job-type=basic:net-io-bytes=226042:net-io-time=0:socket-timeout=30000"
	rawMetrics["statistics"] = "failed_best_practices=true;cluster_size=1;cluster_key=4B8274A4C334;cluster_generation=1;cluster_principal=BB9030011AC4202;cluster_min_compatibility_id=11;cluster_max_compatibility_id=11;cluster_integrity=true;cluster_is_member=true;cluster_duplicate_nodes=null;cluster_clock_skew_stop_writes_sec=0;cluster_clock_skew_ms=0;cluster_clock_skew_outliers=null;uptime=97961;system_total_cpu_pct=6;system_user_cpu_pct=4;system_kernel_cpu_pct=2;system_free_mem_kbytes=9100968;system_free_mem_pct=74;system_thp_mem_kbytes=59392;process_cpu_pct=4;threads_joinable=9;threads_detached=70;threads_pool_total=31;threads_pool_active=27;heap_allocated_kbytes=1313306;heap_active_kbytes=1314744;heap_mapped_kbytes=1390080;heap_efficiency_pct=100;heap_site_count=0;objects=13442132;tombstones=0;info_queue=0;rw_in_progress=0;proxy_in_progress=0;tree_gc_queue=0;client_connections=2;client_connections_opened=5190;client_connections_closed=5188;heartbeat_connections=0;heartbeat_connections_opened=0;heartbeat_connections_closed=0;fabric_connections=0;fabric_connections_opened=0;fabric_connections_closed=0;heartbeat_received_self=0;heartbeat_received_foreign=0;reaped_fds=0;info_complete=108816;info_timeout=0;demarshal_error=0;early_tsvc_client_error=0;early_tsvc_from_proxy_error=0;early_tsvc_batch_sub_error=0;early_tsvc_from_proxy_batch_sub_error=0;early_tsvc_udf_sub_error=0;early_tsvc_ops_sub_error=0;long_queries_active=0;batch_index_initiate=0;batch_index_queue=0:0,0:0,0:0,0:0,0:0;batch_index_complete=0;batch_index_error=0;batch_index_timeout=0;batch_index_delay=0;batch_index_unused_buffers=0;batch_index_huge_buffers=0;batch_index_created_buffers=0;batch_index_destroyed_buffers=0;batch_index_proto_uncompressed_pct=0.000;batch_index_proto_compression_ratio=1.000;paxos_principal=BB9030011AC4202;time_since_rebalance=97888;migrate_allowed=true;migrate_partitions_remaining=0;fabric_bulk_send_rate=0;fabric_bulk_recv_rate=0;fabric_ctrl_send_rate=0;fabric_ctrl_recv_rate=0;fabric_meta_send_rate=0;fabric_meta_recv_rate=0;fabric_rw_send_rate=0;fabric_rw_recv_rate=0"
	rawMetrics["build"] = "6.2.0.0-94-g2ccdbdd"
	rawMetrics["service-clear-std"] = "172.17.0.3:3000"
	rawMetrics["cluster-name"] = "null"

	return rawMetrics
}

func requestInfoNamespaces(rawMetrics map[string]string) map[string]string {
	pass2Metrics := make(map[string]string)
	// pass2Metrics["namespaces"] = "test;bar"

	lNamespaces := ""
	for metricsGrpKey := range rawMetrics {
		if strings.HasPrefix(metricsGrpKey, "namespace/") {
			// our raw-metrics is of construct "namespace/<namespace-name>", so split and take <namespace-name>
			ns := strings.Split(metricsGrpKey, "/")[1]
			lNamespaces = ns + ";" + lNamespaces
		}
	}
	pass2Metrics["namespaces"] = strings.TrimSuffix(lNamespaces, ";")

	return pass2Metrics
}

func createPassTwoExpectedOutputs(rawMetrics map[string]string) []string {
	lNamespaces := []string{}
	for metricsGrpKey := range rawMetrics {
		if strings.HasPrefix(metricsGrpKey, "namespace/") {
			// our raw-metrics is of construct "namespace/<namespace-name>", so split and take <namespace-name>
			lNamespaces = append(lNamespaces, metricsGrpKey)
		}
	}
	return lNamespaces
}

/*
generated the output used by the Namespace-Watcher TestCases, the same output may not be suitable for other watchers,
so for each data-context we need to have a method to generate expected output
*/
func createNamespaceWatcherExpectedOutputs(nsName string, addNsToKey bool) (map[string][]string, map[string][]string) {
	lExpectedMetricNamedValues := map[string][]string{}
	lExpectedMetricLabels := map[string][]string{}

	rawMetrics := getRawMetrics()

	clusterName := rawMetrics["cluster-name"]
	service := rawMetrics["service-clear-std"]

	for metricsGrpKey := range rawMetrics {
		if strings.HasPrefix(metricsGrpKey, "namespace/") && strings.HasSuffix(metricsGrpKey, nsName) {
			ns := strings.Split(metricsGrpKey, "/")[1]
			grpValues := rawMetrics[metricsGrpKey]
			stats := splitAndRetrieveStats(grpValues, ";")

			// process stats and create {metricname,label} and {metric,values} map of strings
			for s, v := range stats {
				key := s
				convertedValue, err := convertValue(v)
				if err != nil {
					fmt.Println("IGNORING, failed converting value ( key: ", key, " - value: ", v, ") = error: ", err)
					continue
				}
				// reconvert float back to string
				value := fmt.Sprintf("%.0f", convertedValue)

				match := seDynamicExtractor.FindStringSubmatch(key)
				// if strings.Contains(key, "[") {
				if len(match) != 4 {
					key = strings.ReplaceAll(key, "-", "_")
					key = strings.ReplaceAll(key, ".", "_")

					metric := "aerospike_namespace_" + key
					valuesArr := lExpectedMetricNamedValues[metric]
					labelsArr := lExpectedMetricLabels[metric]
					if valuesArr == nil {
						valuesArr = []string{}
					}
					if labelsArr == nil {
						labelsArr = []string{}
					}

					labelStr := "[name:\"cluster_name\" value:\"" + clusterName + "\"  name:\"ns\" value:\"" + ns + "\"  name:\"service\" value:\"" + service + "\" ]"

					valuesArr = append(valuesArr, value)
					labelsArr = append(labelsArr, labelStr)

					mapKeyname := makeKeyname(nsName, metric, addNsToKey)
					lExpectedMetricNamedValues[mapKeyname] = valuesArr
					lExpectedMetricLabels[mapKeyname] = labelsArr

				} else {
					metricType := match[1]
					metricIndex := match[2]
					metricName := match[3]
					deviceOrFileName := stats["storage-engine."+metricType+"["+metricIndex+"]"]

					// fmt.Println("metricType: ", metricType, " === metricIndex: ", metricIndex, " ==== metricName: ", metricName, " ===== deviceOrFileName: ", deviceOrFileName)
					metric := "aerospike_namespace_storage_engine_" + metricType + "_" + metricName

					valuesArr := lExpectedMetricNamedValues[metric]
					labelsArr := lExpectedMetricLabels[metric]
					if valuesArr == nil {
						valuesArr = []string{}
					}
					if labelsArr == nil {
						labelsArr = []string{}
					}

					labelStr := "[name:\"cluster_name\" value:\"" + clusterName + "\"  name:\"file\" value:\"" + deviceOrFileName + "\"  name:\"file_index\" value:\"" + metricIndex + "\"  name:\"ns\" value:\"" + ns + "\"  name:\"service\" value:\"" + service + "\" ]"

					valuesArr = append(valuesArr, value)
					labelsArr = append(labelsArr, labelStr)

					mapKeyname := makeKeyname(nsName, metric, addNsToKey)

					lExpectedMetricNamedValues[mapKeyname] = valuesArr
					lExpectedMetricLabels[mapKeyname] = labelsArr
				}
			}
		}
	}

	return lExpectedMetricNamedValues, lExpectedMetricLabels
}
                                                                                                                                                                                                                                                                                                                                                                                                                                              aerospike-prometheus-exporter/._observer.go                                                         000644  000765  000024  00000000243 14426143306 022436  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/observer.go                                                 000644  000765  000024  00000000207 14426143306 024172  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         29 mtime=1683539654.09087741
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                         aerospike-prometheus-exporter/observer.go                                                           000644  000765  000024  00000015313 14426143306 022225  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"crypto/tls"
	"crypto/x509"
	"errors"
	"strings"
	"sync"
	"time"

	"github.com/prometheus/client_golang/prometheus"

	aero "github.com/aerospike/aerospike-client-go/v6"
	log "github.com/sirupsen/logrus"
)

// Observer communicates with Aerospike and helps collecting metrices
type Observer struct {
	conn          *aero.Connection
	newConnection func() (*aero.Connection, error)
	ticks         prometheus.Counter
	watchers      []Watcher
	mutex         sync.Mutex
}

var (
	// aerospike_node_up metric descriptor
	nodeActiveDesc *prometheus.Desc

	// Node service endpoint, cluster name and build version
	gService, gClusterName, gBuild string

	// Number of retries on info request
	retryCount = 3

	// Default info commands
	ikClusterName = "cluster-name"
	ikService     = "service-clear-std"
	ikBuild       = "build"
)

func initAerospikeTLS() *tls.Config {
	if len(config.Aerospike.RootCA) == 0 && len(config.Aerospike.CertFile) == 0 && len(config.Aerospike.KeyFile) == 0 {
		return nil
	}

	var clientPool []tls.Certificate
	var serverPool *x509.CertPool
	var err error

	serverPool, err = loadCACert(config.Aerospike.RootCA)
	if err != nil {
		log.Fatal(err)
	}

	if len(config.Aerospike.CertFile) > 0 || len(config.Aerospike.KeyFile) > 0 {
		clientPool, err = loadServerCertAndKey(config.Aerospike.CertFile, config.Aerospike.KeyFile, config.Aerospike.KeyFilePassphrase)
		if err != nil {
			log.Fatal(err)
		}
	}

	tlsConfig := &tls.Config{
		Certificates:             clientPool,
		RootCAs:                  serverPool,
		InsecureSkipVerify:       false,
		PreferServerCipherSuites: true,
		NameToCertificate:        nil,
	}

	return tlsConfig
}

func newObserver(server *aero.Host, user, pass string) (o *Observer, err error) {
	// initialize aerospike_node_up metric descriptor
	nodeActiveDesc = prometheus.NewDesc(
		"aerospike_node_up",
		"Aerospike node active status",
		[]string{"cluster_name", "service", "build"},
		config.AeroProm.MetricLabels,
	)

	// use all cpus in the system for concurrency
	authMode := strings.ToLower(strings.TrimSpace(config.Aerospike.AuthMode))
	if authMode != "internal" && authMode != "external" {
		log.Fatalln("Invalid auth mode: only `internal` and `external` values are accepted.")
	}

	// Get aerospike auth username
	username, err := getSecret(user)
	if err != nil {
		log.Fatal(err)
	}

	// Get aerospike auth password
	password, err := getSecret(pass)
	if err != nil {
		log.Fatal(err)
	}

	clientPolicy := aero.NewClientPolicy()
	clientPolicy.User = string(username)
	clientPolicy.Password = string(password)
	if authMode == "external" {
		clientPolicy.AuthMode = aero.AuthModeExternal
	}

	// allow only ONE connection
	clientPolicy.ConnectionQueueSize = 1
	clientPolicy.Timeout = time.Duration(config.Aerospike.Timeout) * time.Second

	clientPolicy.TlsConfig = initAerospikeTLS()

	if clientPolicy.TlsConfig != nil {
		ikService = "service-tls-std"
	}

	createNewConnection := func() (*aero.Connection, error) {
		conn, err := aero.NewConnection(clientPolicy, server)
		if err != nil {
			return nil, err
		}

		if clientPolicy.RequiresAuthentication() {
			if err := conn.Login(clientPolicy); err != nil {
				return nil, err
			}
		}

		// Set no connection deadline to re-use connection, but socketTimeout will be in effect
		var deadline time.Time
		err = conn.SetTimeout(deadline, clientPolicy.Timeout)
		if err != nil {
			return nil, err
		}

		return conn, nil
	}

	o = &Observer{
		newConnection: createNewConnection,
		ticks: prometheus.NewCounter(
			prometheus.CounterOpts{
				Namespace: "aerospike",
				Subsystem: "node",
				Name:      "ticks",
				Help:      "Counter that detemines how many times the Aerospike node was scraped for metrics.",
			}),
		watchers: []Watcher{
			&NamespaceWatcher{},
			&SetWatcher{},
			&LatencyWatcher{}, // gets the build version, used by watchers below
			&StatsWatcher{},
			&XdrWatcher{},
			&UserWatcher{},
			&JobsWatcher{},
			&SindexWatcher{}}, // the order is important here
	}

	return o, nil
}

// Describe function of Prometheus' Collector interface
func (o *Observer) Describe(ch chan<- *prometheus.Desc) {}

// Collect function of Prometheus' Collector interface
func (o *Observer) Collect(ch chan<- prometheus.Metric) {
	// Protect against concurrent scrapes
	o.mutex.Lock()
	defer o.mutex.Unlock()

	o.ticks.Inc()
	ch <- o.ticks

	stats, err := o.refresh(ch)
	if err != nil {
		log.Errorln(err)
		ch <- prometheus.MustNewConstMetric(nodeActiveDesc, prometheus.GaugeValue, 0.0, gClusterName, gService, gBuild)
		return
	}

	gClusterName, gService, gBuild = stats[ikClusterName], stats[ikService], stats[ikBuild]
	ch <- prometheus.MustNewConstMetric(nodeActiveDesc, prometheus.GaugeValue, 1.0, gClusterName, gService, gBuild)
}

func (o *Observer) requestInfo(retryCount int, infoKeys []string) (map[string]string, error) {
	var err error
	rawMetrics := make(map[string]string)

	// Retry for connection, timeout, network errors
	// including errors from RequestInfo()
	for i := 0; i < retryCount; i++ {
		// Validate existing connection
		if o.conn == nil || !o.conn.IsConnected() {
			// Create new connection
			o.conn, err = o.newConnection()
			if err != nil {
				log.Debug(err)
				continue
			}
		}

		// Info request
		rawMetrics, err = o.conn.RequestInfo(infoKeys...)
		if err != nil {
			log.Debug(err)
			continue
		}

		break
	}

	if len(rawMetrics) == 1 {
		for k := range rawMetrics {
			if strings.HasPrefix(strings.ToUpper(k), "ERROR:") {
				return nil, errors.New(k)
			}
		}
	}

	return rawMetrics, err
}

func (o *Observer) refresh(ch chan<- prometheus.Metric) (map[string]string, error) {
	log.Debugf("Refreshing node %s", fullHost)

	// fetch first set of info keys
	var infoKeys []string
	for _, c := range o.watchers {
		if keys := c.passOneKeys(); len(keys) > 0 {
			infoKeys = append(infoKeys, keys...)
		}
	}

	// info request for first set of info keys
	rawMetrics, err := o.requestInfo(retryCount, infoKeys)
	if err != nil {
		return nil, err
	}

	// fetch second second set of info keys
	infoKeys = []string{ikClusterName, ikService, ikBuild}
	watcherInfoKeys := make([][]string, len(o.watchers))
	for i, c := range o.watchers {
		if keys := c.passTwoKeys(rawMetrics); len(keys) > 0 {
			infoKeys = append(infoKeys, keys...)
			watcherInfoKeys[i] = keys
		}
	}

	// info request for second set of info keys
	nRawMetrics, err := o.requestInfo(retryCount, infoKeys)
	if err != nil {
		return rawMetrics, err
	}

	rawMetrics = nRawMetrics

	// sanitize the utf8 strings before sending them to watchers
	for k, v := range rawMetrics {
		rawMetrics[k] = sanitizeUTF8(v)
	}

	for i, c := range o.watchers {
		if err := c.refresh(o, watcherInfoKeys[i], rawMetrics, ch); err != nil {
			return rawMetrics, err
		}
	}

	log.Debugf("Refreshing node was successful")

	return rawMetrics, nil
}
                                                                                                                                                                                                                                                                                                                     aerospike-prometheus-exporter/._pkg                                                                 000755  000765  000024  00000000243 14426143306 020767  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/pkg                                                         000755  000765  000024  00000000210 14426143306 022515  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.091016399
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/pkg/                                                                  000755  000765  000024  00000000000 14426143306 020625  5                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         aerospike-prometheus-exporter/pkg/._post-install.sh                                                 000755  000765  000024  00000000243 14426133132 024025  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/pkg/PaxHeader/post-install.sh                                         000755  000765  000024  00000000210 14426133132 025553  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.080670537
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/pkg/post-install.sh                                                   000755  000765  000024  00000000102 14426133132 023602  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         #!/bin/bash
systemctl enable aerospike-prometheus-exporter.service                                                                                                                                                                                                                                                                                                                                                                                                                                                              aerospike-prometheus-exporter/pkg/._Makefile                                                        000644  000765  000024  00000000243 14426143306 022501  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/pkg/PaxHeader/Makefile                                                000644  000765  000024  00000000210 14426143306 024227  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.091106143
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/pkg/Makefile                                                          000644  000765  000024  00000006366 14426143306 022300  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         # Include common variables from TOP DIR
include ../Makefile.vars

# Variables required for this Makefile
PKG_DIR = $(shell dirname $(realpath $(firstword $(MAKEFILE_LIST))))
TOP_DIR = $(PKG_DIR)/..
BUILD_DIR = $(PKG_DIR)/build
TARGET_DIR = $(PKG_DIR)/target

# Package variables
NAME = "aerospike-prometheus-exporter"
VERSION = $(shell git describe --tags | cut -c 2-)
MAINTAINER = "Aerospike"
DESCRIPTION = "Aerospike Prometheus Exporter, An agent to export Aerospike metrics to Prometheus"
LICENSE = "Apache License 2.0"
URL = "https://github.com/aerospike/aerospike-prometheus-exporter"
VENDOR = "Aerospike, Inc."
ARCH ?= $(shell uname -m)
DEB_PKG_ARCH ?= $(shell dpkg-architecture -q DEB_BUILD_ARCH)


.PHONY: all
all: deb rpm tar

.PHONY: fipsparam
fipsparam: 
	@echo "fips enabled "$(IS_OS_FIPS_MODE)
	@echo "os-name "$(OS_FULL_NAME)
	@echo "APE_SUPPORTED_OS ==> "$(APE_SUPPORTED_OS)
ifeq ($(APE_SUPPORTED_OS),validfipsos)
	@echo  "Setting FIPS required params"
	$(eval GO_FIPS=$(GO_BORINGCRYPTO))
	$(eval PKG_FILENAME=$(FIPS_PKG_FILENAME))
	@echo  "Current PKG_FILENAME === "$(PKG_FILENAME)
else
	@echo  "Fips Exporter build is supported only on CentOS 8 or Red Hat 8 versions or have Golang v1.20 and above"
	exit 1
endif


.PHONY: fips-deb
fips-deb: fipsparam deb 
	@echo "Completed FIPS Packaging"

.PHONY: deb
deb: prep
	fpm --force \
		--config-files /etc/aerospike-prometheus-exporter \
		--input-type dir \
		--output-type deb \
		--chdir $(BUILD_DIR)/ \
		--after-install $(PKG_DIR)/post-install.sh \
		--name $(NAME) \
		--version $(VERSION) \
		--maintainer $(MAINTAINER) \
		--description $(DESCRIPTION) \
		--license $(LICENSE) \
		--url $(URL) \
		--vendor $(VENDOR) \
		--architecture $(DEB_PKG_ARCH) \
		--package $(TARGET_DIR)/$(PKG_FILENAME)_$(VERSION)_$(DEB_PKG_ARCH).deb


.PHONY: fips-rpm
fips-rpm: fipsparam rpm 
	@echo "Completed FIPS Packaging"

.PHONY: rpm
rpm: prep
	fpm --force \
		--config-files /etc/aerospike-prometheus-exporter \
		--input-type dir \
		--output-type rpm \
		--chdir $(BUILD_DIR)/ \
		--after-install $(PKG_DIR)/post-install.sh \
		--name $(NAME) \
		--version $(VERSION) \
		--maintainer $(MAINTAINER) \
		--description $(DESCRIPTION) \
		--license $(LICENSE) \
		--url $(URL) \
		--vendor $(VENDOR) \
		--architecture $(ARCH) \
		--package $(TARGET_DIR)/$(PKG_FILENAME)-$(VERSION).$(ARCH).rpm

.PHONY: fips-tar
fips-tar: fipsparam tar 

.PHONY: tar
tar: prep
	fpm --force \
		--config-files /etc/aerospike-prometheus-exporter \
		--input-type dir \
		--output-type tar \
		--chdir $(BUILD_DIR)/ \
		--after-install $(PKG_DIR)/post-install.sh \
		--name $(NAME) \
		--version $(VERSION) \
		--maintainer $(MAINTAINER) \
		--description $(DESCRIPTION) \
		--license $(LICENSE) \
		--url $(URL) \
		--vendor $(VENDOR) \
		--package $(TARGET_DIR)/$(PKG_FILENAME)_$(VERSION)_$(ARCH).tar

.PHONY: prep
prep:
	@echo "prep PKG_FILENAME "$(PKG_FILENAME)
	install -d $(TARGET_DIR)
	install -d $(BUILD_DIR)/usr/bin
	install -d $(BUILD_DIR)/etc/aerospike-prometheus-exporter
	install -pm 755 $(TOP_DIR)/aerospike-prometheus-exporter $(BUILD_DIR)/usr/bin/aerospike-prometheus-exporter
	install -pm 644 $(TOP_DIR)/ape.toml $(BUILD_DIR)/etc/aerospike-prometheus-exporter/ape.toml

.PHONY: clean
clean:
	rm -rf $(TARGET_DIR)
	rm -rf $(BUILD_DIR)/etc
	rm -rf $(BUILD_DIR)/usr/bin
                                                                                                                                                                                                                                                                          aerospike-prometheus-exporter/pkg/._build                                                           000755  000765  000024  00000000243 14426133132 022062  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/pkg/PaxHeader/build                                                   000755  000765  000024  00000000210 14426133132 023610  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.080207664
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/pkg/build/                                                            000755  000765  000024  00000000000 14426133132 021720  5                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         aerospike-prometheus-exporter/pkg/build/._usr                                                       000755  000765  000024  00000000243 14426133132 022673  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/pkg/build/PaxHeader/usr                                               000755  000765  000024  00000000210 14426133132 024421  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.080268664
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/pkg/build/usr/                                                        000755  000765  000024  00000000000 14426133132 022531  5                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         aerospike-prometheus-exporter/pkg/build/usr/._lib                                                   000755  000765  000024  00000000243 14426133132 023441  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/pkg/build/usr/PaxHeader/lib                                           000755  000765  000024  00000000210 14426133132 025167  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.080331747
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/pkg/build/usr/lib/                                                    000755  000765  000024  00000000000 14426133132 023277  5                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         aerospike-prometheus-exporter/pkg/build/usr/lib/._systemd                                           000755  000765  000024  00000000243 14426133132 025131  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/pkg/build/usr/lib/PaxHeader/systemd                                   000755  000765  000024  00000000210 14426133132 026657  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.080403413
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/pkg/build/usr/lib/systemd/                                            000755  000765  000024  00000000000 14426133132 024767  5                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         aerospike-prometheus-exporter/pkg/build/usr/lib/systemd/._system                                    000755  000765  000024  00000000243 14426133132 026455  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/pkg/build/usr/lib/systemd/PaxHeader/system                            000755  000765  000024  00000000210 14426133132 030203  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683535450.080484496
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/pkg/build/usr/lib/systemd/system/                                     000755  000765  000024  00000000000 14426133132 026313  5                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         pkg/build/usr/lib/systemd/system/._aerospike-prometheus-exporter.service                            000644  000765  000024  00000000243 14426133132 036053  0                                                                                                    ustar 00phaniram                        staff                           000000  000000  aerospike-prometheus-exporter                                                                                                                                              Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             pkg/build/usr/lib/systemd/system/PaxHeader/aerospike-prometheus-exporter.service                    000644  000765  000024  00000000210 14426133132 037601  x                                                                                                    ustar 00phaniram                        staff                           000000  000000  aerospike-prometheus-exporter                                                                                                                                          30 mtime=1683535450.080555829
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/pkg/build/usr/lib/systemd/system/aerospike-prometheus-exporter.service000644  000765  000024  00000000512 14426133132 035714  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         [Unit]
Description=Aerospike Prometheus Exporter Service
Documentation=https://github.com/aerospike/aerospike-prometheus-exporter
Wants=network.target
After=network-online.target

[Service]
ExecStart=/usr/bin/aerospike-prometheus-exporter --config /etc/aerospike-prometheus-exporter/ape.toml

[Install]
WantedBy=multi-user.target
                                                                                                                                                                                      aerospike-prometheus-exporter/._tests                                                               000755  000765  000024  00000000243 14426143306 021350  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/tests                                                       000755  000765  000024  00000000210 14426143306 023076  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.091357873
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/tests/                                                                000755  000765  000024  00000000000 14426143306 021206  5                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         aerospike-prometheus-exporter/tests/._default_ape.toml                                              000644  000765  000024  00000000243 14426143306 024570  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/tests/PaxHeader/default_ape.toml                                      000644  000765  000024  00000000210 14426143306 026316  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.091303253
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/tests/default_ape.toml                                                000644  000765  000024  00000015145 14426143306 024362  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         [Agent]
# Exporter HTTPS (TLS) configuration
# HTTPS between Prometheus and Exporter

# TLS certificates.
# Supports below formats,
# 1. Certificate file path                                      - "file:<file-path>"
# 2. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
# 3. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
# Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

# Server certificate
cert_file = ""

# Private key associated with server certificate
key_file = ""

# Root CA to validate client certificates (for mutual TLS)
root_ca = ""

# Passphrase for encrypted key_file. Supports below formats,
# 1. Passphrase directly                                                      - "<passphrase>"
# 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
# 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
# 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
# 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
key_file_passphrase = ""

# labels to add to the prometheus metrics for e.g. labels={zone="asia-south1-a", platform="google compute engine"}
labels = {}

bind = ":9145"

# metrics server timeout in seconds
timeout = 10

# Exporter logging configuration
# Log file path (optional, logs to console by default)
# Level can be info|warning,warn|error,err|debug|trace ('info' by default)
log_file = ""
log_level = ""

# Basic HTTP authentication for '/metrics'.
# Supports below formats,
# 1. Credential directly                                                      - "<credential>"
# 2. Credential via file                                                      - "file:<file-that-contains-credential>"
# 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
# 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
# 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
basic_auth_username = ""
basic_auth_password = ""

[Aerospike]
db_host = "localhost"
db_port = 3000

# TLS certificates.
# Supports below formats,
# 1. Certificate file path                                      - "file:<file-path>"
# 2. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
# 3. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
# Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

# root certificate file
root_ca = ""

# certificate file
cert_file = ""

# key file
key_file = ""

# Passphrase for encrypted key_file. Supports below formats,
# 1. Passphrase directly                                                      - "<passphrase>"
# 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
# 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
# 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
# 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
key_file_passphrase = ""

# node TLS name for authentication
node_tls_name = ""

# Aerospike cluster security credentials.
# Supports below formats,
# 1. Credential directly                                                      - "<credential>"
# 2. Credential via file                                                      - "file:<file-that-contains-credential>"
# 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
# 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
# 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
# Applicable to 'user' and 'password' configurations.

# database user
user = ""

# database password
password = ""

# authentication mode: internal (for server), external (LDAP, etc.)
auth_mode = ""

# timeout for sending commands to the server node in seconds
timeout = 5

# Number of histogram buckets to export for latency metrics. Bucket thresholds range from 2^0 to 2^16 (17 buckets).
# e.g. latency_buckets_count=5 will export first five buckets i.e. <=1ms, <=2ms, <=4ms, <=8ms and <=16ms.
# Default: 0 (export all threshold buckets).
latency_buckets_count = 0

# Order of context - namespace, set, latencies, node-stats, xdr, user, jobs, sindex

# Metrics Allowlist - If specified, only these metrics will be scraped. An empty list will exclude all metrics.
# Commenting out the below allowlist configs will disable metrics filtering (i.e. all metrics will be scraped).

# Metrics Blocklist - If specified, these metrics will be NOT be scraped. An empty list will include all metrics.
# Commenting out the below blocklist configs will disable metrics filtering (i.e. no metrics will be blocked/filtered).

# globbing pattern (wildcard) are allowd for allowlist and blocklist
# for example "batch_index_*_buffers"

# Namespace metrics allowlist, to control which Namespace metrics should be collected.
# namespace_metrics_allowlist = []
# namespace_metrics_blocklist = []

# set_metrics_allowlist = []
# set_metrics_blocklist = []

# Latencies histogram allowlist, to control which Histogram-name metrics should be collected. 
# Note: globbing patterns (wildcard) are not supported for this latency metric configuration. 
# latencies_metrics_allowlist = []
# latencies_metrics_blocklist = []

# node_metrics_allowlist = []
# node_metrics_blocklist = []

# Support only from Aerospike versions 5.0 and above
# xdr_metrics_allowlist = []
# xdr_metrics_blocklist = []

# User statistics are available in Aerospike 5.6+
# Note globbing patterns (wildcard) are not supported for this User configuration.
# user_metrics_users_allowlist = []
# user_metrics_users_blocklist = []

# job_metrics_allowlist = []
# job_metrics_blocklist = []

# sindex_metrics_allowlist = []
# sindex_metrics_blocklist = []

                                                                                                                                                                                                                                                                                                                                                                                                                           aerospike-prometheus-exporter/tests/._ns_allow_block_list_ape.toml                                  000644  000765  000024  00000000243 14426143306 027167  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �fu{��                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/tests/PaxHeader/ns_allow_block_list_ape.toml                          000644  000765  000024  00000000210 14426143306 030715  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683539654.091441242
57 LIBARCHIVE.xattr.com.apple.provenance=AQAADsFmH3V7kIM
49 SCHILY.xattr.com.apple.provenance=  �fu{��
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/tests/ns_allow_block_list_ape.toml                                    000644  000765  000024  00000015164 14426143306 026762  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         [Agent]
# Exporter HTTPS (TLS) configuration
# HTTPS between Prometheus and Exporter

# TLS certificates.
# Supports below formats,
# 1. Certificate file path                                      - "file:<file-path>"
# 2. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
# 3. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
# Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

# Server certificate
cert_file = ""

# Private key associated with server certificate
key_file = ""

# Root CA to validate client certificates (for mutual TLS)
root_ca = ""

# Passphrase for encrypted key_file. Supports below formats,
# 1. Passphrase directly                                                      - "<passphrase>"
# 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
# 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
# 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
# 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
key_file_passphrase = ""

# labels to add to the prometheus metrics for e.g. labels={zone="asia-south1-a", platform="google compute engine"}
labels = {}

bind = ":9145"

# metrics server timeout in seconds
timeout = 10

# Exporter logging configuration
# Log file path (optional, logs to console by default)
# Level can be info|warning,warn|error,err|debug|trace ('info' by default)
log_file = ""
log_level = ""

# Basic HTTP authentication for '/metrics'.
# Supports below formats,
# 1. Credential directly                                                      - "<credential>"
# 2. Credential via file                                                      - "file:<file-that-contains-credential>"
# 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
# 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
# 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
basic_auth_username = ""
basic_auth_password = ""

[Aerospike]
db_host = "localhost"
db_port = 3000

# TLS certificates.
# Supports below formats,
# 1. Certificate file path                                      - "file:<file-path>"
# 2. Environment variable containing base64 encoded certificate - "env-b64:<environment-variable-that-contains-base64-encoded-certificate>"
# 3. Base64 encoded certificate                                 - "b64:<base64-encoded-certificate>"
# Applicable to 'root_ca', 'cert_file' and 'key_file' configurations.

# root certificate file
root_ca = ""

# certificate file
cert_file = ""

# key file
key_file = ""

# Passphrase for encrypted key_file. Supports below formats,
# 1. Passphrase directly                                                      - "<passphrase>"
# 2. Passphrase via file                                                      - "file:<file-that-contains-passphrase>"
# 3. Passphrase via environment variable                                      - "env:<environment-variable-that-holds-passphrase>"
# 4. Passphrase via environment variable containing base64 encoded passphrase - "env-b64:<environment-variable-that-contains-base64-encoded-passphrase>"
# 5. Passphrase in base64 encoded form                                        - "b64:<base64-encoded-passphrase>"
key_file_passphrase = ""

# node TLS name for authentication
node_tls_name = ""

# Aerospike cluster security credentials.
# Supports below formats,
# 1. Credential directly                                                      - "<credential>"
# 2. Credential via file                                                      - "file:<file-that-contains-credential>"
# 3. Credential via environment variable                                      - "env:<environment-variable-that-contains-credential>"
# 4. Credential via environment variable containing base64 encoded credential - "env-b64:<environment-variable-that-contains-base64-encoded-credential>"
# 5. Credential in base64 encoded form                                        - "b64:<base64-encoded-credential>"
# Applicable to 'user' and 'password' configurations.

# database user
user = ""

# database password
password = ""

# authentication mode: internal (for server), external (LDAP, etc.)
auth_mode = ""

# timeout for sending commands to the server node in seconds
timeout = 5

# Number of histogram buckets to export for latency metrics. Bucket thresholds range from 2^0 to 2^16 (17 buckets).
# e.g. latency_buckets_count=5 will export first five buckets i.e. <=1ms, <=2ms, <=4ms, <=8ms and <=16ms.
# Default: 0 (export all threshold buckets).
latency_buckets_count = 0

# Order of context - namespace, set, latencies, node-stats, xdr, user, jobs, sindex

# Metrics Allowlist - If specified, only these metrics will be scraped. An empty list will exclude all metrics.
# Commenting out the below allowlist configs will disable metrics filtering (i.e. all metrics will be scraped).

# Metrics Blocklist - If specified, these metrics will be NOT be scraped. An empty list will include all metrics.
# Commenting out the below blocklist configs will disable metrics filtering (i.e. no metrics will be blocked/filtered).

# globbing pattern (wildcard) are allowd for allowlist and blocklist
# for example "batch_index_*_buffers"

# Namespace metrics allowlist, to control which Namespace metrics should be collected.
#namespace_metrics_allowlist = ["master*object*"]
# namespace_metrics_blocklist = []

# set_metrics_allowlist = []
# set_metrics_blocklist = []

# Latencies histogram allowlist, to control which Histogram-name metrics should be collected. 
# Note: globbing patterns (wildcard) are not supported for this latency metric configuration. 
# latencies_metrics_allowlist = []
# latencies_metrics_blocklist = []

# node_metrics_allowlist = []
# node_metrics_blocklist = []

# Support only from Aerospike versions 5.0 and above
# xdr_metrics_allowlist = []
# xdr_metrics_blocklist = []

# User statistics are available in Aerospike 5.6+
# Note globbing patterns (wildcard) are not supported for this User configuration.
# user_metrics_users_allowlist = []
# user_metrics_users_blocklist = []

# job_metrics_allowlist = []
# job_metrics_blocklist = []

# sindex_metrics_allowlist = []
# sindex_metrics_blocklist = []

                                                                                                                                                                                                                                                                                                                                                                                                            aerospike-prometheus-exporter/._types.go                                                            000644  000765  000024  00000000243 14426144235 021755  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �`�jݹz                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/types.go                                                    000644  000765  000024  00000000210 14426144235 023503  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683540125.584711779
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAhWDpat25B3o
49 SCHILY.xattr.com.apple.provenance=  �`�jݹz
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/types.go                                                              000644  000765  000024  00000003031 14426144235 021536  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import "github.com/prometheus/client_golang/prometheus"

type MetricMap map[string]promMetric

type metricType byte

const (
	mtGauge   metricType = 'G'
	mtCounter metricType = 'C'
)

type Watcher interface {
	passOneKeys() []string
	passTwoKeys(rawMetrics map[string]string) []string
	refresh(o *Observer, infoKeys []string, rawMetrics map[string]string, ch chan<- prometheus.Metric) error
	describe(ch chan<- *prometheus.Desc)
}

type promMetric struct {
	origDesc  string
	desc      *prometheus.Desc
	valueType prometheus.ValueType
}

type StatsMap map[string]interface{}

// Value should be an int64 or a convertible string; otherwise defValue is returned
// this function never panics
func (s StatsMap) TryString(name string, defValue string, aliases ...string) string {
	field := s.Get(name, aliases...)
	if field != nil {
		if value, ok := field.(string); ok {
			return value
		}
	}
	return defValue
}

func (s StatsMap) Get(name string, aliases ...string) interface{} {
	if val, exists := s[name]; exists {
		return val
	}

	for _, alias := range aliases {
		if val, exists := s[alias]; exists {
			return val
		}
	}

	return nil
}

// Value should be an float64 or a convertible string; otherwise defValue is returned
// this function never panics
func (s StatsMap) TryFloat(name string, defValue float64, aliases ...string) float64 {
	field := s.Get(name, aliases...)
	if field != nil {
		if value, ok := field.(float64); ok {
			return value
		}
		if value, ok := field.(int64); ok {
			return float64(value)
		}
	}
	return defValue
}
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       aerospike-prometheus-exporter/._watcher_jobs.go                                                     000644  000765  000024  00000000243 14426445760 023272  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/watcher_jobs.go                                             000644  000765  000024  00000000210 14426445760 025020  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683639280.925111256
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/watcher_jobs.go                                                       000644  000765  000024  00000006130 14426445760 023056  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"strings"

	"github.com/prometheus/client_golang/prometheus"

	log "github.com/sirupsen/logrus"
)

// Jobs raw metrics
var jobsRawMetrics = map[string]metricType{
	"priority":           mtGauge,
	"net-io-time":        mtGauge,
	"n-pids-requested":   mtGauge,
	"rps":                mtGauge,
	"active-threads":     mtGauge,
	"job-progress":       mtGauge,
	"run-time":           mtGauge,
	"time-since-done":    mtGauge,
	"recs-throttled":     mtGauge,
	"recs-filtered-meta": mtGauge,
	"recs-filtered-bins": mtGauge,
	"recs-succeeded":     mtGauge,
	"recs-failed":        mtGauge,
	"net-io-bytes":       mtGauge,
	"socket-timeout":     mtGauge,
	"udf-active":         mtGauge,
	"ops-active":         mtGauge,
}

type JobsWatcher struct{}

func (jw *JobsWatcher) describe(ch chan<- *prometheus.Desc) {}

func (jw *JobsWatcher) passOneKeys() []string {
	// "build" info key should be returned here,
	// but it is also being sent by LatencyWatcher.passOneKeys(),
	// hence skipping here.
	return nil
}

func (jw *JobsWatcher) passTwoKeys(rawMetrics map[string]string) (jobsCommands []string) {
	if config.Aerospike.DisableJobMetrics {
		// disabled
		return nil
	}

	jobsCommands = []string{"jobs:", "scan-show:", "query-show:"}

	ok, err := buildVersionGreaterThanOrEqual(rawMetrics, "6.0.0.0-0")
	if err != nil {
		log.Warn(err)
		return jobsCommands
	}

	if ok {
		return []string{"query-show:"}
	}

	ok, err = buildVersionGreaterThanOrEqual(rawMetrics, "5.7.0.0")
	if err != nil {
		log.Warn(err)
		return jobsCommands
	}

	if ok {
		return []string{"scan-show:", "query-show:"}
	}

	return []string{"jobs:"}
}

var jobMetrics map[string]metricType

func (jw *JobsWatcher) refresh(o *Observer, infoKeys []string, rawMetrics map[string]string, ch chan<- prometheus.Metric) error {
	if config.Aerospike.DisableJobMetrics {
		// disabled
		return nil
	}

	var jobStats []string

	if rawMetrics["scan-show:"] != "" || rawMetrics["query-show:"] != "" {
		jobStats = strings.Split(rawMetrics["scan-show:"], ";")
		jobStats = append(jobStats, strings.Split(rawMetrics["query-show:"], ";")...)
	} else {
		jobStats = strings.Split(rawMetrics["jobs:"], ";")
	}
	log.Tracef("job-stats:%v", jobStats)

	if jobMetrics == nil {
		jobMetrics = getFilteredMetrics(jobsRawMetrics, config.Aerospike.JobMetricsAllowlist, config.Aerospike.JobMetricsAllowlistEnabled, config.Aerospike.JobMetricsBlocklist)
	}

	for i := range jobStats {
		jobObserver := make(MetricMap, len(jobMetrics))
		for m, t := range jobMetrics {
			jobObserver[m] = makeMetric("aerospike_jobs", m, t, config.AeroProm.MetricLabels, "cluster_name", "service", "ns", "set", "module", "job_type", "trid", "sindex_name")
		}

		stats := parseStats(jobStats[i], ":")
		for stat, pm := range jobObserver {
			v, exists := stats[stat]
			if !exists {
				// not found
				continue
			}

			pv, err := tryConvert(v)
			if err != nil {
				continue
			}

			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, pv, rawMetrics[ikClusterName], rawMetrics[ikService], stats["ns"], stats["set"], stats["module"], stats["job-type"], stats["trid"], stats["sindex-name"])
		}
	}

	return nil
}
                                                                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/._watcher_latency.go                                                  000644  000765  000024  00000000243 14426446003 023763  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/watcher_latency.go                                          000644  000765  000024  00000000210 14426446003 025511  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683639299.503596421
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/watcher_latency.go                                                    000644  000765  000024  00000006312 14426446003 023551  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"github.com/prometheus/client_golang/prometheus"

	log "github.com/sirupsen/logrus"
)

type LatencyWatcher struct {
}

func (lw *LatencyWatcher) describe(ch chan<- *prometheus.Desc) {}

func (lw *LatencyWatcher) passOneKeys() []string {
	return []string{"build"}
}

func (lw *LatencyWatcher) passTwoKeys(rawMetrics map[string]string) (latencyCommands []string) {

	// return if this feature is disabled.
	if config.Aerospike.DisableLatenciesMetrics {
		// disabled
		return nil
	}

	latencyCommands = []string{"latencies:", "latency:"}

	ok, err := buildVersionGreaterThanOrEqual(rawMetrics, "5.1.0.0")
	if err != nil {
		log.Warn(err)
		return latencyCommands
	}

	if ok {
		return []string{"latencies:"}
	}

	return []string{"latency:"}
}

func (lw *LatencyWatcher) refresh(o *Observer, infoKeys []string, rawMetrics map[string]string, ch chan<- prometheus.Metric) error {

	allowedLatenciesList := make(map[string]struct{})
	blockedLatenciessList := make(map[string]struct{})

	if config.Aerospike.LatenciesMetricsAllowlistEnabled {
		for _, allowedLatencies := range config.Aerospike.LatenciesMetricsAllowlist {
			allowedLatenciesList[allowedLatencies] = struct{}{}
		}
	}

	if len(config.Aerospike.LatenciesMetricsBlocklist) > 0 {
		for _, blockedLatencies := range config.Aerospike.LatenciesMetricsBlocklist {
			blockedLatenciessList[blockedLatencies] = struct{}{}
		}
	}

	var latencyStats map[string]StatsMap

	if rawMetrics["latencies:"] != "" {
		latencyStats = parseLatencyInfo(rawMetrics["latencies:"], int(config.Aerospike.LatencyBucketsCount))
	} else {
		latencyStats = parseLatencyInfoLegacy(rawMetrics["latency:"], int(config.Aerospike.LatencyBucketsCount))
	}

	log.Tracef("latency-stats:%+v", latencyStats)

	for namespaceName, nsLatencyStats := range latencyStats {
		for operation, opLatencyStats := range nsLatencyStats {

			// operation comes from server as histogram-names
			if config.Aerospike.LatenciesMetricsAllowlistEnabled {
				if _, ok := allowedLatenciesList[operation]; !ok {
					continue
				}
			}

			if len(config.Aerospike.LatenciesMetricsBlocklist) > 0 {
				if _, ok := blockedLatenciessList[operation]; ok {
					continue
				}
			}

			for i, labelValue := range opLatencyStats.(StatsMap)["bucketLabels"].([]string) {
				// aerospike_latencies_<operation>_<timeunit>_bucket metric - Less than or equal to histogram buckets
				pm := makeMetric("aerospike_latencies", operation+"_"+opLatencyStats.(StatsMap)["timeUnit"].(string)+"_bucket", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "ns", "le")
				ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, opLatencyStats.(StatsMap)["bucketValues"].([]float64)[i], rawMetrics[ikClusterName], rawMetrics[ikService], namespaceName, labelValue)

				// aerospike_latencies_<operation>_<timeunit>_count metric
				if i == 0 {
					pm = makeMetric("aerospike_latencies", operation+"_"+opLatencyStats.(StatsMap)["timeUnit"].(string)+"_count", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "ns")
					ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, opLatencyStats.(StatsMap)["bucketValues"].([]float64)[i], rawMetrics[ikClusterName], rawMetrics[ikService], namespaceName)
				}
			}
		}
	}

	return nil
}
                                                                                                                                                                                                                                                                                                                      aerospike-prometheus-exporter/._watcher_namespaces.go                                               000644  000765  000024  00000000243 14426445741 024453  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/watcher_namespaces.go                                       000644  000765  000024  00000000210 14426445741 026201  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683639265.687316328
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/watcher_namespaces.go                                                 000644  000765  000024  00000066344 14426445741 024254  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"regexp"
	"strings"

	"github.com/prometheus/client_golang/prometheus"

	log "github.com/sirupsen/logrus"
)

// Namespace raw metrics
var namespaceRawMetrics = map[string]metricType{
	"allow-nonxdr-writes":                    mtGauge,
	"allow-xdr-writes":                       mtGauge,
	"cache_read_pct":                         mtGauge,
	"cold-start-evict-ttl":                   mtGauge,
	"conflict-resolution-policy":             mtGauge,
	"conflict-resolve-writes":                mtGauge,
	"data-in-index":                          mtGauge,
	"default-ttl":                            mtGauge,
	"disable-write-dup-res":                  mtGauge,
	"disallow-null-setname":                  mtGauge,
	"enable-benchmarks-batch-sub":            mtGauge,
	"enable-benchmarks-read":                 mtGauge,
	"enable-benchmarks-udf-sub":              mtGauge,
	"enable-benchmarks-udf":                  mtGauge,
	"enable-benchmarks-write":                mtGauge,
	"enable-benchmarks-ops-sub":              mtGauge,
	"enable-hist-proxy":                      mtGauge,
	"enable-xdr":                             mtGauge,
	"evict_ttl":                              mtGauge,
	"geo2dsphere-within.earth-radius-meters": mtGauge,
	"geo2dsphere-within.level-mod":           mtGauge,
	"geo2dsphere-within.max-cells":           mtGauge,
	"geo2dsphere-within.max-level":           mtGauge,
	"geo2dsphere-within.min-level":           mtGauge,
	"geo2dsphere-within.strict":              mtGauge,
	"max-ttl":                                mtGauge,
	"migrate-order":                          mtGauge,
	"migrate-retransmit-ms":                  mtGauge,
	"migrate-sleep":                          mtGauge,
	"ns-forward-xdr-writes":                  mtGauge,
	"nsup_cycle_duration":                    mtGauge,
	"nsup_cycle_sleep_pct":                   mtGauge,
	"nsup_cycle_deleted_pct":                 mtGauge,
	"obj-size-hist-max":                      mtGauge,
	"partition-tree-locks":                   mtGauge,
	"partition-tree-sprigs":                  mtGauge,
	"rack-id":                                mtGauge,
	"read-consistency-level-override":        mtGauge,
	"sets-enable-xdr":                        mtGauge,
	"sindex.num-partitions":                  mtGauge,
	"single-bin":                             mtGauge,
	"storage-engine":                         mtGauge,
	"tomb-raider-eligible-age":               mtGauge,
	"tomb-raider-period":                     mtGauge,
	"truncate_lut":                           mtGauge,
	"write-commit-level-override":            mtGauge,
	"allow-ttl-without-nsup":                 mtGauge,
	"background-scan-max-rps":                mtGauge,
	"disable-cold-start-eviction":            mtGauge,
	"index-stage-size":                       mtGauge,
	"nsup-hist-period":                       mtGauge,
	"nsup-period":                            mtGauge,
	"nsup-threads":                           mtGauge,
	"prefer-uniform-balance":                 mtGauge,
	"reject-non-xdr-writes":                  mtGauge,
	"reject-xdr-writes":                      mtGauge,
	"single-scan-threads":                    mtGauge,
	"strong-consistency":                     mtGauge,
	"strong-consistency-allow-expunge":       mtGauge,
	"transaction-pending-limit":              mtGauge,
	"truncate-threads":                       mtGauge,
	"xdr-tomb-raider-period":                 mtGauge,
	"xdr-tomb-raider-threads":                mtGauge,
	"xdr-bin-tombstone-ttl":                  mtGauge,
	"ignore-migrate-fill-delay":              mtGauge,
	"max-record-size":                        mtGauge,

	"clock_skew_stop_writes":                   mtGauge,
	"unreplicated_records":                     mtGauge,
	"dead_partitions":                          mtGauge,
	"unavailable_partitions":                   mtGauge,
	"available_bin_names":                      mtGauge,
	"defrag_q":                                 mtGauge,
	"pmem_available_pct":                       mtGauge,
	"pmem_free_pct":                            mtGauge,
	"pmem_total_bytes":                         mtGauge,
	"pmem_used_bytes":                          mtGauge,
	"pmem_compression_ratio":                   mtGauge,
	"device_available_pct":                     mtGauge,
	"device_compression_ratio":                 mtGauge,
	"device_free_pct":                          mtGauge,
	"device_total_bytes":                       mtGauge,
	"device_used_bytes":                        mtGauge,
	"effective_is_quiesced":                    mtGauge,
	"effective_replication_factor":             mtGauge,
	"evict-hist-buckets":                       mtGauge,
	"evict-tenths-pct":                         mtGauge,
	"high-water-disk-pct":                      mtGauge,
	"high-water-memory-pct":                    mtGauge,
	"hwm_breached":                             mtGauge,
	"index_pmem_used_bytes":                    mtGauge,
	"index_pmem_used_pct":                      mtGauge,
	"index_flash_used_bytes":                   mtGauge,
	"index_flash_used_pct":                     mtGauge,
	"index_flash_alloc_bytes":                  mtGauge,
	"index_flash_alloc_pct":                    mtGauge,
	"index-type.mounts-high-water-pct":         mtGauge,
	"index-type.mounts-size-limit":             mtGauge,
	"master_objects":                           mtGauge,
	"master_tombstones":                        mtGauge,
	"memory_free_pct":                          mtGauge,
	"memory_used_bytes":                        mtGauge,
	"memory_used_data_bytes":                   mtGauge,
	"memory_used_index_bytes":                  mtGauge,
	"memory_used_set_index_bytes":              mtGauge,
	"memory_used_sindex_bytes":                 mtGauge,
	"memory-size":                              mtGauge,
	"migrate_record_receives":                  mtGauge,
	"migrate_record_retransmits":               mtGauge,
	"migrate_records_skipped":                  mtGauge,
	"migrate_records_transmitted":              mtGauge,
	"migrate_rx_instances":                     mtGauge,
	"migrate_rx_partitions_active":             mtGauge,
	"migrate_rx_partitions_initial":            mtGauge,
	"migrate_rx_partitions_remaining":          mtGauge,
	"migrate_signals_active":                   mtGauge,
	"migrate_signals_remaining":                mtGauge,
	"migrate_tx_instances":                     mtGauge,
	"migrate_tx_partitions_active":             mtGauge,
	"migrate_tx_partitions_imbalance":          mtGauge,
	"migrate_tx_partitions_initial":            mtGauge,
	"migrate_tx_partitions_remaining":          mtGauge,
	"n_nodes_quiesced":                         mtGauge,
	"non_expirable_objects":                    mtGauge,
	"non_replica_objects":                      mtGauge,
	"non_replica_tombstones":                   mtGauge,
	"ns_cluster_size":                          mtGauge,
	"objects":                                  mtGauge,
	"pending_quiesce":                          mtGauge,
	"prole_objects":                            mtGauge,
	"prole_tombstones":                         mtGauge,
	"replication-factor":                       mtGauge,
	"shadow_write_q":                           mtGauge,
	"stop_writes":                              mtGauge,
	"stop-writes-pct":                          mtGauge,
	"stop-writes-sys-memory-pct":               mtGauge,
	"tombstones":                               mtGauge,
	"write_q":                                  mtGauge,
	"xdr_tombstones":                           mtGauge,
	"xdr_bin_cemeteries":                       mtGauge,
	"record_proto_uncompressed_pct":            mtGauge,
	"record_proto_compression_ratio":           mtGauge,
	"scan_proto_uncompressed_pct":              mtGauge,
	"scan_proto_compression_ratio":             mtGauge,
	"query_proto_uncompressed_pct":             mtGauge,
	"query_proto_compression_ratio":            mtGauge,
	"effective_prefer_uniform_balance":         mtGauge,
	"migrate_tx_partitions_lead_remaining":     mtGauge,
	"appeals_tx_active":                        mtGauge,
	"appeals_rx_active":                        mtGauge,
	"appeals_tx_remaining":                     mtGauge,
	"query_basic_avg_rec_count":                mtGauge,
	"query_aggr_avg_rec_count":                 mtGauge,
	"truncated_records":                        mtCounter,
	"batch_sub_proxy_complete":                 mtCounter,
	"batch_sub_proxy_error":                    mtCounter,
	"batch_sub_proxy_timeout":                  mtCounter,
	"batch_sub_read_error":                     mtCounter,
	"batch_sub_read_not_found":                 mtCounter,
	"batch_sub_read_success":                   mtCounter,
	"batch_sub_read_timeout":                   mtCounter,
	"batch_sub_read_filtered_out":              mtCounter,
	"batch_sub_tsvc_error":                     mtCounter,
	"batch_sub_tsvc_timeout":                   mtCounter,
	"client_delete_error":                      mtCounter,
	"client_delete_not_found":                  mtCounter,
	"client_delete_success":                    mtCounter,
	"client_delete_timeout":                    mtCounter,
	"client_delete_filtered_out":               mtCounter,
	"client_lang_delete_success":               mtCounter,
	"client_lang_error":                        mtCounter,
	"client_lang_read_success":                 mtCounter,
	"client_lang_write_success":                mtCounter,
	"client_proxy_complete":                    mtCounter,
	"client_proxy_error":                       mtCounter,
	"client_proxy_timeout":                     mtCounter,
	"client_read_error":                        mtCounter,
	"client_read_not_found":                    mtCounter,
	"client_read_success":                      mtCounter,
	"client_read_timeout":                      mtCounter,
	"client_read_filtered_out":                 mtCounter,
	"client_tsvc_error":                        mtCounter,
	"client_tsvc_timeout":                      mtCounter,
	"client_udf_complete":                      mtCounter,
	"client_udf_error":                         mtCounter,
	"client_udf_timeout":                       mtCounter,
	"client_udf_filtered_out":                  mtCounter,
	"client_write_error":                       mtCounter,
	"client_write_success":                     mtCounter,
	"client_write_timeout":                     mtCounter,
	"client_write_filtered_out":                mtCounter,
	"defrag_reads":                             mtCounter,
	"defrag_writes":                            mtCounter,
	"evicted_objects":                          mtCounter,
	"expired_objects":                          mtCounter,
	"fail_generation":                          mtCounter,
	"fail_key_busy":                            mtCounter,
	"fail_record_too_big":                      mtCounter,
	"fail_xdr_forbidden":                       mtCounter,
	"fail_client_lost_conflict":                mtCounter,
	"fail_xdr_lost_conflict":                   mtCounter,
	"from_proxy_delete_error":                  mtCounter,
	"from_proxy_delete_not_found":              mtCounter,
	"from_proxy_delete_success":                mtCounter,
	"from_proxy_delete_timeout":                mtCounter,
	"from_proxy_delete_filtered_out":           mtCounter,
	"from_proxy_read_error":                    mtCounter,
	"from_proxy_read_not_found":                mtCounter,
	"from_proxy_read_success":                  mtCounter,
	"from_proxy_read_timeout":                  mtCounter,
	"from_proxy_read_filtered_out":             mtCounter,
	"from_proxy_tsvc_error":                    mtCounter,
	"from_proxy_tsvc_timeout":                  mtCounter,
	"from_proxy_write_error":                   mtCounter,
	"from_proxy_write_success":                 mtCounter,
	"from_proxy_write_timeout":                 mtCounter,
	"from_proxy_write_filtered_out":            mtCounter,
	"from_proxy_udf_complete":                  mtCounter,
	"from_proxy_udf_error":                     mtCounter,
	"from_proxy_udf_timeout":                   mtCounter,
	"from_proxy_udf_filtered_out":              mtCounter,
	"from_proxy_lang_read_success":             mtCounter,
	"from_proxy_lang_write_success":            mtCounter,
	"from_proxy_lang_delete_success":           mtCounter,
	"from_proxy_lang_error":                    mtCounter,
	"from_proxy_batch_sub_tsvc_error":          mtCounter,
	"from_proxy_batch_sub_tsvc_timeout":        mtCounter,
	"from_proxy_batch_sub_read_success":        mtCounter,
	"from_proxy_batch_sub_read_error":          mtCounter,
	"from_proxy_batch_sub_read_timeout":        mtCounter,
	"from_proxy_batch_sub_read_not_found":      mtCounter,
	"from_proxy_batch_sub_read_filtered_out":   mtCounter,
	"geo_region_query_cells":                   mtCounter,
	"geo_region_query_falsepos":                mtCounter,
	"geo_region_query_points":                  mtCounter,
	"geo_region_query_reqs":                    mtCounter,
	"query_agg_abort":                          mtCounter,
	"query_agg_avg_rec_count":                  mtCounter,
	"query_agg_error":                          mtCounter,
	"query_agg_success":                        mtCounter,
	"query_agg":                                mtCounter,
	"query_fail":                               mtCounter,
	"query_long_queue_full":                    mtCounter,
	"query_long_reqs":                          mtCounter,
	"query_lookup_abort":                       mtCounter,
	"query_lookup_avg_rec_count":               mtCounter,
	"query_lookup_error":                       mtCounter,
	"query_lookup_success":                     mtCounter,
	"query_lookups":                            mtCounter,
	"query_reqs":                               mtCounter,
	"query_short_queue_full":                   mtCounter,
	"query_short_reqs":                         mtCounter,
	"query_udf_bg_failure":                     mtCounter,
	"query_udf_bg_success":                     mtCounter,
	"query_ops_bg_success":                     mtCounter,
	"query_ops_bg_failure":                     mtCounter,
	"retransmit_batch_sub_dup_res":             mtCounter,
	"retransmit_client_delete_dup_res":         mtCounter,
	"retransmit_client_delete_repl_write":      mtCounter,
	"retransmit_client_read_dup_res":           mtCounter,
	"retransmit_client_udf_dup_res":            mtCounter,
	"retransmit_client_udf_repl_write":         mtCounter,
	"retransmit_client_write_dup_res":          mtCounter,
	"retransmit_client_write_repl_write":       mtCounter,
	"retransmit_nsup_repl_write":               mtCounter,
	"retransmit_udf_sub_dup_res":               mtCounter,
	"retransmit_udf_sub_repl_write":            mtCounter,
	"scan_aggr_abort":                          mtCounter,
	"scan_aggr_complete":                       mtCounter,
	"scan_aggr_error":                          mtCounter,
	"scan_basic_abort":                         mtCounter,
	"scan_basic_complete":                      mtCounter,
	"scan_basic_error":                         mtCounter,
	"scan_udf_bg_abort":                        mtCounter,
	"scan_udf_bg_complete":                     mtCounter,
	"scan_udf_bg_error":                        mtCounter,
	"scan_ops_bg_complete":                     mtCounter,
	"scan_ops_bg_error":                        mtCounter,
	"scan_ops_bg_abort":                        mtCounter,
	"pi_query_long_basic_complete":             mtCounter,
	"pi_query_long_basic_error":                mtCounter,
	"pi_query_long_basic_abort":                mtCounter,
	"pi_query_short_basic_complete":            mtCounter,
	"pi_query_short_basic_error":               mtCounter,
	"pi_query_short_basic_timeout":             mtCounter,
	"pi_query_aggr_complete":                   mtCounter,
	"pi_query_aggr_error":                      mtCounter,
	"pi_query_aggr_abort":                      mtCounter,
	"pi_query_udf_bg_complete":                 mtCounter,
	"pi_query_udf_bg_error":                    mtCounter,
	"pi_query_udf_bg_abort":                    mtCounter,
	"pi_query_ops_bg_complete":                 mtCounter,
	"pi_query_ops_bg_error":                    mtCounter,
	"pi_query_ops_bg_abort":                    mtCounter,
	"udf_sub_lang_delete_success":              mtCounter,
	"udf_sub_lang_error":                       mtCounter,
	"udf_sub_lang_read_success":                mtCounter,
	"udf_sub_lang_write_success":               mtCounter,
	"udf_sub_tsvc_error":                       mtCounter,
	"udf_sub_tsvc_timeout":                     mtCounter,
	"udf_sub_udf_complete":                     mtCounter,
	"udf_sub_udf_error":                        mtCounter,
	"udf_sub_udf_timeout":                      mtCounter,
	"udf_sub_udf_filtered_out":                 mtCounter,
	"xdr_write_error":                          mtCounter,
	"xdr_write_success":                        mtCounter,
	"xdr_write_timeout":                        mtCounter,
	"appeals_records_exonerated":               mtCounter,
	"xdr_client_write_success":                 mtCounter,
	"xdr_client_write_error":                   mtCounter,
	"xdr_client_write_timeout":                 mtCounter,
	"xdr_client_delete_success":                mtCounter,
	"xdr_client_delete_error":                  mtCounter,
	"xdr_client_delete_timeout":                mtCounter,
	"xdr_client_delete_not_found":              mtCounter,
	"xdr_from_proxy_write_success":             mtCounter,
	"xdr_from_proxy_write_error":               mtCounter,
	"xdr_from_proxy_write_timeout":             mtCounter,
	"xdr_from_proxy_delete_success":            mtCounter,
	"xdr_from_proxy_delete_error":              mtCounter,
	"xdr_from_proxy_delete_timeout":            mtCounter,
	"xdr_from_proxy_delete_not_found":          mtCounter,
	"ops_sub_tsvc_error":                       mtCounter,
	"ops_sub_tsvc_timeout":                     mtCounter,
	"ops_sub_write_success":                    mtCounter,
	"ops_sub_write_error":                      mtCounter,
	"ops_sub_write_timeout":                    mtCounter,
	"ops_sub_write_filtered_out":               mtCounter,
	"dup_res_ask":                              mtCounter,
	"dup_res_respond_read":                     mtCounter,
	"dup_res_respond_no_read":                  mtCounter,
	"retransmit_all_read_dup_res":              mtCounter,
	"retransmit_all_write_dup_res":             mtCounter,
	"retransmit_all_write_repl_write":          mtCounter,
	"retransmit_all_delete_dup_res":            mtCounter,
	"retransmit_all_delete_repl_write":         mtCounter,
	"retransmit_all_udf_dup_res":               mtCounter,
	"retransmit_all_udf_repl_write":            mtCounter,
	"retransmit_all_batch_sub_dup_res":         mtCounter,
	"retransmit_ops_sub_dup_res":               mtCounter,
	"retransmit_ops_sub_repl_write":            mtCounter,
	"re_repl_success":                          mtCounter,
	"re_repl_error":                            mtCounter,
	"re_repl_timeout":                          mtCounter,
	"deleted_last_bin":                         mtCounter,
	"current_time":                             mtCounter,
	"evict_void_time":                          mtCounter,
	"smd_evict_void_time":                      mtCounter,
	"sindex_gc_cleaned":                        mtCounter,
	"query_false_positives":                    mtCounter,
	"query_basic_complete":                     mtCounter,
	"query_basic_error":                        mtCounter,
	"query_basic_abort":                        mtCounter,
	"query_aggr_complete":                      mtCounter,
	"query_aggr_error":                         mtCounter,
	"query_aggr_abort":                         mtCounter,
	"query_udf_bg_complete":                    mtCounter,
	"query_udf_bg_error":                       mtCounter,
	"query_udf_bg_abort":                       mtCounter,
	"query_ops_bg_complete":                    mtCounter,
	"query_ops_bg_error":                       mtCounter,
	"query_ops_bg_abort":                       mtCounter,
	"si_query_long_basic_complete":             mtCounter,
	"si_query_long_basic_error":                mtCounter,
	"si_query_long_basic_abort":                mtCounter,
	"si_query_short_basic_complete":            mtCounter,
	"si_query_short_basic_error":               mtCounter,
	"si_query_short_basic_timeout":             mtCounter,
	"si_query_aggr_complete":                   mtCounter,
	"si_query_aggr_error":                      mtCounter,
	"si_query_aggr_abort":                      mtCounter,
	"si_query_udf_bg_complete":                 mtCounter,
	"si_query_udf_bg_error":                    mtCounter,
	"si_query_udf_bg_abort":                    mtCounter,
	"si_query_ops_bg_complete":                 mtCounter,
	"si_query_ops_bg_error":                    mtCounter,
	"si_query_ops_bg_abort":                    mtCounter,
	"batch_sub_delete_error":                   mtCounter,
	"batch_sub_delete_not_found":               mtCounter,
	"batch_sub_delete_success":                 mtCounter,
	"batch_sub_delete_timeout":                 mtCounter,
	"batch_sub_delete_filtered_out":            mtCounter,
	"batch_sub_lang_error":                     mtCounter,
	"batch_sub_lang_delete_success":            mtCounter,
	"batch_sub_lang_read_success":              mtCounter,
	"batch_sub_lang_write_success":             mtCounter,
	"batch_sub_udf_complete":                   mtCounter,
	"batch_sub_udf_error":                      mtCounter,
	"batch_sub_udf_filtered_out":               mtCounter,
	"batch_sub_udf_timeout":                    mtCounter,
	"batch_sub_write_error":                    mtCounter,
	"batch_sub_write_filtered_out":             mtCounter,
	"batch_sub_write_success":                  mtCounter,
	"batch_sub_write_timeout":                  mtCounter,
	"from_proxy_batch_sub_delete_error":        mtCounter,
	"from_proxy_batch_sub_delete_filtered_out": mtCounter,
	"from_proxy_batch_sub_delete_not_found":    mtCounter,
	"from_proxy_batch_sub_delete_success":      mtCounter,
	"from_proxy_batch_sub_delete_timeout":      mtCounter,
	"from_proxy_batch_sub_lang_delete_success": mtCounter,
	"from_proxy_batch_sub_lang_error":          mtCounter,
	"from_proxy_batch_sub_lang_read_success":   mtCounter,
	"from_proxy_batch_sub_lang_write_success":  mtCounter,
	"from_proxy_batch_sub_udf_complete":        mtCounter,
	"from_proxy_batch_sub_udf_error":           mtCounter,
	"from_proxy_batch_sub_udf_filtered_out":    mtCounter,
	"from_proxy_batch_sub_udf_timeout":         mtCounter,
	"from_proxy_batch_sub_write_error":         mtCounter,
	"from_proxy_batch_sub_write_filtered_out":  mtCounter,
	"from_proxy_batch_sub_write_success":       mtCounter,
	"from_proxy_batch_sub_write_timeout":       mtCounter,
	"storage-engine.filesize":                  mtGauge, //=1073741824
	"storage-engine.write-block-size":          mtGauge, //=1048576
	"storage-engine.data-in-memory":            mtGauge, //=false
	"storage-engine.cold-start-empty":          mtGauge, //=false
	"storage-engine.commit-to-device":          mtGauge, //=false
	"storage-engine.commit-min-size":           mtGauge, //=0
	"storage-engine.compression-level":         mtGauge, //=0
	"storage-engine.defrag-lwm-pct":            mtGauge, //=50
	"storage-engine.defrag-queue-min":          mtGauge, //=0
	"storage-engine.defrag-sleep":              mtGauge, //=1000
	"storage-engine.defrag-startup-minimum":    mtGauge, //=10
	"storage-engine.direct-files":              mtGauge, //=false
	"storage-engine.enable-benchmarks-storage": mtGauge, //=false
	"storage-engine.flush-max-ms":              mtGauge, //=1000
	"storage-engine.max-write-cache":           mtGauge, //=67108864
	"storage-engine.min-avail-pct":             mtGauge, //=5
	"storage-engine.post-write-queue":          mtGauge, //=256
	"storage-engine.read-page-cache":           mtGauge, //=false
	"storage-engine.serialize-tomb-raider":     mtGauge, //=false
	"storage-engine.tomb-raider-sleep":         mtGauge, //=1000
	"storage-engine.cache-replica-writes":      mtGauge, //=false
	"storage-engine.disable-odsync":            mtGauge, //=false
	"storage-engine.max-used-pct":              mtGauge, //=70

	"storage-engine.file.age":              mtGauge,
	"storage-engine.file.defrag_q":         mtGauge,
	"storage-engine.file.defrag_reads":     mtGauge,
	"storage-engine.file.defrag_writes":    mtGauge,
	"storage-engine.file.free_wblocks":     mtGauge,
	"storage-engine.file.shadow_write_q":   mtGauge,
	"storage-engine.file.used_bytes":       mtGauge,
	"storage-engine.file.write_q":          mtGauge,
	"storage-engine.file.writes":           mtGauge,
	"storage-engine.device.age":            mtGauge,
	"storage-engine.device.defrag_q":       mtGauge,
	"storage-engine.device.defrag_reads":   mtGauge,
	"storage-engine.device.defrag_writes":  mtGauge,
	"storage-engine.device.free_wblocks":   mtGauge,
	"storage-engine.device.shadow_write_q": mtGauge,
	"storage-engine.device.used_bytes":     mtGauge,
	"storage-engine.device.write_q":        mtGauge,
	"storage-engine.device.writes":         mtGauge,
}

type NamespaceWatcher struct{}

func (nw *NamespaceWatcher) describe(ch chan<- *prometheus.Desc) {}

func (nw *NamespaceWatcher) passOneKeys() []string {
	return []string{"namespaces"}
}

func (nw *NamespaceWatcher) passTwoKeys(rawMetrics map[string]string) []string {
	s := rawMetrics["namespaces"]
	list := strings.Split(s, ";")

	var infoKeys []string
	for _, k := range list {
		infoKeys = append(infoKeys, "namespace/"+k)
	}

	return infoKeys
}

// Filtered namespace metrics. Populated by getFilteredMetrics() based on the config.Aerospike.NamespaceMetricsAllowlist, config.Aerospike.NamespaceMetricsBlocklist and namespaceRawMetrics.
var namespaceMetrics map[string]metricType

// Regex for identifying storage-engine stats.
var seDynamicExtractor = regexp.MustCompile(`storage\-engine\.(?P<type>file|device)\[(?P<idx>\d+)\]\.(?P<metric>.+)`)

func (nw *NamespaceWatcher) refresh(o *Observer, infoKeys []string, rawMetrics map[string]string, ch chan<- prometheus.Metric) error {
	if namespaceMetrics == nil {
		namespaceMetrics = getFilteredMetrics(namespaceRawMetrics, config.Aerospike.NamespaceMetricsAllowlist, config.Aerospike.NamespaceMetricsAllowlistEnabled, config.Aerospike.NamespaceMetricsBlocklist)
	}

	for _, ns := range infoKeys {
		nsName := strings.ReplaceAll(ns, "namespace/", "")
		log.Tracef("namespace-stats:%s:%s", nsName, rawMetrics[ns])

		namespaceObserver := make(MetricMap, len(namespaceMetrics))
		for m, t := range namespaceMetrics {
			namespaceObserver[m] = makeMetric("aerospike_namespace", m, t, config.AeroProm.MetricLabels, "cluster_name", "service", "ns")
		}

		stats := parseStats(rawMetrics[ns], ";")
		for stat, pm := range namespaceObserver {
			v, exists := stats[stat]
			if !exists {
				// not found
				continue
			}

			pv, err := tryConvert(v)
			if err != nil {
				continue
			}

			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, pv, rawMetrics[ikClusterName], rawMetrics[ikService], nsName)
		}

		for stat, value := range stats {
			match := seDynamicExtractor.FindStringSubmatch(stat)
			if len(match) != 4 {
				continue
			}

			metricType := match[1]
			metricIndex := match[2]
			metricName := match[3]

			_, exists := namespaceMetrics["storage-engine."+metricType+"."+metricName]
			if !exists {
				continue
			}

			deviceOrFileName := stats["storage-engine."+metricType+"["+metricIndex+"]"]
			pm := makeMetric("aerospike_namespace", "storage-engine_"+metricType+"_"+metricName, mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "ns", metricType+"_index", metricType)

			pv, err := tryConvert(value)
			if err != nil {
				continue
			}

			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, pv, rawMetrics[ikClusterName], rawMetrics[ikService], nsName, metricIndex, deviceOrFileName)
		}
	}

	return nil
}
                                                                                                                                                                                                                                                                                            aerospike-prometheus-exporter/._watcher_namespaces_test.go                                          000644  000765  000024  00000000243 14426144171 025503  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �`�jݹz                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/watcher_namespaces_test.go                                  000644  000765  000024  00000000207 14426144171 027237  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         29 mtime=1683540089.01210907
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAhWDpat25B3o
49 SCHILY.xattr.com.apple.provenance=  �`�jݹz
                                                                                                                                                                                                                                                                                                                                                                                         aerospike-prometheus-exporter/watcher_namespaces_test.go                                            000644  000765  000024  00000010573 14426144171 025275  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"fmt"
	"strings"
	"testing"
	"time"

	"github.com/prometheus/client_golang/prometheus"
	"github.com/stretchr/testify/assert"

	dto "github.com/prometheus/client_model/go"
)

func TestPassOneKeys(t *testing.T) {
	nsWatcher := new(NamespaceWatcher)
	// Check passoneKeys
	nsPassOneKeys := nsWatcher.passOneKeys()
	assert.Equal(t, nsPassOneKeys, []string{"namespaces"})

}

func TestPassTwoKeys(t *testing.T) {
	rawMetrics := getRawMetrics()
	nsWatcher := new(NamespaceWatcher)

	// simulate, as if we are sending requestInfo to AS and get the namespaces, these are coming from mock-data-generator
	pass2Keys := requestInfoNamespaces(rawMetrics)
	nsOutputs := nsWatcher.passTwoKeys(pass2Keys)

	// nsExpected := []string{"namespace/bar", "namespace/test"}
	nsExpected := createPassTwoExpectedOutputs(rawMetrics)

	assert := assert.New(t)

	for idx := range nsExpected {
		// assert each element returned by NamespaceWatcher exists in expected outputs
		assert.Contains(nsOutputs, nsExpected[idx], " value exists!")
	}
}

func TestNamespaceRefreshDefault(t *testing.T) {

	fmt.Println("initializing config ... TestNamespaceRefreshDefault")
	// Initialize and validate config
	config = new(Config)
	initConfig(DEFAULT_APE_TOML, config)

	config.validateAndUpdate()

	// read raw-metrics from mock data gen, create observer and channel prometeus metric ingestion and processing
	rawMetrics := getRawMetrics()
	nsWatcher := new(NamespaceWatcher)
	lObserver := &Observer{}
	ch := make(chan prometheus.Metric, 1000)
	pass2Metrics := requestInfoNamespaces(rawMetrics)

	nsWatcher.passTwoKeys(rawMetrics)

	expectedOutputs := createPassTwoExpectedOutputs(rawMetrics)

	// outputs := nsWatcher.passTwoKeys(pass2Metrics)
	// assert.Equal(t, outputs, expectedOutputs)

	err := nsWatcher.refresh(lObserver, expectedOutputs, rawMetrics, ch)

	if err != nil {
		// map of string ==> map["namespace/metric-name"]["<VALUE>"]
		// map of string ==> map["namespace/metric-name"]["<Label>"]
		//  both used to assert the return values from actual code against calculated values
		lOutputValues := map[string]string{}
		lOutputLabels := map[string]string{}

		// reads data from the Prom channel and creates a map of strings so we can assert in the below loop
		domore := 1

		for domore == 1 {
			select {

			case nsMetric := <-ch:
				description := nsMetric.Desc().String()
				var protobuffer dto.Metric
				err := nsMetric.Write(&protobuffer)
				if err != nil {
					fmt.Println(" unable to get metric ", description, " data into protobuf ", err)
				}

				metricValue := ""
				metricLabel := fmt.Sprintf("%s", protobuffer.Label)
				if protobuffer.Gauge != nil {
					metricValue = fmt.Sprintf("%.0f", *protobuffer.Gauge.Value)
				} else if protobuffer.Counter != nil {
					metricValue = fmt.Sprintf("%.0f", *protobuffer.Counter.Value)
				}

				// Desc{fqName: "aerospike_namespac_memory_free_pct", help: "memory free pct", constLabels: {}, variableLabels: [cluster_name service ns]}
				metricNameFromDesc := extractMetricNameFromDesc(description)
				namespaceFromLabel := extractNamespaceFromLabel(metricLabel)

				// key will be like namespace/<metric_name>, this we use this check during assertion
				keyName := makeKeyname(namespaceFromLabel, metricNameFromDesc, true)
				lOutputValues[keyName] = metricValue
				lOutputLabels[keyName] = metricLabel

			case <-time.After(1 * time.Second):
				domore = 0

			} // end select
		}

		// loop each namespace and compare the label and value
		arrNames := strings.Split(pass2Metrics["namespaces"], ";")

		for nsIndex := range arrNames {
			tnsForNamespace := arrNames[nsIndex]
			fmt.Println("Running test data assertion for namespace : ", tnsForNamespace)
			lExpectedMetricNamedValues, lExpectedMetricLabels := createNamespaceWatcherExpectedOutputs(tnsForNamespace, true)

			for key := range lOutputValues {
				// fmt.Println(key)
				// fmt.Println(values)
				expectedValues := lExpectedMetricNamedValues[key]
				expectedLabels := lExpectedMetricLabels[key]
				outputMetricValues := lOutputValues[key]
				outpuMetrictLabels := lOutputLabels[key]

				// assert - only if the value belongs to the namespace we read expected values and processing
				if strings.HasSuffix(key, tnsForNamespace) {
					assert.Contains(t, expectedValues, outputMetricValues)
					assert.Contains(t, expectedLabels, outpuMetrictLabels)
				}
			}

		}
	} else {
		fmt.Println(" Failed Refreshing, error: ", err)
	}

}
                                                                                                                                     aerospike-prometheus-exporter/._watcher_node_stats.go                                               000644  000765  000024  00000000243 14426445750 024477  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/watcher_node_stats.go                                       000644  000765  000024  00000000210 14426445750 026225  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683639272.903754149
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/watcher_node_stats.go                                                 000644  000765  000024  00000017763 14426445750 024301  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"github.com/prometheus/client_golang/prometheus"

	log "github.com/sirupsen/logrus"
)

// Node raw metrics
// gauge: true, counter: false
var statsRawMetrics = map[string]metricType{
	"cluster_size":                          mtGauge,
	"cluster_min_compatibility_id":          mtGauge,
	"cluster_max_compatibility_id":          mtGauge,
	"cluster_integrity":                     mtGauge,
	"cluster_is_member":                     mtGauge,
	"cluster_clock_skew_stop_writes_sec":    mtGauge,
	"cluster_clock_skew_ms":                 mtGauge,
	"cluster_generation":                    mtCounter,
	"uptime":                                mtCounter,
	"system_total_cpu_pct":                  mtGauge,
	"system_user_cpu_pct":                   mtGauge,
	"system_kernel_cpu_pct":                 mtGauge,
	"process_cpu_pct":                       mtGauge,
	"system_free_mem_pct":                   mtGauge,
	"heap_allocated_kbytes":                 mtGauge,
	"heap_active_kbytes":                    mtGauge,
	"heap_mapped_kbytes":                    mtGauge,
	"heap_efficiency_pct":                   mtGauge,
	"heap_site_count":                       mtGauge,
	"objects":                               mtGauge,
	"tombstones":                            mtGauge,
	"tsvc_queue":                            mtGauge,
	"info_queue":                            mtGauge,
	"rw_in_progress":                        mtGauge,
	"proxy_in_progress":                     mtGauge,
	"tree_gc_queue":                         mtGauge,
	"client_connections":                    mtGauge,
	"heartbeat_connections":                 mtGauge,
	"fabric_connections":                    mtGauge,
	"client_connections_opened":             mtCounter,
	"client_connections_closed":             mtCounter,
	"heartbeat_connections_opened":          mtCounter,
	"heartbeat_connections_closed":          mtCounter,
	"fabric_connections_opened":             mtCounter,
	"fabric_connections_closed":             mtCounter,
	"batch_index_proto_uncompressed_pct":    mtGauge,
	"batch_index_proto_compression_ratio":   mtGauge,
	"heartbeat_received_self":               mtCounter,
	"heartbeat_received_foreign":            mtCounter,
	"reaped_fds":                            mtCounter,
	"info_complete":                         mtCounter,
	"demarshal_error":                       mtCounter,
	"early_tsvc_client_error":               mtCounter,
	"early_tsvc_from_proxy_error":           mtCounter,
	"early_tsvc_batch_sub_error":            mtCounter,
	"early_tsvc_from_proxy_batch_sub_error": mtCounter,
	"early_tsvc_udf_sub_error":              mtCounter,
	"early_tsvc_ops_sub_error":              mtCounter,
	"batch_index_initiate":                  mtCounter,
	"batch_index_queue":                     mtGauge,
	"batch_index_complete":                  mtCounter,
	"batch_index_error":                     mtCounter,
	"batch_index_timeout":                   mtCounter,
	"batch_index_delay":                     mtCounter,
	"batch_index_unused_buffers":            mtGauge,
	"batch_index_huge_buffers":              mtGauge,
	"batch_index_created_buffers":           mtGauge,
	"batch_index_destroyed_buffers":         mtCounter,
	"scans_active":                          mtGauge,
	"queries_active":                        mtGauge,
	"query_short_running":                   mtCounter,
	"query_long_running":                    mtCounter,
	"sindex_ucgarbage_found":                mtCounter,
	"sindex_gc_retries":                     mtCounter,
	"sindex_gc_list_creation_time":          mtGauge,
	"sindex_gc_list_deletion_time":          mtGauge,
	"sindex_gc_objects_validated":           mtCounter,
	"sindex_gc_garbage_found":               mtCounter,
	"sindex_gc_garbage_cleaned":             mtCounter,
	"time_since_rebalance":                  mtGauge,
	"migrate_allowed":                       mtCounter,
	"migrate_partitions_remaining":          mtGauge,
	"fabric_bulk_send_rate":                 mtGauge,
	"fabric_bulk_recv_rate":                 mtGauge,
	"fabric_ctrl_send_rate":                 mtGauge,
	"fabric_ctrl_recv_rate":                 mtGauge,
	"fabric_meta_send_rate":                 mtGauge,
	"fabric_meta_recv_rate":                 mtGauge,
	"fabric_rw_send_rate":                   mtGauge,
	"fabric_rw_recv_rate":                   mtGauge,
	"dlog_used_objects":                     mtGauge,
	"dlog_free_pct":                         mtGauge,
	"dlog_logged":                           mtGauge,
	"dlog_relogged":                         mtCounter,
	"dlog_processed_main":                   mtCounter,
	"dlog_processed_replica":                mtCounter,
	"dlog_processed_link_down":              mtCounter,
	"dlog_overwritten_error":                mtCounter,
	"xdr_ship_success":                      mtCounter,
	"xdr_ship_delete_success":               mtCounter,
	"xdr_ship_source_error":                 mtCounter,
	"xdr_ship_destination_error":            mtCounter,
	"xdr_ship_destination_permanent_error":  mtCounter,
	"xdr_ship_fullrecord":                   mtCounter,
	"xdr_ship_bytes":                        mtCounter,
	"xdr_ship_inflight_objects":             mtGauge,
	"xdr_ship_outstanding_objects":          mtGauge,
	"xdr_ship_latency_avg":                  mtGauge,
	"xdr_ship_compression_avg_pct":          mtGauge,
	"xdr_read_success":                      mtCounter,
	"xdr_read_error":                        mtCounter,
	"xdr_read_notfound":                     mtCounter,
	"xdr_read_latency_avg":                  mtGauge,
	"xdr_read_active_avg_pct":               mtGauge,
	"xdr_read_idle_avg_pct":                 mtGauge,
	"xdr_read_reqq_used":                    mtGauge,
	"xdr_read_respq_used":                   mtGauge,
	"xdr_read_reqq_used_pct":                mtGauge,
	"xdr_read_txnq_used":                    mtGauge,
	"xdr_read_txnq_used_pct":                mtGauge,
	"xdr_relogged_incoming":                 mtGauge,
	"xdr_relogged_outgoing":                 mtGauge,
	"xdr_queue_overflow_error":              mtCounter,
	"xdr_active_failed_node_sessions":       mtGauge,
	"xdr_active_link_down_sessions":         mtGauge,
	"xdr_hotkey_fetch":                      mtCounter,
	"xdr_hotkey_skip":                       mtCounter,
	"xdr_unknown_namespace_error":           mtCounter,
	"xdr_timelag":                           mtGauge,
	"xdr_throughput":                        mtGauge,
	"xdr_global_lastshiptime":               mtGauge,
	"threads_joinable":                      mtGauge,
	"threads_detached":                      mtGauge,
	"threads_pool_total":                    mtGauge,
	"threads_pool_active":                   mtGauge,
	"failed_best_practices":                 mtGauge,
}

type StatsWatcher struct{}

func (sw *StatsWatcher) describe(ch chan<- *prometheus.Desc) {}

func (sw *StatsWatcher) passOneKeys() []string {
	return nil
}

func (sw *StatsWatcher) passTwoKeys(rawMetrics map[string]string) []string {
	return []string{"statistics"}
}

// Filtered node statistics. Populated by getFilteredMetrics() based on config.Aerospike.NodeMetricsAllowlist, config.Aerospike.NodeMetricsBlocklist and statsRawMetrics.
var nodeMetrics map[string]metricType

func (sw *StatsWatcher) refresh(o *Observer, infoKeys []string, rawMetrics map[string]string, ch chan<- prometheus.Metric) error {
	log.Tracef("node-stats:%s", rawMetrics["statistics"])

	if nodeMetrics == nil {
		nodeMetrics = getFilteredMetrics(statsRawMetrics, config.Aerospike.NodeMetricsAllowlist, config.Aerospike.NodeMetricsAllowlistEnabled, config.Aerospike.NodeMetricsBlocklist)
	}

	statsObserver := make(MetricMap, len(nodeMetrics))
	for m, t := range nodeMetrics {
		statsObserver[m] = makeMetric("aerospike_node_stats", m, t, config.AeroProm.MetricLabels, "cluster_name", "service")
	}

	stats := parseStats(rawMetrics["statistics"], ";")

	for stat, pm := range statsObserver {
		v, exists := stats[stat]
		if !exists {
			// not found
			continue
		}

		pv, err := tryConvert(v)
		if err != nil {
			continue
		}

		ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, pv, rawMetrics[ikClusterName], rawMetrics[ikService])
	}

	return nil
}
             aerospike-prometheus-exporter/._watcher_sets.go                                                     000644  000765  000024  00000000243 14426446012 023302  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/watcher_sets.go                                             000644  000765  000024  00000000210 14426446012 025030  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683639306.026572192
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/watcher_sets.go                                                       000644  000765  000024  00000003756 14426446012 023101  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"strings"

	"github.com/prometheus/client_golang/prometheus"

	log "github.com/sirupsen/logrus"
)

// Set Raw metrics
var setRawMetrics = map[string]metricType{
	"objects":           mtGauge,
	"tombstones":        mtGauge,
	"memory_data_bytes": mtGauge,
	"device_data_bytes": mtGauge,
	"truncate_lut":      mtGauge,
	"stop-writes-count": mtGauge,
	"stop-writes-size":  mtGauge,
	"disable-eviction":  mtGauge,
	"index_populating":  mtGauge,
	"sindexes":          mtGauge,
	"enable-index":      mtGauge,
}

type SetWatcher struct{}

func (sw *SetWatcher) describe(ch chan<- *prometheus.Desc) {}

func (sw *SetWatcher) passOneKeys() []string {
	return nil
}

func (sw *SetWatcher) passTwoKeys(rawMetrics map[string]string) []string {
	return []string{"sets"}
}

// Filtered set metrics. Populated by getFilteredMetrics() based on config.Aerospike.SetMetricsAllowlist, config.Aerospike.SetMetricsBlocklist and setRawMetrics.
var setMetrics map[string]metricType

func (sw *SetWatcher) refresh(o *Observer, infoKeys []string, rawMetrics map[string]string, ch chan<- prometheus.Metric) error {
	setStats := strings.Split(rawMetrics["sets"], ";")
	log.Tracef("set-stats:%v", setStats)

	if setMetrics == nil {
		setMetrics = getFilteredMetrics(setRawMetrics, config.Aerospike.SetMetricsAllowlist, config.Aerospike.SetMetricsAllowlistEnabled, config.Aerospike.SetMetricsBlocklist)
	}

	for i := range setStats {
		setObserver := make(MetricMap, len(setMetrics))
		for m, t := range setMetrics {
			setObserver[m] = makeMetric("aerospike_sets", m, t, config.AeroProm.MetricLabels, "cluster_name", "service", "ns", "set")
		}

		stats := parseStats(setStats[i], ":")
		for stat, pm := range setObserver {
			v, exists := stats[stat]
			if !exists {
				// not found
				continue
			}

			pv, err := tryConvert(v)
			if err != nil {
				continue
			}

			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, pv, rawMetrics[ikClusterName], rawMetrics[ikService], stats["ns"], stats["set"])
		}
	}

	return nil
}
                  aerospike-prometheus-exporter/._watcher_sindex.go                                                   000644  000765  000024  00000000243 14426445772 023632  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/watcher_sindex.go                                           000644  000765  000024  00000000210 14426445772 025360  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683639290.033129449
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/watcher_sindex.go                                                     000644  000765  000024  00000007327 14426445772 023427  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"strings"

	"github.com/prometheus/client_golang/prometheus"

	log "github.com/sirupsen/logrus"
)

// Sindex raw metrics
var sindexRawMetrics = map[string]metricType{
	"keys":                      mtGauge, // removed in server6.0
	"entries":                   mtGauge,
	"ibtr_memory_used":          mtGauge, // removed in server6.0
	"nbtr_memory_used":          mtGauge, // removed in server6.0
	"load_pct":                  mtGauge,
	"loadtime":                  mtGauge,   // removed in server6.0
	"write_success":             mtCounter, // removed in server6.0
	"write_error":               mtCounter, // removed in server6.0
	"delete_success":            mtCounter, // removed in server6.0
	"delete_error":              mtCounter, // removed in server6.0
	"stat_gc_recs":              mtCounter,
	"query_basic_complete":      mtCounter, // removed in server6.0
	"query_basic_error":         mtCounter, // removed in server6.0
	"query_basic_abort":         mtCounter, // removed in server6.0
	"query_basic_avg_rec_count": mtGauge,   // removed in server6.0
	"histogram":                 mtGauge,   // removed in server6.0
	"memory_used":               mtGauge,   // deprecated in server6.3 version and replaced by used_bytes
	"used_bytes":                mtGauge,   // added in server6.3 represents memory used by data (aka memory_used)
	"load_time":                 mtGauge,
	"entries_per_rec":           mtGauge,
	"entries_per_bval":          mtGauge,
}

type SindexWatcher struct {
}

func (siw *SindexWatcher) describe(ch chan<- *prometheus.Desc) {}

func (siw *SindexWatcher) passOneKeys() []string {
	if config.Aerospike.DisableSindexMetrics {
		// disabled
		return nil
	}

	return []string{"sindex"}
}

func (siw *SindexWatcher) passTwoKeys(rawMetrics map[string]string) (sindexCommands []string) {
	if config.Aerospike.DisableSindexMetrics {
		// disabled
		return nil
	}

	sindexesMeta := strings.Split(rawMetrics["sindex"], ";")
	sindexCommands = siw.getSindexCommands(sindexesMeta)

	return sindexCommands
}

// getSindexCommands returns list of commands to fetch sindex statistics
func (siw *SindexWatcher) getSindexCommands(sindexesMeta []string) (sindexCommands []string) {
	for _, sindex := range sindexesMeta {
		stats := parseStats(sindex, ":")
		sindexCommands = append(sindexCommands, "sindex/"+stats["ns"]+"/"+stats["indexname"])
	}

	return sindexCommands
}

var sindexMetrics map[string]metricType

func (siw *SindexWatcher) refresh(o *Observer, infoKeys []string, rawMetrics map[string]string, ch chan<- prometheus.Metric) error {
	if config.Aerospike.DisableSindexMetrics {
		// disabled
		return nil
	}

	if sindexMetrics == nil {
		sindexMetrics = getFilteredMetrics(sindexRawMetrics, config.Aerospike.SindexMetricsAllowlist, config.Aerospike.SindexMetricsAllowlistEnabled, config.Aerospike.SindexMetricsBlocklist)
	}

	for _, sindex := range infoKeys {
		sindexInfoKey := strings.ReplaceAll(sindex, "sindex/", "")
		sindexInfoKeySplit := strings.Split(sindexInfoKey, "/")
		nsName := sindexInfoKeySplit[0]
		sindexName := sindexInfoKeySplit[1]
		log.Tracef("sindex-stats:%s:%s:%s", nsName, sindexName, rawMetrics[sindex])
		sindexObserver := make(MetricMap, len(sindexMetrics))
		for m, t := range sindexMetrics {
			sindexObserver[m] = makeMetric("aerospike_sindex", m, t, config.AeroProm.MetricLabels, "cluster_name", "service", "ns", "sindex")
		}

		stats := parseStats(rawMetrics[sindex], ";")
		for stat, pm := range sindexObserver {
			v, exists := stats[stat]
			if !exists {
				// not found
				continue
			}

			pv, err := tryConvert(v)
			if err != nil {
				continue
			}

			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, pv, rawMetrics[ikClusterName], rawMetrics[ikService], nsName, sindexName)
		}
	}

	return nil
}
                                                                                                                                                                                                                                                                                                         aerospike-prometheus-exporter/._watcher_users.go                                                    000644  000765  000024  00000000243 14426446017 023472  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/watcher_users.go                                            000644  000765  000024  00000000206 14426446017 025225  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         28 mtime=1683639311.0397018
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                          aerospike-prometheus-exporter/watcher_users.go                                                      000644  000765  000024  00000013642 14426446017 023264  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"fmt"
	"time"

	"github.com/aerospike/aerospike-client-go/v6/types"
	"github.com/prometheus/client_golang/prometheus"

	aero "github.com/aerospike/aerospike-client-go/v6"
	log "github.com/sirupsen/logrus"
)

var (
	shouldFetchUserStatistics bool = true
)

type UserWatcher struct{}

func (uw *UserWatcher) describe(ch chan<- *prometheus.Desc) {}

func (uw *UserWatcher) passOneKeys() []string {
	// "build" info key should be returned here,
	// but it is also being sent by LatencyWatcher.passOneKeys(),
	// hence skipping here.
	return nil
}

func (uw *UserWatcher) passTwoKeys(rawMetrics map[string]string) []string {
	return nil
}

func (uw *UserWatcher) refresh(o *Observer, infoKeys []string, rawMetrics map[string]string, ch chan<- prometheus.Metric) error {
	// check if security configurations are enabled
	if config.Aerospike.User == "" && config.Aerospike.Password == "" {
		return nil
	}

	// check if we should fetch user metrics
	if !shouldFetchUserStatistics {
		log.Debug("Fetching user statistics is disabled")
		return nil
	}

	// validate aerospike build version
	// support for user statistics is added in aerospike 5.6
	var err error
	ok, err := buildVersionGreaterThanOrEqual(rawMetrics, "5.6.0.0")
	if err != nil {
		// just log warning. don't send an error back
		log.Warn(err)
		return nil
	}

	if !ok {
		// disable user statisitcs if build version is not >= 5.6.0.0
		log.Debug("Aerospike version doesn't support user statistics")
		shouldFetchUserStatistics = false
		return nil
	}

	admPlcy := aero.NewAdminPolicy()
	admPlcy.Timeout = time.Duration(config.Aerospike.Timeout) * time.Second
	admCmd := aero.NewAdminCommand(nil)

	var users []*aero.UserRoles
	var aeroErr aero.Error

	for i := 0; i < retryCount; i++ {
		// Validate existing connection
		if o.conn == nil || !o.conn.IsConnected() {
			// Create new connection
			o.conn, err = o.newConnection()
			if err != nil {
				log.Debug(err)
				continue
			}
		}

		// query users
		users, aeroErr = admCmd.QueryUsers(o.conn, admPlcy)
		if aeroErr != nil {
			// Do not retry if there's role violation.
			// This could be a permanent error leading to unnecessary errors on server end.
			if aeroErr.Matches(types.ROLE_VIOLATION) {
				shouldFetchUserStatistics = false
				log.Debugf("Unable to fetch user statistics: %s", aeroErr.Error())
				break
			}

			err = fmt.Errorf(aeroErr.Error())
			log.Debugf("Error while querying users: %s", aeroErr.Error())
			continue
		}

		break
	}

	allowedUsersList := make(map[string]struct{})
	blockedUsersList := make(map[string]struct{})

	if config.Aerospike.UserMetricsUsersAllowlistEnabled {
		for _, allowedUser := range config.Aerospike.UserMetricsUsersAllowlist {
			allowedUsersList[allowedUser] = struct{}{}
		}
	}

	if len(config.Aerospike.UserMetricsUsersBlocklist) > 0 {
		for _, blockedUser := range config.Aerospike.UserMetricsUsersBlocklist {
			blockedUsersList[blockedUser] = struct{}{}
		}
	}

	for _, user := range users {
		// check if user is allowed
		if config.Aerospike.UserMetricsUsersAllowlistEnabled {
			if _, ok := allowedUsersList[user.User]; !ok {
				continue
			}
		}

		// check if user is blocked
		if len(config.Aerospike.UserMetricsUsersBlocklist) > 0 {
			if _, ok := blockedUsersList[user.User]; ok {
				continue
			}
		}

		// Connections in use
		pm := makeMetric("aerospike_users", "conns_in_use", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "user")
		ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, float64(user.ConnsInUse), rawMetrics[ikClusterName], rawMetrics[ikService], user.User)

		if len(user.ReadInfo) >= 4 && len(user.WriteInfo) >= 4 {
			// User read info statistics
			pm = makeMetric("aerospike_users", "read_quota", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "user")
			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, float64(user.ReadInfo[0]), rawMetrics[ikClusterName], rawMetrics[ikService], user.User)
			pm = makeMetric("aerospike_users", "read_single_record_tps", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "user")
			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, float64(user.ReadInfo[1]), rawMetrics[ikClusterName], rawMetrics[ikService], user.User)
			pm = makeMetric("aerospike_users", "read_scan_query_rps", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "user")
			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, float64(user.ReadInfo[2]), rawMetrics[ikClusterName], rawMetrics[ikService], user.User)
			pm = makeMetric("aerospike_users", "limitless_read_scan_query", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "user")
			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, float64(user.ReadInfo[3]), rawMetrics[ikClusterName], rawMetrics[ikService], user.User)

			// User write info statistics
			pm = makeMetric("aerospike_users", "write_quota", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "user")
			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, float64(user.WriteInfo[0]), rawMetrics[ikClusterName], rawMetrics[ikService], user.User)
			pm = makeMetric("aerospike_users", "write_single_record_tps", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "user")
			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, float64(user.WriteInfo[1]), rawMetrics[ikClusterName], rawMetrics[ikService], user.User)
			pm = makeMetric("aerospike_users", "write_scan_query_rps", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "user")
			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, float64(user.WriteInfo[2]), rawMetrics[ikClusterName], rawMetrics[ikService], user.User)
			pm = makeMetric("aerospike_users", "limitless_write_scan_query", mtGauge, config.AeroProm.MetricLabels, "cluster_name", "service", "user")
			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, float64(user.WriteInfo[3]), rawMetrics[ikClusterName], rawMetrics[ikService], user.User)
		}
	}

	return err
}
                                                                                              aerospike-prometheus-exporter/._watcher_xdr.go                                                      000644  000765  000024  00000000243 14426445776 023141  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                             Mac OS X            	   2   q      �                                      ATTR       �   �                     �     com.apple.provenance   �>qj�-�:                                                                                                                                                                                                                                                                                                                                                             aerospike-prometheus-exporter/PaxHeader/watcher_xdr.go                                              000644  000765  000024  00000000210 14426445776 024667  x                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         30 mtime=1683639294.730437618
57 LIBARCHIVE.xattr.com.apple.provenance=AQAAnj5xav0t9To
49 SCHILY.xattr.com.apple.provenance=  �>qj�-�:
                                                                                                                                                                                                                                                                                                                                                                                        aerospike-prometheus-exporter/watcher_xdr.go                                                        000644  000765  000024  00000005133 14426445776 022727  0                                                                                                    ustar 00phaniram                        staff                           000000  000000                                                                                                                                                                         package main

import (
	"strings"

	"github.com/prometheus/client_golang/prometheus"

	log "github.com/sirupsen/logrus"
)

// XDR raw metrics
var xdrRawMetrics = map[string]metricType{
	"lag":                mtGauge,
	"in_queue":           mtGauge,
	"in_progress":        mtGauge,
	"recoveries_pending": mtGauge,
	"uncompressed_pct":   mtGauge,
	"compression_ratio":  mtGauge,
	"throughput":         mtGauge,
	"latency_ms":         mtGauge,
	"lap_us":             mtGauge,
	"nodes":              mtGauge,
	"success":            mtCounter,
	"abandoned":          mtCounter,
	"not_found":          mtCounter,
	"filtered_out":       mtCounter,
	"retry_conn_reset":   mtCounter,
	"retry_dest":         mtCounter,
	"recoveries":         mtCounter,
	"hot_keys":           mtCounter,
	"retry_no_node":      mtCounter,
	"bytes_shipped":      mtCounter,
}

type XdrWatcher struct{}

func (xw *XdrWatcher) describe(ch chan<- *prometheus.Desc) {}

func (xw *XdrWatcher) passOneKeys() []string {
	return []string{"get-config:context=xdr"}
}

func (xw *XdrWatcher) passTwoKeys(rawMetrics map[string]string) []string {
	res := rawMetrics["get-config:context=xdr"]
	list := parseStats(res, ";")
	dcsList := strings.Split(list["dcs"], ",")

	var infoKeys []string
	for _, dc := range dcsList {
		if dc != "" {
			infoKeys = append(infoKeys, "get-stats:context=xdr;dc="+dc)
		}
	}

	return infoKeys
}

// Filtered XDR metrics. Populated by getFilteredMetrics() based on the config.Aerospike.XdrMetricsAllowlist, config.Aerospike.XdrMetricsBlocklist and xdrRawMetrics.
var xdrMetrics map[string]metricType

func (xw *XdrWatcher) refresh(o *Observer, infoKeys []string, rawMetrics map[string]string, ch chan<- prometheus.Metric) error {

	if xdrMetrics == nil {
		xdrMetrics = getFilteredMetrics(xdrRawMetrics, config.Aerospike.XdrMetricsAllowlist, config.Aerospike.XdrMetricsAllowlistEnabled, config.Aerospike.XdrMetricsBlocklist)
	}

	for _, dc := range infoKeys {
		dcName := strings.ReplaceAll(dc, "get-stats:context=xdr;dc=", "")
		log.Tracef("xdr-stats:%s:%s", dcName, rawMetrics[dc])

		xdrObserver := make(MetricMap, len(xdrMetrics))
		for m, t := range xdrMetrics {
			xdrObserver[m] = makeMetric("aerospike_xdr", m, t, config.AeroProm.MetricLabels, "cluster_name", "service", "dc")
		}

		stats := parseStats(rawMetrics[dc], ";")
		for stat, pm := range xdrObserver {
			v, exists := stats[stat]
			if !exists {
				// not found
				continue
			}

			pv, err := tryConvert(v)
			if err != nil {
				continue
			}

			ch <- prometheus.MustNewConstMetric(pm.desc, pm.valueType, pv, rawMetrics[ikClusterName], rawMetrics[ikService], dcName)
		}
	}

	return nil
}
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     