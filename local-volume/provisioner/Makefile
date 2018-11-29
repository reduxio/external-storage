# Copyright 2017 The Kubernetes Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.


REGISTRY = quay.io/reduxio
VERSION = latest
IMAGE = $(REGISTRY)/local-volume-provisioner:$(VERSION)


.PHONY: all
all:
	go get -v -d ./cmd
	CGO_ENABLED=0 GOOS=linux go build -a -ldflags '-extldflags "-static"' -o local-volume-provisioner ./cmd


.PHONY: image
image:
	cp local-volume-provisioner deployment/docker
	sudo docker login -u="reduxio+buzi" -p="PVHGFW9YERAOPYCNXKC8FJMGLQ0EN9S2O2UX5R01G3V86W714MZ65Q5FGJHN6EOF" quay.io
	@echo "Building image"
	sudo docker build -t $(IMAGE) deployment/docker
	@echo Pushing image
	sudo docker push $(IMAGE)
	@echo Image was pushed successfully

.PHONY: clean
clean:
	rm -f local-volume-provisioner
	rm -f deployment/docker/local-volume-provisioner
	go clean -cache -r -i
